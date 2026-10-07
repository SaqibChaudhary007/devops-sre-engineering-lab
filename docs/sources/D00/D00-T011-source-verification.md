# D00-T011 Source Verification — Distributed Systems Foundations

## Verification Goal

Verify the core claims in **00.11 — Distributed Systems Foundations** against authoritative distributed-systems literature and current guidance from AWS, Google SRE, Microsoft Azure Architecture Center, Google Cloud Pub/Sub, and the original CAP literature.

## Verification Status

**Result:** Core claims verified with important nuances around ambiguous failure, retries, idempotency, message delivery semantics, consistency, CAP, failure detection, resilience patterns, and queue/backpressure behavior.

**Evidence level:** E2 — supported by primary/authoritative engineering guidance and foundational papers.

This topic remains at the D00 mental-model level. Deep consensus algorithms, formal consistency models, distributed database internals, Kafka/MQ internals, Raft/Paxos, service meshes, and protocol implementation belong to later domains.

---

## Verified Claim Map

| Topic claim | Verification | Primary source |
|---|---|---|
| Distributed systems introduce independent failure, latency, and uncertainty | Verified | AWS Builders' Library / Well-Architected |
| A timeout does not prove whether a remote operation executed | Verified | AWS Builders' Library distributed-systems guidance |
| Retries can recover transient faults but can amplify overload | Verified | AWS Builders' Library; Google SRE |
| Exponential backoff and jitter reduce synchronized retry pressure | Verified | AWS Builders' Library; Google SRE |
| Retries should be bounded and applied selectively | Verified | Google SRE; Azure transient-fault guidance |
| Circuit breakers stop repeated calls to a likely failing dependency | Verified | Azure Circuit Breaker pattern |
| Bulkheads isolate resource pools and limit failure propagation | Verified | Azure Bulkhead pattern |
| Queues decouple producers/consumers and buffer variable load | Verified | Azure Competing Consumers pattern |
| At-least-once delivery can result in duplicate processing | Verified | Google Cloud Pub/Sub |
| Exactly-once delivery guarantees are scoped and system-specific | Verified with strong nuance | Google Cloud Pub/Sub |
| Ordering guarantees are scoped, not universal | Verified | Google Cloud Pub/Sub ordering behavior |
| CAP applies specifically to consistency/availability trade-offs during partition | Verified | Gilbert & Lynch 2002; Gilbert & Lynch 2012 |
| Replica placement across failure domains matters for availability | Verified | Google SRE Managing Critical State |
| Cascading failures can arise from overload, retries, and dependency chains | Verified | Google SRE Cascading Failures |
| Graceful degradation and load shedding can preserve useful service | Verified | Google SRE |
| Queue backlog and downstream capacity require flow-control/backpressure thinking | Verified | AWS Builders' Library; Google Pub/Sub subscriber flow control |

---

# Primary / Authoritative Sources

## 1. AWS Builders' Library — Distributed-System Failure and Retry Behavior

- https://aws.amazon.com/builders-library/
- https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/
- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_prevent_interaction_failure_identify.html

Supports:

- remote calls fail in more ways than local calls
- latency and network uncertainty are normal distributed-system concerns
- timeouts, retries, and backoff are core resilience tools
- distributed systems should be designed expecting partial failure
- larger systems turn rare failure modes into regular operational events

### Important nuance

A timeout does not uniquely identify the failure.

The caller may not know whether:

- the request never arrived
- the remote side processed it
- the response was lost
- the remote side is merely slow

Therefore:

> Timeout means uncertainty, not proof of non-execution.

---

## 2. Google SRE — Cascading Failures and Retry Amplification

- https://sre.google/sre-book/addressing-cascading-failures/
- https://sre.google/sre-book/service-best-practices/

Supports:

- retries can amplify load
- retries at multiple layers multiply downstream attempts
- retry budgets can limit aggregate retry pressure
- exponential backoff with jitter reduces synchronized retry storms
- overload can create positive-feedback cascading failures
- graceful degradation and traffic shedding can preserve availability

### Important nuance

Retry is not universally beneficial.

A strong D00 rule is:

~~~text
Retry only when:
- the failure is plausibly transient
- the operation is safe to repeat
- the dependency is not being overwhelmed
- retry count / budget is bounded
~~~

---

## 3. Microsoft Azure Architecture Center — Circuit Breaker and Bulkhead

- https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker
- https://learn.microsoft.com/en-us/azure/architecture/patterns/bulkhead
- https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults

Supports:

- circuit breaker prevents repeated calls to a dependency likely to fail
- retry and circuit breaker solve different problems
- bulkheads isolate resource pools to contain failure
- retries should be finite and use backoff
- aggregate retry budgets can protect struggling dependencies

### Important nuance

Circuit breaker does not fix a dependency.

It protects the caller/system by failing fast while the dependency recovers.

Bulkhead does not remove failure.

It limits how far failure can spread.

---

## 4. Microsoft Azure Architecture Center — Queues / Competing Consumers

- https://learn.microsoft.com/en-us/azure/architecture/patterns/competing-consumers

Supports:

- queues decouple producers from consumers
- asynchronous processing can absorb variable load
- multiple consumers can improve throughput and availability
- failed consumers need not block producers
- delivery can be at-least-once, requiring duplicate-safe processing

### Important nuance

Queues trade synchronous coupling for new responsibilities:

- backlog monitoring
- duplicate handling
- ordering
- consumer scaling
- poison/dead-letter behavior
- end-to-end latency

---

## 5. Google Cloud Pub/Sub — Delivery Semantics and Ordering

- https://cloud.google.com/pubsub/docs/subscription-overview
- https://cloud.google.com/pubsub/docs/exactly-once-delivery
- https://cloud.google.com/pubsub/docs/subscribe-best-practices

Supports:

- default at-least-once delivery
- duplicate delivery can occur
- ordering is optional and scoped
- exactly-once delivery is a product-specific feature with explicit limits
- flow control protects subscribers from unbounded outstanding work

### Important nuance

The topic should avoid saying "exactly once is impossible" as an absolute statement.

A more accurate mental model is:

> Exactly-once guarantees are scoped to specific systems and conditions, while exactly-once **business effect** still requires end-to-end application design.

Even with product-level exactly-once delivery, application-side duplicate publishes, region scope, acknowledgment behavior, and side-effect handling still matter.

---

## 6. Gilbert & Lynch — CAP Theorem

Foundational reference:

- https://dl.acm.org/doi/10.1145/564585.564601
- https://dspace.mit.edu/handle/1721.1/79112

Supports:

- in the asynchronous network model, consistency, availability, and partition tolerance cannot all be guaranteed simultaneously
- the practical concern is behavior during partition
- CAP is not a permanent "pick any two" architecture slogan

### Important nuance

D00 should teach:

> Under partition, systems face a consistency-vs-availability trade-off for affected operations.

Do not teach:

~~~text
Choose two forever.
~~~

Real systems make operation-specific and failure-specific trade-offs.

---

## 7. Google SRE — Distributed Consensus / Critical State

- https://sre.google/sre-book/managing-critical-state/

Supports:

- distributed consensus for critical state
- quorum-based decision making
- replica placement across failure domains
- availability consequences of poor replica placement
- coordination as a reliability concern

### Important nuance

Leader election, quorum, and consensus are related but not interchangeable.

At D00:

~~~text
Leader Election
→ selects coordinator

Quorum
→ enough participants for a decision

Consensus
→ nodes agree on a value/order despite failures
~~~

Deep protocol mechanics belong later.

---

# Verified Nuances / Corrections

## 1. Timeout = Ambiguity, Not Proof of Failure

A timeout only tells the caller that the result was not received within the deadline.

The remote operation might still have executed.

This directly motivates:

- request identity
- idempotency
- deduplication
- safe retry design

## 2. Retry Safety Depends on Operation Semantics

Retrying:

~~~text
Set status = ACTIVE
~~~

is different from retrying:

~~~text
Charge card
Add credits
Create shipment
~~~

Non-idempotent side effects need request identity/deduplication or another correctness mechanism.

## 3. Retry Amplification Is Multiplicative

If multiple layers each retry, one user request can create many downstream attempts.

Retry ownership should be deliberate.

Avoid independent retry policies at every layer.

## 4. Backoff Without Jitter Can Still Synchronize Clients

Exponential backoff lowers pressure.

Jitter reduces synchronized retry waves.

The two are complementary.

## 5. Circuit Breaker and Retry Are Different Controls

Retry assumes another attempt may succeed.

Circuit breaker stops repeated attempts when continued calling is likely harmful.

They can be combined carefully.

## 6. Exactly-Once Requires Scoped Language

Messaging products can provide exactly-once guarantees under defined conditions.

However:

> Exactly-once delivery is not the same as automatically guaranteeing one end-to-end business side effect.

Application behavior, duplicate publishing, external side effects, and transaction boundaries still matter.

## 7. Ordering Is Scoped

Ordering may be guaranteed:

- per key
- per partition
- per stream
- within one region or configuration

Do not teach universal global ordering unless the system explicitly provides it.

## 8. CAP Is a Partition-Time Trade-Off

The canonical D00 wording is valid when taught as:

~~~text
Partition occurs
→ cannot guarantee both:
   - one consistent view
   - full availability to all partitioned sides
~~~

Do not use "pick two" as the primary model.

## 9. Replica Count Is Not Availability

Replicas that share one:

- zone
- rack
- dependency
- network path
- storage system

can fail together.

Replication must be evaluated against actual failure domains.

## 10. Failure Detection Is Inference

Silence from another node can mean:

- failure
- overload
- pause
- network loss
- long latency

Heartbeats and timeouts create suspicion thresholds, not perfect knowledge.

## 11. Queues Buffer; They Do Not Create Infinite Capacity

A queue can absorb bursts and decouple producer/consumer timing.

If producers continuously exceed consumer capacity:

~~~text
Backlog
→ Latency
→ Storage / Memory Pressure
→ Operational Failure
~~~

Backpressure and capacity management are still required.

## 12. Graceful Degradation Can Be More Reliable Than Full-Service Failure

Under overload or dependency failure, intentionally reducing noncritical functionality can preserve critical user operations.

## 13. Cascading Failure Is Often Positive Feedback

A slow dependency can create:

~~~text
Longer Requests
→ More In-Flight Work
→ Resource Saturation
→ Retries
→ More Dependency Load
→ Wider Failure
~~~

Resilience patterns aim to break this feedback loop.

---

# Evidence Decision

The following D00-T011 areas are now eligible for **DOC-VERIFIED** status:

- distributed-system failure/latency mental model
- partial failure and ambiguous timeout
- retries and retry amplification
- backoff and jitter
- retry budgets
- circuit breaker
- bulkhead
- queue decoupling
- at-least-once delivery and duplicate handling
- scoped exactly-once guarantees
- scoped ordering guarantees
- CAP partition-time trade-off
- failure-domain-aware replication
- consensus/quorum high-level reasoning
- cascading failure
- graceful degradation
- flow-control/backpressure mental model

The following remain intentionally high-level previews pending deeper domains:

- PACELC
- formal consistency models
- logical clocks
- split-brain fencing protocols
- Raft/Paxos internals
- distributed transactions
- saga orchestration/choreography details
- cache-coherence algorithms
- sharding/rebalancing protocols

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured exercises:

- diagnose an ambiguous timeout
- classify safe/unsafe retry operations
- design an idempotency key
- model duplicate message delivery
- reason about replication lag/stale reads
- reason about CAP behavior during a partition
- model retry amplification across multiple layers
- design timeout/retry/backoff/jitter/circuit-breaker behavior
- model queue backlog and backpressure
- map replicas across failure domains
- trace one request with correlation/tracing data
- classify graceful-degradation choices

These become the D00-T011 practical package.

# D00-T011 — Applied Distributed Systems Scenario

## Scenario

A customer places an order through:

~~~text
Client
→ API Gateway
→ Order Service
→ Payment Service
→ Inventory Service
→ Queue
→ Fulfillment Worker
→ Database
~~~

Current behavior:

~~~text
- API timeout = 2 seconds
- Client retries up to 3 times
- Gateway retries up to 3 times
- Order Service retries Payment up to 3 times
- Payment charge is not idempotent
- Payment response is occasionally lost after successful charge
- Inventory reads come from a lagging replica
- Queue delivery is at-least-once
- One tenant creates 50% of queue traffic
- Consumer capacity is lower than producer rate during peak
- all three database replicas are in one availability zone
- Recommendation service is required for checkout
- logs have no common correlation ID
- the team says "CAP means choose two"
- the team says "exactly-once queue delivery guarantees one business effect"
~~~

## Task 1 — Map the Distributed Request Path

Identify every synchronous and asynchronous boundary.

Explain where partial failure can occur.

## Task 2 — Ambiguous Timeout

The Payment Service completes a charge, but the response is lost.

The caller times out.

Explain:

- what the caller knows
- what the caller does not know
- why immediate blind retry is dangerous
- what evidence is needed

## Task 3 — Retry Amplification

Calculate the maximum payment attempts if:

~~~text
Client attempts = 3
Gateway attempts = 3
Order Service payment attempts = 3
~~~

Explain the operational risk.

## Task 4 — Idempotency Design

Design a conceptual request-identity model for the charge operation.

Explain how repeated logical requests should behave.

## Task 5 — Retry Ownership

Choose a safer retry owner.

Explain why not every layer should retry independently.

## Task 6 — Backoff, Jitter, Circuit Breaker

Design a high-level policy for a slowing Payment Service using:

- bounded timeout
- bounded retry
- exponential backoff
- jitter
- circuit breaker

Explain the purpose of each control.

## Task 7 — Replication Lag

Inventory reads from a follower that is 5 seconds behind.

Explain:

- what stale read risk exists
- whether this is acceptable for checkout inventory
- which business rule determines the answer

## Task 8 — CAP Reasoning

A network partition isolates one database replica set from another.

Explain the consistency-versus-availability trade-off for order writes.

Do not use "pick two" as the answer.

## Task 9 — Failure Domains

All three database replicas are in one zone.

Explain why replica count alone is weak resilience evidence.

Design a better failure-domain model conceptually.

## Task 10 — Queue Backlog

Peak traffic:

~~~text
Producer = 3000 messages/min
Consumer capacity = 1800 messages/min
~~~

Explain what happens to backlog, latency, recovery time, and storage pressure.

## Task 11 — Backpressure

Design a conceptual response to sustained overload.

Include:

- producer slowing or admission control
- bounded outstanding work
- consumer scaling where justified
- lower-priority work shedding
- queue-depth alerting

## Task 12 — Hot Tenant

One tenant produces 50% of all queue traffic.

Explain why:

- average metrics may hide the problem
- partitioning can become uneven
- per-tenant or per-partition metrics matter

## Task 13 — At-Least-Once Delivery

A fulfillment message is delivered twice.

Explain how duplicate business effects can occur.

Design a deduplication/idempotency approach conceptually.

## Task 14 — Graceful Degradation

Recommendation Service fails.

Compare:

~~~text
A: Checkout fails completely
B: Checkout continues without recommendations
~~~

Explain when graceful degradation is safe and when it is not.

## Task 15 — Observability

Design an evidence model using:

- correlation ID
- traces
- logs
- metrics
- retry count
- queue depth
- replica lag
- dependency health
- deployment/change markers

## Task 16 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Impact
→ Request Identity
→ Timeline
→ Retry Path
→ Dependency State
→ Data Freshness
→ Queue State
→ Evidence
→ Recovery
~~~

### SRE

Connect the incident to:

- availability
- latency
- error rate
- saturation
- retry amplification
- backlog
- blast radius
- SLO impact

### Architect

Design safer boundaries for:

- retry ownership
- idempotency
- consistency per operation
- queue capacity
- failure domains
- graceful degradation
- observability

## Success Standard

A strong answer should explicitly reject:

- timeout = definite failure
- retry everywhere
- replica count = availability
- CAP = choose any two forever
- exactly-once transport = one business effect
- queue = infinite buffer

---
id: EXP-D00-018
domain: D00
topics:
  - D00-T011
level: L2-L3
type: experiment
status: draft
estimated_time: 60-80m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# EXP-D00-018 — Replication, Partition Trade-Offs, Backpressure, and Failure Domains

## Objective

Practice reasoning about replication lag, stale reads, network partitions, CAP trade-offs, queue backlog, backpressure, hot spots, and replica placement across failure domains.

## Safety

This is a local architecture exercise. No real partition injection, production manipulation, load testing, or destructive activity is required.

## Scenario

A service has:

~~~text
Leader copy in Zone A
Replica in Zone B
Replica in Zone C
Queue between API and Worker
Stable user request path across multiple services
~~~

The system experiences:

- intermittent network loss between zones
- increasing replica lag
- rising queue backlog
- one hot tenant
- worker capacity below producer rate

## 1. Replication Lag

Model:

~~~text
T0 Write commits on leader
T1 Client reads from follower
T2 Replica catches up
~~~

Explain what a stale read is.

Classify stale reads for:

- product recommendations
- user avatar
- payment balance
- inventory count during checkout
- audit record

Use Usually Acceptable, Usually Not Acceptable, or Depends on Business Rule.

## 2. Consistency as Business Requirement

For each operation define:

- what correctness means
- tolerable staleness
- user impact of stale data
- whether read availability can be traded for fresher data

## 3. Partition Scenario

Assume Zone A cannot communicate with Zone B, but both sides are otherwise running.

Compare:

~~~text
Choice A
Preserve one coordinated view
→ reject or pause some writes

Choice B
Keep serving writes on both sides
→ risk divergence/conflict
~~~

Explain why this is the useful D00 CAP mental model.

Do not reduce CAP to a permanent "pick two" slogan.

## 4. Failure Detection

A replica stops responding.

List possible causes:

- process failed
- network path broke
- replica overloaded
- long pause
- packet loss
- storage stall

Explain why missed heartbeats create suspicion rather than perfect knowledge.

## 5. Failure Domain Placement

Compare:

~~~text
Placement A
Replica 1 — Zone A
Replica 2 — Zone A
Replica 3 — Zone A

Placement B
Replica 1 — Zone A
Replica 2 — Zone B
Replica 3 — Zone C
~~~

Explain why three replicas do not imply equal resilience.

## 6. Queue Backlog

Initial:

~~~text
Producer rate = 1000 messages/min
Consumer capacity = 1200 messages/min
~~~

Later:

~~~text
Producer rate = 2000 messages/min
Consumer capacity = 1200 messages/min
~~~

Explain what happens to:

- queue depth
- end-to-end latency
- storage pressure
- recovery time

## 7. Backpressure

Design a conceptual overload response:

- slow producer
- reject lower-priority work
- cap outstanding work
- increase consumer capacity if justified
- preserve critical traffic

Explain why a queue does not create infinite downstream capacity.

## 8. Hot Tenant / Hot Partition

Assume one tenant produces 60% of all requests.

Discuss:

- why average CPU may still look acceptable
- how one partition can saturate
- why partition-key choice matters
- which metrics reveal hot spots

## 9. Graceful Degradation

A recommendation service becomes unavailable.

Compare:

~~~text
Model A
Entire checkout fails

Model B
Checkout continues
Recommendations omitted
~~~

Explain when graceful degradation is appropriate and when it would violate correctness.

## 10. Distributed Evidence

Model:

~~~text
Client
→ API
→ Service A
→ Queue Publish
→ Worker
→ Database
~~~

Define evidence:

- correlation ID
- trace/spans
- per-service logs
- queue depth
- replication lag
- error rate
- latency
- deployment/change markers

Explain which signals distinguish latency, backlog, stale reads, and dependency failure.

## 11. Senior Engineer Connection

Use:

~~~text
User Impact
→ Dependency Path
→ Reachability
→ Replica State
→ Lag / Freshness
→ Queue Depth
→ Capacity
→ Hot Spots
→ Evidence
→ Recovery
~~~

## 12. SRE Connection

Connect the scenario to availability, latency, saturation, backlog, freshness, graceful degradation, SLO impact, and recovery time.

## 13. Architect Connection

Design decisions should cover:

- consistency requirement per operation
- replica placement
- failure domains
- queue capacity
- backpressure
- partition strategy
- hot-key mitigation
- graceful degradation boundaries
- cross-service observability

## Validation Checklist

- [ ] Explained replication lag and stale reads
- [ ] Connected consistency to business semantics
- [ ] Explained partition-time consistency/availability trade-off
- [ ] Explained uncertainty in failure detection
- [ ] Compared replica placement across failure domains
- [ ] Modeled queue backlog growth
- [ ] Designed backpressure conceptually
- [ ] Identified hot-tenant/hot-partition risk
- [ ] Designed graceful degradation
- [ ] Built a cross-service evidence model

## Teach-Back

Explain: Replication, queues, and retries improve systems only when their lag, capacity, failure domains, and correctness trade-offs are understood.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

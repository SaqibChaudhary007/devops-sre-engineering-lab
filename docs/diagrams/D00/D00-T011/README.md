# D00-T011 Visual / Diagram Package — Distributed Systems Foundations

This package provides reusable diagrams for **00.11 — Distributed Systems Foundations**.

## Diagram Set

1. [DIA-D00-059 — Local Call vs Network Call](DIA-D00-059-local-call-vs-network-call.md)
2. [DIA-D00-060 — Partial Failure & Ambiguous Timeout](DIA-D00-060-partial-failure-ambiguous-timeout.md)
3. [DIA-D00-061 — Retry → Duplicate → Idempotency Key](DIA-D00-061-retry-duplicate-idempotency.md)
4. [DIA-D00-062 — Replication → Lag → Stale Read](DIA-D00-062-replication-lag-stale-read.md)
5. [DIA-D00-063 — Partition Trade-Off / CAP Mental Model](DIA-D00-063-partition-cap-mental-model.md)
6. [DIA-D00-064 — Timeout + Retry + Backoff + Circuit Breaker Failure Loop](DIA-D00-064-timeout-retry-backoff-circuit-breaker.md)

## Learning Progression

~~~text
Call
→ Wait
→ Timeout
→ Uncertainty
→ Retry Decision
→ Duplicate Safety
→ State / Replication
→ Partition Trade-Off
→ Recovery Controls
~~~

## Design Rules

- stay provider-neutral
- show uncertainty explicitly
- distinguish caller observation from remote reality
- show retries as additional load
- separate delivery guarantees from business-side-effect guarantees
- show replication lag and stale-read risk
- teach CAP as a partition-time consistency-versus-availability trade-off
- show resilience controls as bounded protections, not magical recovery
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Deep Raft/Paxos, formal consistency models, distributed database internals, Kafka/MQ semantics, sharding protocols, service meshes, and distributed transaction implementation belong to later domains.

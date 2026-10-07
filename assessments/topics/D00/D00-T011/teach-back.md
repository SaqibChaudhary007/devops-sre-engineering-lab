# D00-T011 — Teach-Back Assessment

## Goal

Demonstrate that you can explain distributed systems through uncertainty, correctness, and trade-offs without relying on slogans.

## Task A — Beginner

Explain:

- what a distributed system is
- why partial failure exists
- why a network call is different from a local call

## Task B — Timeout Challenge

Explain why:

~~~text
Timeout
≠
Proof the remote operation failed
~~~

Use one example where the operation succeeds but the caller still sees a timeout.

## Task C — Retry Challenge

Explain:

- when retry helps
- when retry amplifies failure
- why idempotency matters
- why every layer should not retry independently

## Task D — Delivery Semantics

Explain:

~~~text
At-most-once
At-least-once
Exactly-once delivery
Exactly-once business effect
~~~

Keep the distinction clear.

## Task E — Replication & Consistency

Explain:

- replication
- replication lag
- stale reads
- eventual consistency
- why business semantics determine acceptable staleness

## Task F — CAP

Explain CAP without saying only "choose two."

Use a network-partition example.

## Task G — Senior Engineer

Explain an evidence-first method for diagnosing:

~~~text
Client timeout
→ duplicate retry
→ lagging replica
→ queue backlog
~~~

## Task H — SRE

Explain how retries, queue backlog, saturation, and dependency slowdown can create a cascading failure.

## Task I — Architect

Explain how you would choose:

- retry ownership
- idempotency boundary
- consistency per operation
- replica failure domains
- queue/backpressure policy
- graceful degradation

## Task J — Observability

Explain how correlation IDs, logs, metrics, and traces help follow one request across multiple services.

## Scoring

Score 1–5 for:

- correctness
- clarity
- uncertainty/timeout reasoning
- retry/idempotency reasoning
- consistency/CAP reasoning
- reliability awareness
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

# D00-T018 — Teach-Back Assessment

## Goal

Demonstrate that you can explain how systems fail, how failure propagates, and how engineers contain, recover, validate, and learn safely.

## Task A — Beginner

Explain:

- fault
- error/degraded state
- failure
- failure mode
- impact

## Task B — Failure Types

Explain the difference between:

- transient
- permanent/non-transient
- intermittent
- partial
- slow
- stale/incorrect
- observer-dependent/gray

## Task C — Failure Domains

Explain:

~~~text
Redundancy
≠
Independence
~~~

Use a shared database or identity system as the example.

## Task D — Retry Amplification

Teach:

~~~text
Dependency Slow
→ Timeouts
→ Retries
→ More Load
→ Wider Failure
~~~

## Task E — Pressure Protection

Explain how these differ:

- timeout
- fail-fast
- backpressure
- load shedding
- graceful degradation
- isolation
- circuit breaker

## Task F — Recovery

Explain:

~~~text
Detect
→ Contain
→ Recover
→ Validate
→ Learn
~~~

## Task G — Backup vs Recovery

Explain why:

~~~text
Backup Exists
≠
Recovery Proven
~~~

Then explain restore validation.

## Task H — RTO / RPO

Explain the business meaning of:

- RTO
- RPO

## Task I — Distributed-State Preview

Explain why partition/quorum behavior is protocol-specific.

## Task J — Safe Failure Testing

Explain why failure testing needs:

- hypothesis
- scope
- observability
- stop conditions
- recovery plan
- authorization
- validation

## Task K — Architect

Explain how you would use:

- failure modes
- failure domains
- blast radius
- dependency criticality
- recovery objectives
- validation evidence

to review a production architecture.

## Scoring

Score 1–5 for:

- correctness
- clarity
- failure-mode reasoning
- propagation/blast-radius reasoning
- retry/overload reasoning
- recovery reasoning
- SRE/resilience reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

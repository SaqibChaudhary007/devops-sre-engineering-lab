# D00-T018 — Teach-Back Assessment

## Goal

Demonstrate that you can explain how systems fail, how failure propagates, how impact is contained, and how recovery is proven.

## Task A — Beginner

Explain:

- fault
- error/degraded state
- failure
- impact
- failure mode

## Task B — Failure Types

Explain the difference between:

- unavailable
- slow
- partial
- intermittent
- stale
- incorrect
- observer-dependent / gray

## Task C — Failure Domains

Teach:

~~~text
Redundancy
≠
Independence
~~~

Use shared database or shared identity as the example.

## Task D — Cascading Failure

Explain:

~~~text
Dependency Slows
→ Timeouts
→ Retries
→ Load
→ Saturation
→ Wider Failure
~~~

## Task E — Overload Protection

Explain:

- timeout
- fail-fast
- backpressure
- load shedding
- graceful degradation

and how they differ.

## Task F — Failover

Explain why failover can fail.

Include:

- detection
- capacity
- state
- routing
- shared dependencies
- validation

## Task G — Backup / Restore / RTO / RPO

Explain why:

~~~text
Backup Exists
≠
Recovery Proven
~~~

Then explain RTO vs RPO.

## Task H — State Uncertainty

Explain:

~~~text
Request Sent
→ Timeout
→ Outcome Unknown
~~~

and how idempotency/reconciliation help.

## Task I — Recovery Validation

Teach why:

~~~text
One Green Metric
≠
Recovery
~~~

Use end-to-end validation.

## Task J — Safe Failure Testing

Explain the model:

~~~text
Hypothesis
→ Controlled Scenario
→ Observe
→ Stop if Unsafe
→ Recover
→ Validate
→ Learn
~~~

Then explain why chaos engineering is not random destruction.

## Task K — Architect

Explain how you would use:

- failure domains
- blast radius
- dependency criticality
- containment
- recovery objectives
- recovery validation
- game days

to review a production architecture.

## Scoring

Score 1–5 for:

- correctness
- clarity
- failure-mode reasoning
- propagation/blast-radius reasoning
- overload/retry reasoning
- recovery reasoning
- SRE/resilience reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

# D00-T016 — Teach-Back Assessment

## Goal

Demonstrate that you can explain automation as a state-aware, bounded, observable operating system rather than simply as scripts.

## Task A — Beginner

Explain:

- automation
- trigger
- state
- action
- validation

## Task B — Reconciliation

Teach:

~~~text
Current State
↔
Desired State
→ Observe
→ Compare
→ Act
→ Observe Again
~~~

Explain why this is iterative.

## Task C — Imperative vs Declarative

Explain the difference and give one good use case for each.

## Task D — Idempotency

Explain:

- repeatability
- idempotency
- duplicate execution
- side effects

Then explain why idempotency does not guarantee success.

## Task E — Retry Safety

Teach:

~~~text
Classify Failure
→ Check Retry Safety
→ Bound Attempts
→ Backoff
→ Jitter
→ Timeout Budget
→ Stop / Escalate
~~~

## Task F — Partial Failure

Explain:

- partial failure
- rollback
- roll-forward
- compensation

Then explain why rollback is not always possible.

## Task G — Guardrails

Explain how to bound:

- environment
- target count
- rate
- concurrency
- permissions
- retries
- time window

## Task H — Human Approval

Explain why human-in-the-loop is a valid design boundary for high-impact, irreversible, ambiguous, or security-sensitive actions.

## Task I — Automation Identity and Observability

Explain why automation requires:

- dedicated identity
- least privilege
- secret controls
- logs/audit
- validation evidence

## Task J — AI-Assisted Automation

Explain how autonomy should decrease as impact, irreversibility, and uncertainty increase.

## Scoring

Score 1–5 for:

- correctness
- clarity
- state/reconciliation reasoning
- idempotency/retry reasoning
- failure/recovery reasoning
- guardrail/identity reasoning
- SRE/platform reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

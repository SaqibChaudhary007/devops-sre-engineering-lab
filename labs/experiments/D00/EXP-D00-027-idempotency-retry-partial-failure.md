---
id: EXP-D00-027
domain: D00
topics:
  - D00-T016
level: L2-L3
type: experiment
status: draft
estimated_time: 60-80m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-027 — Idempotency, Retry Safety, and Partial Failure

## Objective

Practice reasoning about repeated execution, retry policy, timeouts, backoff, jitter, partial failure, rollback, roll-forward, and compensation.

## Safety

This is a design exercise only.

Do not invoke payment systems, external APIs, production automation, or destructive workflows.

## Scenario

Compare these operations:

~~~text
A. Ensure directory exists
B. Ensure service has 3 replicas
C. Send deployment notification
D. Charge customer
E. Append audit record
F. Create cloud resource
G. Update DNS target
H. Rotate credential
~~~

## 1. Idempotency Classification

Classify each as:

~~~text
Naturally Idempotent
Can Be Made Idempotent
Non-Idempotent / Side-Effect Sensitive
Needs More Context
~~~

Explain why repeatability and idempotency are not the same thing.

## 2. Duplicate Execution

For each operation, imagine:

- worker restarts after timeout
- event is delivered twice
- human resubmits request
- scheduler overlaps
- network response is lost

Explain the possible duplicate effect.

## 3. Retry Eligibility

For each failure, decide:

~~~text
Retry
Retry with Conditions
Do Not Retry Automatically
Escalate / Investigate
~~~

Failures:

- transient network timeout
- authentication denied
- dependency rate-limited
- invalid input
- target already in desired state
- dependency overloaded
- unknown server error
- operation outcome unknown after timeout

## 4. Retry Policy

Design a conceptual retry policy:

~~~text
Classify Failure
→ Check Idempotency / Side Effects
→ Bound Attempts
→ Backoff
→ Jitter Where Useful
→ Respect Timeout Budget
→ Stop / Escalate
~~~

Explain why retry is a policy rather than an instinct.

## 5. Backoff and Jitter

Assume 1,000 workers fail at once.

Compare:

~~~text
Immediate Retry
Fixed Delay
Increasing Backoff
Backoff + Jitter
~~~

Explain how synchronized retries can amplify an outage.

## 6. Timeout Budget

Design a total operation budget:

~~~text
Overall Time Budget
→ Attempt Timeout
→ Retry Delay
→ Remaining Attempts
~~~

Explain why per-attempt timeout without an overall budget can create very slow failures.

## 7. Partial Failure

Use this workflow:

~~~text
Provision Resource
→ Configure
→ Register
→ Deploy
→ Validate
~~~

Assume failure occurs after Configure.

List:

- what succeeded
- what failed
- what current state exists
- what evidence is needed
- what next action is safe

## 8. Rollback vs Roll-Forward

Compare:

~~~text
Rollback
Roll-Forward
Manual Reconciliation
~~~

for:

- reversible configuration change
- incompatible data migration
- external notification already sent
- credential rotation partially completed

Explain why rollback is not universally safe.

## 9. Compensation

For a non-reversible side effect, design a conceptual compensating action.

Example:

~~~text
Reserve Capacity
→ Later Step Fails
→ Release Reservation
~~~

Explain why compensation is not identical to time travel or true rollback.

## 10. Unknown Outcome

A request times out after sending a side-effecting operation.

You do not know whether the dependency completed it.

Design a safe reasoning path:

~~~text
Do Not Blindly Repeat
→ Query / Reconcile State
→ Use Idempotency Key or Unique Operation Identity Where Available
→ Decide Next Action
~~~

Keep this conceptual.

## 11. Senior Engineer Connection

Use:

~~~text
Operation
→ Side Effect
→ Duplicate Risk
→ Retry Safety
→ Timeout
→ Partial Failure
→ Recovery
~~~

## 12. SRE Connection

Connect retry design to:

- dependency overload
- cascading failure
- MTTR
- alert noise
- recovery validation

## 13. Architect Connection

Decide:

- which operations need idempotency keys
- where retries are allowed
- where compensation is needed
- where workflow state should live
- what global retry budget is acceptable

## Validation Checklist

- [ ] Classified idempotent and side-effect-sensitive operations
- [ ] Analyzed duplicate execution
- [ ] Classified retry eligibility
- [ ] Designed bounded retry policy
- [ ] Explained backoff and jitter
- [ ] Designed timeout-budget reasoning
- [ ] Modeled partial failure
- [ ] Compared rollback and roll-forward
- [ ] Designed compensation
- [ ] Handled unknown outcome safely

## Teach-Back

Explain:

> "Safe automation assumes duplicate execution, partial failure, and uncertain outcomes can happen, so idempotency, bounded retries, state checks, and explicit recovery paths must be designed in."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

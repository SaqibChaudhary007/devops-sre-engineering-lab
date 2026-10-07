---
id: EXP-D00-028
domain: D00
topics:
  - D00-T016
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

# EXP-D00-028 — Reconciliation, Guardrails, Human Approval, and Automation Readiness

## Objective

Practice control-loop, reconciliation, concurrency, blast-radius, observability, identity, approval-boundary, and production-readiness reasoning.

## Safety

This is a local architecture exercise.

Do not connect automation to production systems, run auto-remediation, change credentials, or create high-impact autonomous actions.

## Scenario

A platform team proposes automation for:

~~~text
- desired replica reconciliation
- configuration drift correction
- certificate renewal
- failed-job retry
- service recovery action
- deployment promotion
- account deactivation
~~~

The initial proposal gives the automation broad administrator access and no stop conditions.

## 1. Imperative vs Declarative

Classify each task as better suited to:

~~~text
Imperative
Declarative / Reconciled
Either / Depends
~~~

Explain the trade-off.

## 2. Reconciliation Loop

Design:

~~~text
Observe Current State
→ Compare with Desired State
→ Decide
→ Act
→ Measure
→ Repeat
~~~

For replica count or configuration drift.

Explain why reconciliation is iterative rather than one-time.

## 3. Stale State

Assume observation is delayed.

Ask:

- what could have changed since observation?
- can the action conflict with a newer state?
- should the automation re-read before write?
- what validation is required?

## 4. Concurrency and Duplicate Work

Assume two automation workers act on the same target.

Identify risks:

- duplicate action
- conflicting update
- stale write
- resource overload
- inconsistent workflow state

Describe conceptual controls such as:

- ownership/lease
- version check
- serialized work
- idempotent operation
- queue partitioning

Do not implement distributed locking.

## 5. Blast-Radius Guardrails

Design bounds for:

- environment
- target count
- batch size
- action rate
- retry count
- permission scope
- allowed time window
- maximum concurrent changes

Explain why small batches and pause controls matter.

## 6. Human Approval Boundary

Classify actions as:

~~~text
Fully Automated
Automated with Approval
Human-Led with Automation Assistance
~~~

Consider:

- routine certificate renewal
- production database schema migration
- known low-risk remediation
- unknown security event
- high-impact account deletion
- deployment to production

Explain your criteria using impact, reversibility, confidence, and business context.

## 7. Automation Identity

Design a dedicated automation identity.

Review:

- resource scope
- environment scope
- allowed actions
- duration
- secret/credential method
- audit evidence

Explain why shared human credentials are weak automation design.

## 8. Observability

Define what every run should record:

~~~text
Trigger
Actor
Target
Input
Preconditions
Action
Start / End
Retry Count
Validation
Result
Failure Reason
~~~

Explain why opaque automation is difficult to trust.

## 9. Stop Conditions

For auto-remediation, define:

- max attempts
- no-improvement condition
- unexpected state condition
- dependency unhealthy condition
- blast-radius threshold
- mandatory human escalation

## 10. Self-Healing Review

Review this weak rule:

~~~text
If health check fails
→ restart forever
~~~

Replace it with:

~~~text
Detect
→ Confirm Condition
→ Check Preconditions
→ One Bounded Action
→ Recheck
→ Stop or Escalate
~~~

Explain why repeated restart loops can hide deeper failure.

## 11. Security Review

Check:

- least privilege
- secret exposure
- environment isolation
- auditability
- approval for high-impact actions

Explain how a bug plus broad permissions can become a security incident.

## 12. Production-Readiness Review

Score each:

~~~text
Ready
Partially Ready
Not Ready
~~~

for:

- intent defined
- trigger defined
- authoritative state identified
- preconditions defined
- idempotency understood
- retry policy bounded
- timeout budget defined
- concurrency considered
- guardrails defined
- dedicated identity scoped
- secrets controlled
- observability ready
- stop/escalation defined
- human approval boundary defined
- recovery/compensation understood
- owner defined

## 13. AI-Assisted Automation Boundary

For an AI-generated recommendation, classify:

~~~text
Recommend Only
Draft Action for Review
Execute Low-Risk Reversible Action
Require Explicit Human Approval
~~~

Explain why autonomy should decrease as impact, irreversibility, and uncertainty increase.

## 14. Senior Engineer Connection

Use:

~~~text
Desired State
→ Observation
→ Decision
→ Bounded Action
→ Validation
→ Feedback
→ Escalation
~~~

## 15. SRE / Platform Connection

Connect:

- reconciliation
- toil reduction
- bounded remediation
- policy
- auditability
- operational feedback

## 16. Architect Connection

Decide:

- where state should live
- what the automation authority boundary is
- which controls are centralized
- which approvals are mandatory
- what the maximum safe blast radius is

## Validation Checklist

- [ ] Compared imperative and declarative models
- [ ] Designed a reconciliation loop
- [ ] Reasoned about stale state
- [ ] Reviewed concurrency and duplicates
- [ ] Defined blast-radius guardrails
- [ ] Defined human approval boundaries
- [ ] Designed dedicated automation identity
- [ ] Defined observability/audit evidence
- [ ] Defined stop conditions
- [ ] Improved self-healing logic
- [ ] Reviewed security boundaries
- [ ] Performed production-readiness review
- [ ] Defined an AI-assisted autonomy boundary

## Teach-Back

Explain:

> "Production automation should reconcile state through bounded, observable actions with explicit identity, guardrails, stop conditions, and human approval where impact or uncertainty is high."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

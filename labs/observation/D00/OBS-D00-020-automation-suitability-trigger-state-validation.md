---
id: OBS-D00-020
domain: D00
topics:
  - D00-T016
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# OBS-D00-020 — Automation Suitability, Trigger, State, and Validation

## Objective

Decide which operational tasks are good automation candidates and model them using intent, trigger, preconditions, state, action, validation, and escalation.

## Why This Matters

Automation should not begin with "what can we script?"

It should begin with:

> What work is understood well enough, bounded well enough, and valuable enough to automate safely?

## Safety

This is a local reasoning exercise only.

Do not execute production changes, real remediations, destructive commands, credential changes, or autonomous actions.

## Scenario

A team performs these tasks:

- produce a daily service-health report
- restart a service when one health check fails
- rotate a credential on a planned schedule
- approve a high-impact production database change
- remove old temporary files
- investigate an unknown latency incident
- reconcile desired replica count with actual replica count
- re-run a failed payment
- notify a team when a deployment completes
- disable an account after an approved offboarding event

## 1. Classify Automation Suitability

Classify each task as:

~~~text
Strong Candidate
Candidate with Guardrails
Human Judgment Required
Needs More Understanding
~~~

Use these questions:

- is the task repetitive?
- is the state observable?
- is the action bounded?
- is the outcome measurable?
- is the failure mode understood?
- is the action reversible?
- could duplicate execution create harm?
- is human judgment essential?

## 2. Define Intent

For three automation candidates, rewrite vague goals into explicit intent.

Weak:

~~~text
Fix unhealthy services automatically.
~~~

Stronger:

~~~text
When a known health condition persists for the defined window,
perform one bounded recovery action,
then validate user-facing health,
otherwise stop and escalate.
~~~

## 3. Define Trigger

For each selected candidate, choose:

- human request
- schedule
- event
- threshold
- queue message
- reconciliation loop

Explain why a trigger only starts evaluation; it does not prove an action is safe.

## 4. Define Preconditions

Write preconditions such as:

- correct target
- expected version
- approval present
- dependency available
- maintenance window active
- capacity available
- no conflicting workflow active

## 5. Model State

For one candidate, define:

~~~text
Current State
Desired State
Observed Evidence
Decision
~~~

Explain what could happen if the state is stale or incomplete.

## 6. Define Action

Describe the smallest bounded action that could satisfy the intent.

Prefer:

~~~text
Small Scope
→ One Action
→ Validate
~~~

over:

~~~text
Broad Scope
→ Many Changes
→ Hope
~~~

## 7. Define Postconditions

Specify what must be true after the action.

Examples:

- target state reached
- service healthy
- user journey works
- credential rotated
- audit event recorded
- no critical error introduced

## 8. Validate Outcome

Distinguish:

~~~text
Process Completed
vs
Desired Outcome Achieved
~~~

Explain why exit code 0 is not enough.

## 9. Define Stop / Escalation

For each candidate, define:

- retry limit
- stop condition
- human escalation point
- rollback/compensation need
- audit evidence

## 10. Automation Economics

For each candidate, compare:

~~~text
Manual Cost
Automation Build Cost
Maintenance Cost
Failure Risk
Long-Term Value
~~~

Explain why low-frequency, high-judgment work may remain manual.

## 11. Senior Engineer Connection

Use:

~~~text
Intent
→ Trigger
→ Preconditions
→ State
→ Action
→ Postcondition
→ Validation
→ Escalation
~~~

## 12. SRE / Platform Connection

Connect the exercise to:

- toil reduction
- bounded remediation
- operational feedback
- safe defaults
- blast-radius control

## 13. Architect Connection

Ask:

- what classes of work should be automated?
- which require approval?
- what state must be authoritative?
- which outcomes need end-to-end validation?
- what is the maximum safe scope?

## Validation Checklist

- [ ] Classified tasks by automation suitability
- [ ] Defined explicit intent
- [ ] Chosen appropriate triggers
- [ ] Defined preconditions
- [ ] Modeled current vs desired state
- [ ] Chosen bounded actions
- [ ] Defined postconditions
- [ ] Distinguished process success from outcome success
- [ ] Defined stop/escalation behavior
- [ ] Considered automation economics

## Teach-Back

Explain:

> "A good automation candidate is understood, measurable, bounded, valuable, and safe enough that its trigger, state, action, validation, and failure path can be designed explicitly."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

# D00-T016 — Applied Automation Scenario

## Scenario

A platform team wants to automate these operational tasks:

~~~text
- reconcile application replicas
- restart unhealthy workloads
- rotate credentials
- promote deployments
- retry failed jobs
- deactivate user accounts
- clean temporary files
~~~

Current proposal:

~~~text
- one administrator credential for all automation
- retry every failed action forever
- no timeout budget
- no distinction between current and desired state
- no duplicate-execution handling
- no stop condition for self-healing
- no human approval for high-impact changes
- success = process exit code 0
- no audit log
- automation can change every environment at once
~~~

## Task 1 — Automation Suitability

Classify each task as:

~~~text
Strong Candidate
Candidate with Guardrails
Human Approval Required
Needs More Understanding
~~~

Explain why.

## Task 2 — Define Intent

Choose three tasks and define explicit intent.

Use:

~~~text
Trigger
→ Preconditions
→ State
→ Action
→ Postcondition
→ Validation
→ Escalation
~~~

## Task 3 — Current vs Desired State

For replica reconciliation, define:

- current state
- desired state
- authoritative source
- stale-state risk
- validation

## Task 4 — Imperative vs Declarative

Classify the tasks by whether they fit:

~~~text
Imperative
Declarative / Reconciled
Either / Depends
~~~

Explain your reasoning.

## Task 5 — Preconditions and Postconditions

For credential rotation and deployment promotion, define preconditions and postconditions.

Explain why process completion is not enough.

## Task 6 — Idempotency Review

Classify these operations:

- ensure replica count
- send notification
- deactivate account
- create resource
- append audit record
- rotate credential

Use:

~~~text
Naturally Idempotent
Can Be Made Idempotent
Side-Effect Sensitive
Needs More Context
~~~

## Task 7 — Duplicate Execution

Explain what can happen if:

- event delivered twice
- scheduler overlaps
- worker restarts
- network response is lost
- human resubmits

Design safeguards.

## Task 8 — Retry Policy

Replace:

~~~text
Retry Forever
~~~

with:

~~~text
Classify Failure
→ Check Retry Safety
→ Bound Attempts
→ Backoff
→ Jitter
→ Respect Timeout Budget
→ Stop / Escalate
~~~

Apply it to:

- transient timeout
- authorization denied
- invalid input
- dependency overload
- unknown outcome after timeout

## Task 9 — Partial Failure

Use:

~~~text
Provision
→ Configure
→ Register
→ Deploy
→ Validate
~~~

Assume failure after Configure.

Explain:

- current state
- what evidence is needed
- whether rollback is safe
- whether roll-forward is better
- whether compensation is needed

## Task 10 — Human Approval Boundary

Classify:

- certificate renewal
- production database migration
- known low-risk remediation
- unknown security event
- production deployment
- destructive account deletion

Use:

~~~text
Fully Automated
Automated with Approval
Human-Led with Automation Assistance
~~~

## Task 11 — Blast-Radius Guardrails

Design bounds for:

- environment
- target count
- batch size
- rate
- concurrency
- permission scope
- retry count
- time window

## Task 12 — Automation Identity

Replace the shared admin credential with a dedicated automation identity.

Define:

- scope
- permissions
- environment boundary
- credential model
- audit requirements

## Task 13 — Observability and Auditability

Define evidence for every run:

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

Explain how this supports troubleshooting and security review.

## Task 14 — Self-Healing

Replace:

~~~text
If health check fails
→ restart forever
~~~

with:

~~~text
Detect
→ Confirm
→ Check Preconditions
→ One Bounded Action
→ Recheck
→ Stop / Escalate
~~~

Explain why.

## Task 15 — Automation Economics

Choose one low-frequency task and one high-frequency task.

Compare:

- manual cost
- automation build cost
- maintenance
- failure risk
- long-term value

## Task 16 — AI-Assisted Automation

For an AI-generated recommendation, decide when to:

~~~text
Recommend Only
Draft Action for Review
Execute Low-Risk Reversible Action
Require Explicit Human Approval
~~~

Use impact, reversibility, and uncertainty.

## Task 17 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Intent
→ State
→ Idempotency
→ Retry Safety
→ Validation
→ Recovery
~~~

### SRE / Platform Engineer

Connect:

- toil
- bounded remediation
- observability
- stop conditions
- human escalation
- blast radius

### Architect

Redesign:

- authority boundaries
- state ownership
- concurrency controls
- approval points
- identity
- global guardrails
- maximum safe blast radius

## Success Standard

A strong answer should explicitly reject:

- automation = script everything
- exit code 0 = intended outcome achieved
- every failure should retry
- idempotency = guaranteed success
- rollback is always safe
- duplicate execution can be ignored
- self-healing = restart forever
- human approval = automation failure
- admin access = convenient and acceptable

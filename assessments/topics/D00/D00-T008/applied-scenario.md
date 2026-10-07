# D00-T008 — Applied IaC Change Scenario

## Scenario

A payments platform uses IaC for production infrastructure.

Current design:

~~~text
Shared Network State
        ↓
Payments Application State
        ↓
Managed Database
        ↓
Monitoring / Alerts
~~~

A proposed production change shows:

~~~text
Plan Summary

+ Create
  - 2 application instances
  - 1 monitoring rule

~ Update
  - autoscaling maximum: 6 → 12
  - health-check timeout: 5s → 2s
  - database backup retention: 14 days → 3 days

-/+ Replace
  - primary application load balancer
    reason: immutable property changed

- Delete
  - legacy storage bucket
    deletion protection: disabled

~ Update
  - SSH source:
    10.0.0.0/8 → 0.0.0.0/0

~ Update
  - instance size:
    medium → xlarge
    count: 4
~~~

Additional facts:

~~~text
- application code is healthy
- a manual emergency firewall change was made yesterday
- shared remote state is used
- backend locking capability has not been documented
- one manually created monitoring resource is not in IaC
- the database is business-critical
- the team assumes Git revert is enough for rollback
~~~

## Task 1 — Desired vs Actual State

Identify:

- intended state
- observed actual state
- known drift
- unmanaged resources

Explain why the repository alone is insufficient during investigation.

## Task 2 — Drift

Classify the emergency firewall change and manual monitoring resource.

For each, decide:

- reconcile code to reality
- reconcile reality to code
- import/adopt
- investigate before action

Explain your reasoning.

## Task 3 — Plan Classification

For every plan item, classify:

- create
- update
- replace
- delete

Then rate:

- availability risk
- security risk
- data risk
- cost risk

## Task 4 — Replacement Risk

The load balancer must be replaced.

Explain:

- possible identity/address changes
- dependency risk
- traffic-shift considerations
- downtime risk
- recovery strategy

Do not assume replacement is equivalent to update.

## Task 5 — Delete Risk

The storage bucket is marked for deletion.

List evidence required before approval.

Include:

- data ownership
- retention requirements
- consumers
- backup/replication
- recoverability

## Task 6 — State / Locking

The team uses remote state but cannot confirm locking support.

Explain:

- what risk concurrent apply creates
- what state locking protects
- what state locking does not protect
- why backend capabilities must be verified

## Task 7 — Scaling Dependency

Autoscaling maximum changes from 6 to 12.

Analyze:

- database connection capacity
- downstream dependencies
- quotas
- cost
- statefulness
- failure domains

Explain why scaling the app tier may worsen another bottleneck.

## Task 8 — Security

Review:

~~~text
SSH:
10.0.0.0/8
→ 0.0.0.0/0
~~~

Explain:

- exposure increase
- evidence required
- safer alternatives
- whether policy should block the change

## Task 9 — Backup / Recovery

Backup retention changes from 14 days to 3 days.

Explain:

- recovery impact
- compliance/business requirement implications
- who should approve the requirement change

## Task 10 — Preview Limitations

Explain why a clean plan cannot guarantee successful apply.

Include at least five of:

- authorization
- quota
- API availability
- provider capacity
- dependency behavior
- runtime health
- concurrent change
- external system failure

## Task 11 — Rollback vs Roll Forward

Evaluate the statement:

> "If this fails, we will revert the Git commit."

Explain why that may be insufficient.

For the riskiest plan items, choose likely recovery strategies from:

~~~text
Rollback
Roll Forward
Failover
Restore
Manual Investigation
~~~

## Task 12 — Senior Engineer Response

Write the review sequence using:

~~~text
Intent
→ Actual State
→ Drift
→ Plan
→ Replacement/Delete Risk
→ Dependencies
→ Security/Data/Cost
→ Blast Radius
→ Recovery
→ Approval
~~~

## Task 13 — SRE View

Connect this infrastructure change to:

- SLOs
- incident/change markers
- blast radius
- alerts
- failover
- restore
- emergency reconciliation

## Task 14 — Architect View

Design a safer IaC operating model including:

- state boundaries
- ownership
- backend capabilities
- apply permissions
- policy checks
- change review
- environment separation
- observability
- recovery

## Success Standard

A strong answer treats IaC as production change management, not file management.

It should identify:

- drift
- replacement and deletion risk
- state/locking limitations
- scaling dependencies
- security exposure
- backup implications
- rollback limitations
- policy opportunities

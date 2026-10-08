---
id: EXP-D00-032
domain: D00
topics:
  - D00-T018
level: L2-L3
type: experiment
status: draft
estimated_time: 60-90m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# EXP-D00-032 — Failover, Recovery Validation, Backup/Restore, and Safe Failure Testing

## Objective

Practice evaluating failover, recovery, backup/restore, RTO/RPO, state uncertainty, and safe failure-testing design without performing destructive actions.

## Safety

This exercise is tabletop only.

Do not trigger failover, restore production data, inject faults, change quorum, partition networks, or perform destructive chaos experiments.

## Scenario

A business-critical service has:

~~~text
Primary Region
Secondary Region
Managed Database
Object Storage Backups
DNS-Based Traffic Routing
Shared Identity Provider
Shared Deployment Pipeline
~~~

Business expectations:

~~~text
"Recovery should be fast."
"Recent data loss should be minimal."
~~~

These statements are not yet formal recovery objectives.

## 1. Define RTO and RPO

Translate the business expectations into questions:

~~~text
RTO:
How long can recovery take?

RPO:
How much recent data loss is acceptable?
~~~

Explain why architecture cannot choose these targets without business input.

## 2. Failover Assumptions

List what must be true for failover to work:

- failure is detected correctly
- secondary is healthy
- secondary has enough capacity
- data/state is acceptable
- routing can move
- credentials/configuration work
- shared dependencies are healthy
- operators know what to do

## 3. Failover Failure Modes

Consider:

- false detection
- stale secondary
- under-capacity secondary
- shared identity outage
- shared DNS issue
- deployment drift
- routing delay

Explain how failover can create a second incident.

## 4. Redundancy vs Independence

Review whether primary and secondary truly differ across:

- region
- database dependency
- identity
- deployment path
- artifact source
- DNS/control plane
- operator/team

Mark each as:

~~~text
Independent Enough
Shared
Unknown
Needs Evidence
~~~

## 5. Backup vs Recovery

Use:

~~~text
Backup Exists
→ Restore Attempt
→ Integrity Check
→ Application Starts
→ User Journey Works
→ Recovery Objective Met
~~~

Explain why a successful backup job does not prove recoverability.

## 6. Restore Validation

Design a safe non-production restore-validation checklist:

- backup can be located
- restore completes
- expected data exists
- data is readable
- application can connect
- schema/version is compatible
- representative user journey works
- recovery timing is measured
- evidence is recorded

## 7. State Uncertainty

Scenario:

~~~text
Payment request sent
→ caller times out
→ outcome unknown
~~~

Decide what information would help reconcile state:

- operation ID
- transaction status lookup
- idempotency key
- audit event
- business record

Explain why immediate blind retry can be unsafe.

## 8. Partition / Quorum Preview

Tabletop only:

~~~text
Cluster members lose communication
→ majority side remains authoritative in a majority-based design
→ minority side cannot safely act as sole authority
~~~

Explain why exact behavior is protocol-specific.

## 9. Recovery Validation

After hypothetical failover, validate:

- user-facing SLO
- error rate
- latency
- queue state
- data correctness
- retry volume
- dependency health
- security/identity state
- capacity headroom

## 10. Failback Preview

Ask:

- when is the original site truly healthy?
- has state converged?
- is capacity stable?
- can traffic return gradually?
- what would trigger rollback of failback?

## 11. Pre-Mortem

Imagine the DR event failed badly.

List likely reasons:

- secondary was stale
- credentials were wrong
- backup could not restore
- routing was slow
- runbook was outdated
- shared identity failed
- team ownership was unclear

Turn each into a verification item.

## 12. Design a Safe Failure-Test Hypothesis

Example structure:

~~~text
Hypothesis:
If the primary application endpoint becomes unavailable in a controlled non-production environment,
traffic should move to the secondary path within the expected test window without data loss beyond the approved test objective.
~~~

Define:

- environment
- scope
- expected steady state
- controlled disturbance
- observability
- stop conditions
- recovery plan
- validation
- owner / authorization

## 13. Game-Day Design

Create a tabletop game day around:

~~~text
Primary Region Unavailable
~~~

Include:

- incident roles
- detection
- decision points
- communication
- failover criteria
- validation
- failback criteria
- lessons learned

## 14. Chaos-Engineering Boundary

Explain why:

~~~text
Randomly breaking production
≠
Chaos engineering
~~~

and why hypothesis, observability, blast-radius control, stop conditions, and authorization are mandatory.

## 15. Senior Engineer Connection

Use:

~~~text
Failure Assumption
→ Recovery Objective
→ Failover Preconditions
→ Recovery Action
→ Validation
→ Learning
~~~

## 16. SRE Connection

Connect:

- RTO / RPO
- incident response
- SLO recovery
- restore testing
- game days
- operational readiness

## 17. Architect Connection

Decide:

- what must be independent
- what state must survive
- what recovery objectives drive topology
- what common-mode dependencies remain
- what tests prove recoverability
- where manual approval is required

## Validation Checklist

- [ ] Explained RTO vs RPO
- [ ] Listed failover preconditions
- [ ] Identified failover failure modes
- [ ] Reviewed redundancy vs independence
- [ ] Distinguished backup from recovery
- [ ] Designed restore validation
- [ ] Analyzed state uncertainty
- [ ] Kept partition/quorum reasoning protocol-specific
- [ ] Defined recovery validation
- [ ] Reviewed failback risks
- [ ] Completed a pre-mortem
- [ ] Designed a safe bounded failure-test hypothesis
- [ ] Designed a tabletop game day
- [ ] Explained the chaos-engineering safety boundary

## Teach-Back

Explain:

> "A recovery strategy is only trustworthy when its assumptions, objectives, failover path, restore path, validation criteria, and failure-testing evidence are explicit."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

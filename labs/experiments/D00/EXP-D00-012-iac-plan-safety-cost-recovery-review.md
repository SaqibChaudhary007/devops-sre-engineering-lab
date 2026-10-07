---
id: EXP-D00-012
domain: D00
topics:
  - D00-T008
level: L2-L3
type: experiment
status: draft
estimated_time: 55-75m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-012 — Review a Hypothetical IaC Plan for Safety, Cost, and Recovery

## Objective

Practice reading infrastructure change intent like a production engineer.

The goal is not to approve syntax.

The goal is to reason about:

- create/update/replace/delete actions
- blast radius
- state
- security
- cost
- dependencies
- recovery

## Safety

This is a paper/local simulation.

Do not execute any infrastructure command.

## Scenario

A hypothetical production plan reports:

~~~text
Plan Summary

+ Create
  - 2 application instances
  - 1 monitoring rule

~ Update
  - load balancer health-check timeout: 5s → 2s
  - autoscaling maximum: 6 → 12

-/+ Replace
  - primary application load balancer
    reason: immutable property changed

- Delete
  - old storage bucket
    lifecycle: no retention protection

~ Update
  - database backup retention: 14 days → 3 days

~ Update
  - network rule:
    source 10.0.0.0/8 → 0.0.0.0/0
    port 22

~ Update
  - instance type:
    medium → xlarge
    count: 4 instances
~~~

Assume the plan passed syntax validation.

## 1. Classify the Plan

Build:

| Change | Action | Availability Risk | Security Risk | Data Risk | Cost Risk | Review Decision |
|---|---|---|---|---|---|---|
| Add 2 app instances | | | | | | |
| Health timeout 5s → 2s | | | | | | |
| Autoscaling max 6 → 12 | | | | | | |
| Replace load balancer | | | | | | |
| Delete bucket | | | | | | |
| Backup retention 14 → 3 | | | | | | |
| SSH 0.0.0.0/0 | | | | | | |
| medium → xlarge | | | | | | |

Use decisions:

~~~text
Approve
Approve with Conditions
Block
Need More Evidence
~~~

## 2. Replacement Reasoning

The load balancer is marked for replacement.

Ask:

- will its address or identity change?
- what depends on it?
- can traffic be shifted safely?
- is downtime possible?
- is DNS involved?
- is there a rollback/recovery path?
- should the replacement be staged?

Explain why replacement deserves more review than a normal in-place update.

## 3. Delete Reasoning

The storage bucket is marked for deletion.

Before approval, ask:

- is there data?
- is the data replicated?
- is retention required?
- is deletion recoverable?
- what consumes the bucket?
- is deletion protection available?
- is the bucket actually obsolete?

Explain why:

> "The plan says delete"

is not enough evidence to delete a stateful resource.

## 4. Security Review

Review:

~~~text
SSH source
10.0.0.0/8
→ 0.0.0.0/0
~~~

Explain:

- why this increases exposure
- what evidence would justify it
- what safer alternatives may exist
- whether the change should be blocked by policy

## 5. Reliability Review

Review:

~~~text
health-check timeout
5s → 2s
~~~

Discuss:

- faster failure detection
- false failure risk
- dependency latency
- healthy instance eviction
- cascading effects

Do not assume lower timeout is automatically better.

## 6. Scaling and Dependency Review

Review:

~~~text
autoscaling max
6 → 12
~~~

Ask:

- can the database handle the connection increase?
- are quotas sufficient?
- is downstream capacity sufficient?
- what happens to cost?
- does the application hold local state?

Explain why scaling one tier can worsen another bottleneck.

## 7. Cost Review

Estimate relative cost change qualitatively.

Changes include:

- 2 additional instances
- 4 instances changing medium → xlarge
- higher autoscaling maximum

Classify:

~~~text
Low
Medium
High
Unknown
~~~

Then list the missing information needed for a real estimate.

## 8. Backup / Recovery Review

Review:

~~~text
database backup retention
14 days → 3 days
~~~

Ask:

- what business/recovery requirement exists?
- does compliance require longer retention?
- what failure window becomes unrecoverable?
- who approved the requirement change?

Explain why backup retention is an architecture/recovery decision, not just a cost parameter.

## 9. Plan Is Not a Guarantee

Even if every change is approved, list reasons apply could still fail:

- API failure
- permission issue
- quota
- provider capacity
- dependency failure
- timeout
- race/concurrency
- runtime behavior after success

## 10. Rollback vs Roll Forward

For each risky change, decide whether likely recovery is:

~~~text
Rollback
Roll Forward
Failover
Restore
Manual Investigation
~~~

Explain why reverting source control alone may not be enough.

## 11. Senior Engineer Connection

Use this review sequence:

~~~text
Intent
→ Plan Actions
→ Replacement / Delete Risk
→ Dependencies
→ Security
→ Data
→ Cost
→ Blast Radius
→ Recovery
→ Approval
~~~

## 12. SRE Connection

Connect the plan to:

- SLO risk
- deployment/change markers
- alerts
- rollback/failover
- backup/restore
- incident blast radius

## 13. Architect Connection

Define which plan conditions should become automated policy.

Examples:

- public SSH
- missing encryption
- deletion without protection
- unapproved regions
- excessive instance size
- missing ownership tags

Then identify which decisions still require human judgment.

## Validation Checklist

- [ ] Classified every plan action
- [ ] Reviewed replacement risk
- [ ] Reviewed delete/data risk
- [ ] Identified security exposure
- [ ] Reviewed scaling dependencies
- [ ] Reviewed cost impact
- [ ] Reviewed backup/recovery impact
- [ ] Explained why preview does not guarantee success
- [ ] Selected recovery strategies
- [ ] Proposed policy-as-code candidates

## Teach-Back

Explain:

> "A valid IaC plan is a change proposal, not proof that the change is safe."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

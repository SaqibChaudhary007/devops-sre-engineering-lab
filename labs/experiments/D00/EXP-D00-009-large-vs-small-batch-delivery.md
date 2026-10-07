---
id: EXP-D00-009
domain: D00
topics:
  - D00-T007
level: L2-L3
type: experiment
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Calculator or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-009 — Compare Large-Batch vs Small-Batch Delivery

## Objective

Compare two delivery models and reason about lead time, feedback speed, rollback scope, and failure isolation.

## Safety

This is a local simulation only. No real deployment is performed.

## Scenario

A team has 20 independent changes ready over a two-week period.

### Model A — Large Batch

~~~text
20 changes
→ one release
→ one production deployment
~~~

### Model B — Small Batches

~~~text
20 changes
→ 10 releases
→ 2 changes per deployment
~~~

Assumptions:

~~~text
Validation time per deployment: 20 minutes
Production verification: 10 minutes
Rollback decision time: 10 minutes
One defect exists among the 20 changes
~~~

These numbers are hypothetical and only support reasoning.

## 1. Failure Isolation

For Model A, if production fails after deployment, how many changes are candidates, how large is the investigation set, and how large is the rollback scope?

For Model B, how many changes are candidates in the failing deployment, and what changed about diagnosis complexity?

## 2. Feedback Timing

Assume the defect is introduced on Day 2.

Model A ships on Day 10. Model B ships small batches every day.

Ask:

- how long can the defect remain undiscovered in each model?
- which model returns production feedback sooner?
- why does earlier feedback matter?

## 3. Delivery Overhead

Calculate validation overhead.

### Model A

~~~text
1 deployment × 30 minutes
= 30 minutes
~~~

### Model B

~~~text
10 deployments × 30 minutes
= 300 minutes
~~~

Now answer:

> Does higher deployment overhead automatically mean Model A is better?

Discuss automation, risk per release, feedback speed, rollback scope, debugging, queueing, and release confidence.

## 4. Change Failure Thought Experiment

Assume:

- Model A has 1 failed deployment out of 1
- Model B has 1 failed deployment out of 10

Calculate:

~~~text
Change Fail Rate
=
Failed Deployments
/
Total Deployments
× 100
~~~

Then explain why this metric alone does not capture the full business impact.

## 5. Recovery Thought Experiment

Assume:

### Model A

~~~text
45 minutes to identify the failing change
30 minutes to coordinate rollback
15 minutes to restore
~~~

### Model B

~~~text
10 minutes to identify the failing batch
10 minutes to roll back
10 minutes to restore
~~~

Compare failed deployment recovery time.

## 6. Deployment Rework Rate

Suppose one corrective deployment is needed after the failure.

Explain how deployment rework rate adds information beyond change fail rate.

## 7. Queue Effect

Now add a weekly change window.

What happens to:

- queue size
- batch size
- lead time
- context loss
- release risk

## 8. Senior Engineer Connection

Explain why:

> "We should deploy less often because deployments are risky"

can become a self-reinforcing problem if the process creates larger and harder-to-understand batches.

## 9. SRE Connection

Connect batch size to:

- blast radius
- change fail rate
- failed deployment recovery time
- alert correlation
- rollback confidence

## 10. Architect Connection

Do not conclude that every organization should continuously deploy every change.

Discuss constraints such as:

- regulation
- safety
- data migrations
- testing maturity
- deployment architecture
- customer expectations

## Validation Checklist

- [ ] Compared large and small batch failure isolation
- [ ] Compared feedback timing
- [ ] Calculated simple change fail rates
- [ ] Compared failed deployment recovery time
- [ ] Explained deployment rework rate
- [ ] Explained queue effects
- [ ] Discussed when smaller batches still require strong controls

## Teach-Back

Explain:

> "Smaller batches reduce uncertainty, but only a capable delivery system makes frequent change safe."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

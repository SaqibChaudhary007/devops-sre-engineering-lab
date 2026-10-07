---
id: EXP-D00-010
domain: D00
topics:
  - D00-T007
level: L2-L3
type: experiment
status: draft
estimated_time: 50-70m
environment:
  - Local workstation
  - Spreadsheet or text editor optional
evidence_status:
  - DRAFT
---

# EXP-D00-010 — Build a Delivery Metrics, Toil, and Feedback Worksheet

## Objective

Practice measuring a delivery system without turning metrics into vanity targets.

This exercise uses the current DORA five-metric model:

~~~text
Throughput
├── Change Lead Time
├── Deployment Frequency
└── Failed Deployment Recovery Time

Instability
├── Change Fail Rate
└── Deployment Rework Rate
~~~

It also classifies operational work as toil vs judgment/engineering work.

## Safety

This is a local worksheet exercise.

No production access or organization data is required.

Use the hypothetical dataset below.

## Dataset

| Day | Deployments | Failed Deployments | Corrective Deployments | Median Change Lead Time | Recovery Time from Failed Deployment |
|---|---:|---:|---:|---:|---:|
| Mon | 3 | 0 | 0 | 10h | - |
| Tue | 4 | 1 | 1 | 9h | 35m |
| Wed | 2 | 0 | 0 | 12h | - |
| Thu | 5 | 1 | 1 | 8h | 20m |
| Fri | 4 | 0 | 1 | 7h | - |
| Sat | 0 | 0 | 0 | - | - |
| Sun | 0 | 0 | 0 | - | - |

These values are hypothetical.

## 1. Deployment Frequency

Calculate total deployments for the week and report:

- deployments/week
- average deployments per active deployment day

Do not label the result "good" or "bad" without context.

## 2. Change Lead Time

Review:

~~~text
10h, 9h, 12h, 8h, 7h
~~~

Ask:

- is the trend improving?
- which day is the outlier?
- what queue or bottleneck could explain it?
- what additional evidence is required?

## 3. Change Fail Rate

Calculate:

~~~text
Change Fail Rate
=
Failed Deployments
/
Total Deployments
× 100
~~~

Clearly state what this simplified exercise counts as a failed deployment.

## 4. Failed Deployment Recovery Time

Use only days with failed deployments:

~~~text
35m
20m
~~~

Calculate a simple average.

Then answer:

- is average enough?
- why might median or percentile views be useful?
- why should recovery definitions be explicit?

## 5. Deployment Rework Rate

Calculate:

~~~text
Deployment Rework Rate
=
Corrective Deployments
/
Total Deployments
× 100
~~~

Then explain what this reveals and why corrective deployment volume may expose instability not fully represented by failed-deployment count.

## 6. Avoid Metric Gaming

For each bad optimization, explain the likely failure.

### "Maximize deployment frequency"

Possible result:

- meaningless deployments
- unnecessary operational noise

### "Drive change fail rate to zero"

Possible result:

- fewer deployments
- giant approval queues
- larger batches
- hidden risk

### "Minimize lead time at all costs"

Possible result:

- skipped validation
- unstable releases

## 7. Toil Classification

Classify each task as:

~~~text
Likely Toil
Engineering Improvement
Judgment Work
Depends
~~~

Tasks:

1. Run the same deployment checklist manually every day.
2. Design a safer rollback mechanism.
3. Investigate a novel production failure.
4. Copy logs from five hosts every morning.
5. Build automated log collection.
6. Approve an exceptional high-risk production migration.
7. Reset the same environment by hand three times per week.
8. Create a reusable environment-reset workflow.
9. Review an architecture trade-off.
10. Manually create identical user permissions repeatedly.

For every "Likely Toil" item, propose an engineering improvement.

## 8. Feedback Loop Worksheet

Complete:

| Signal | Produced Where | Who Needs It | Expected Response Time | Action |
|---|---|---|---|---|
| Build failure | | | | |
| Test failure | | | | |
| Deployment failure | | | | |
| Latency regression | | | | |
| Error-rate increase | | | | |
| User complaint | | | | |
| Cost anomaly | | | | |

## 9. Senior Engineer Connection

A senior engineer should distinguish:

~~~text
Metric
from
Outcome
~~~

A metric is evidence. It is not the business objective itself.

## 10. SRE Connection

Connect delivery metrics to:

- deployment markers
- incidents
- SLO impact
- rollback/failover
- toil
- recovery

## 11. Architect Connection

Ask:

- which measurements should be standardized?
- what should remain service-specific?
- where can a platform provide common telemetry?
- which metrics are unsafe to compare across unrelated services without context?

## Validation Checklist

- [ ] Calculated all five current DORA metrics where applicable
- [ ] Explained assumptions
- [ ] Identified at least three metric-gaming risks
- [ ] Classified ten work items
- [ ] Proposed engineering improvements for toil
- [ ] Built a feedback-loop worksheet
- [ ] Distinguished metrics from outcomes

## Teach-Back

Explain:

> "Delivery metrics are diagnostic signals for improving a system, not targets to optimize in isolation."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

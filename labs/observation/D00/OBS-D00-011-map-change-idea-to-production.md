---
id: OBS-D00-011
domain: D00
topics:
  - D00-T007
level: L1-L2
type: observation
status: draft
estimated_time: 40-60m
environment:
  - Local workstation
  - Text editor or notebook
evidence_status:
  - DRAFT
---

# OBS-D00-011 — Map a Change from Idea to Production and Feedback

## Objective

Observe a complete software-delivery flow as a system instead of thinking only about individual tools.

You will map one hypothetical product change through:

~~~text
Idea
→ Plan
→ Code
→ Review
→ Build
→ Test
→ Release
→ Deploy
→ Operate
→ Observe
→ Learn
~~~

## Why This Matters

DevOps improves the end-to-end delivery system.

A fast coding step does not create fast delivery if work spends most of its time waiting in queues, handoffs, approvals, broken environments, or recovery.

## Safety

This is a documentation and reasoning exercise.

No production system, credentials, privileged access, or cloud resources are required.

## Scenario

Use this hypothetical change:

> Add a new API endpoint that allows a customer to update a notification preference.

Assume the organization has developers, code review, automated build, automated tests, a QA environment, production approval, deployment pipeline, production monitoring, and an incident/on-call process.

## 1. Draw the Current-State Flow

Create a table:

| Stage | Owner | Active Work Time | Waiting Time | Input | Output | Feedback |
|---|---|---:|---:|---|---|---|
| Idea | | | | | | |
| Plan | | | | | | |
| Code | | | | | | |
| Review | | | | | | |
| Build | | | | | | |
| Test | | | | | | |
| Release | | | | | | |
| Deploy | | | | | | |
| Operate | | | | | | |
| Observe | | | | | | |
| Learn | | | | | | |

You may invent reasonable times, but clearly label them as assumptions.

## 2. Identify Queues

Mark where work waits, such as review, build runner, QA environment, approval, or change window.

For at least three queues, write:

~~~text
Queue:
Cause:
Impact:
Possible improvement:
~~~

## 3. Identify Handoffs

For every responsibility transition, ask:

- what context could be lost?
- what information must travel with the work?
- can the handoff be reduced?
- can automation preserve evidence?

## 4. Identify Feedback Loops

Add feedback from code review, build, tests, deployment result, production metrics, logs/events, user behavior, and incident learning.

Classify each as Fast, Medium, or Slow.

## 5. Measure Flow Efficiency

Use:

~~~text
Flow Efficiency
=
Active Work Time
/
Total Elapsed Time
× 100
~~~

Example:

~~~text
Active work = 6 hours
Total elapsed = 30 hours
Flow efficiency = 20%
~~~

The exact number is less important than seeing how much time is waiting rather than engineering.

## 6. Find the Bottleneck

Answer:

1. Which stage limits throughput?
2. What evidence supports that conclusion?
3. Would adding more developers improve the bottleneck?
4. What system change would help more?

## 7. Production Feedback

Add this event:

> The new endpoint deploys successfully, but latency rises for a dependent service.

Explain which pre-production checks could have helped, what only production telemetry reveals, what signal should feed back to the delivery team, and what should be learned for the next release.

## 8. Senior Engineer Connection

A senior engineer should be able to explain where work waits, where feedback is slow, where ownership is unclear, where manual work exists, and where release risk accumulates.

## 9. SRE Connection

Connect the flow to deployment events, user-facing latency, errors, rollback/failover, failed deployment recovery time, and change fail rate.

## 10. Architect Connection

Ask which boundaries force handoffs, which controls should become automated, which platform capability could remove repeated delivery friction, and which risks still require human judgment.

## Validation Checklist

- [ ] Mapped the full change path
- [ ] Identified at least three queues
- [ ] Identified at least three handoffs
- [ ] Identified at least five feedback loops
- [ ] Calculated flow efficiency
- [ ] Identified a bottleneck using evidence
- [ ] Connected production feedback to future delivery improvement

## Teach-Back

Explain:

> "DevOps optimizes the delivery system, not only the pipeline."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completing and reviewing the exercise.

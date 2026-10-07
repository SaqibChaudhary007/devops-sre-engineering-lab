---
id: EXP-D00-021
domain: D00
topics:
  - D00-T013
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

# EXP-D00-021 — Error Budget, Toil, Automation, and Safe Change Decisions

## Objective

Practice SRE decision-making around error budgets, operational toil, automation candidates, and reliability-versus-change trade-offs.

## Safety

This is a local reasoning exercise.

No production deployment, live paging, automated remediation, or destructive testing is required.

## Scenario

A service has:

~~~text
SLO = 99.9% successful requests over 30 days

Recent issues:
- repeated manual restarts every few days
- one recurring certificate-renewal ticket
- frequent copy/paste health checks
- a release caused a short user-impacting outage
- on-call receives noisy CPU alerts
- a complex one-time data migration is being planned
~~~

## 1. Conceptual Error-Budget Reasoning

For:

~~~text
SLO = 99.9%
~~~

explain:

~~~text
100% - 99.9%
→ conceptual allowed unreliability
~~~

Then discuss how a team might react when:

- budget is healthy
- budget is being consumed unusually fast
- budget is nearly exhausted

Do not assume one universal freeze policy.

## 2. Reliability vs Change Velocity

Compare:

### Case A

~~~text
Reliability Healthy
→ normal controlled delivery
~~~

### Case B

~~~text
Reliability Degrading
→ higher scrutiny
→ reduce avoidable risk
→ prioritize reliability work
~~~

Explain why SRE aims for safe velocity rather than zero change.

## 3. Classify Toil vs Non-Toil

Classify each item:

~~~text
Likely Toil
Engineering Work
Operational Work but Not Clearly Toil
Needs More Context
~~~

Items:

- repeated manual restart
- recurring copy/paste health check
- one-time architecture redesign
- novel incident diagnosis
- repetitive certificate-renewal ticket
- building a durable automation system
- writing a new failure-mode test
- manually fixing the same configuration every week

Explain your reasoning.

## 4. Toil Characteristics

For each likely toil item, evaluate whether it is:

- manual
- repetitive
- automatable
- tactical/reactive
- low enduring value
- scaling with service growth

Explain why no single characteristic should automatically decide the classification.

## 5. Select an Automation Candidate

Choose one repeated task.

Use:

~~~text
Task
→ Preconditions
→ Safe Boundary
→ Automation
→ Observability
→ Validation
→ Failure Handling
~~~

Describe the automation conceptually.

Do not implement production-changing automation.

## 6. Automation Risk Review

For the chosen automation, ask:

- what if the input is wrong?
- what if the dependency is unavailable?
- what if the automation repeats?
- what if permissions are too broad?
- what evidence proves success?
- how can a human stop or override it?

Explain why automation can increase blast radius if the process is poorly understood.

## 7. Alert Review

Current alert:

~~~text
CPU > 80%
→ Page On-Call
~~~

Review whether that should:

- page
- create a ticket
- remain dashboard context
- depend on user impact

Propose a stronger user-impact signal.

## 8. On-Call Feedback Loop

Map:

~~~text
Repeated Page
→ Investigate Pattern
→ Identify Toil / Design Weakness
→ Engineering Work
→ Reduce Future Interrupts
~~~

Explain why permanent firefighting is not a mature SRE model.

## 9. Safe Change Review

A release previously caused a short outage.

Design a conceptual safer path:

~~~text
Small Change
→ Automated Checks
→ Limited Exposure
→ Observe
→ Validate
→ Continue / Stop / Recover
~~~

Explain what evidence is needed before wider rollout.

## 10. Senior Engineer Connection

Use:

~~~text
Reliability State
→ Change Risk
→ Toil
→ Automation Candidate
→ Safety Controls
→ Evidence
~~~

## 11. SRE Connection

Connect:

- SLO
- error budget
- on-call interrupts
- toil
- automation
- safe change

into one operating model.

## 12. Architect Connection

Decide:

- which operational work should remain human
- which work should be engineered away
- what automation boundaries are safe
- how reliability state should influence delivery risk

## Validation Checklist

- [ ] Explained conceptual error-budget use
- [ ] Avoided universal freeze-policy assumptions
- [ ] Classified toil carefully
- [ ] Identified a safe automation candidate
- [ ] Reviewed automation failure modes
- [ ] Improved alert/actionability reasoning
- [ ] Connected on-call pain to engineering work
- [ ] Designed a safer change path

## Teach-Back

Explain:

> "SRE uses reliability objectives to guide risk, turns recurring toil into engineering opportunities, and automates only when the task and failure boundaries are understood."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

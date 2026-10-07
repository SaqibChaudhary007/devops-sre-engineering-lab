# D00-T007 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- DevOps is an end-to-end delivery/operations system, not a tool
- flow and feedback are central
- queues, handoffs, WIP, and bottlenecks influence lead time
- smaller batches often reduce uncertainty and rollback scope
- automation improves repeatability but can amplify bad decisions
- CI is frequent integration plus automated validation
- continuous delivery and continuous deployment are different
- current DORA uses five delivery-performance metrics
- metrics are diagnostic signals, not universal targets
- ownership includes operating and learning from production outcomes
- toil has specific operational characteristics
- observability closes the production feedback loop
- shift left and shift right are complementary
- blameless learning focuses on system improvement
- DevOps, SRE, and platform engineering overlap but are not identical

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T007

Critical misconception override: no competency if the learner believes DevOps is primarily a tool/team, CI/CD equals owning a pipeline product, deployment frequency alone proves maturity, toil means undesirable work, blameless means no accountability, or platform engineering replaces DevOps.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Flow mapping | 10 |
| Queue / handoff / bottleneck reasoning | 15 |
| Batch-size reasoning | 10 |
| CI/CD reasoning | 10 |
| DORA metric interpretation | 15 |
| Ownership / feedback reasoning | 10 |
| Toil / automation reasoning | 10 |
| Shift-left/right and incident learning | 5 |
| Senior improvement plan | 5 |
| SRE / architecture trade-offs | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- identify waiting time instead of blaming coding speed
- identify code review, QA, approvals, and shared environments as likely queues
- connect large release windows to larger batches
- distinguish pipeline tooling from CI/CD outcomes
- correctly use all five current DORA metrics
- identify missing production feedback
- identify toil and propose engineering fixes
- improve security feedback without simply adding more gates
- improve recovery, not only prevention
- avoid proposing a new tool as the primary solution

## Follow-Up Evaluation

- L1: defines DevOps terms
- L2: connects flow, feedback, automation, and ownership
- L3: diagnoses delivery-system constraints
- L4: connects delivery to reliability and SLOs
- L5: designs organizational/platform/delivery trade-offs

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. adaptable, production-aware, and trade-off aware

Target: 4/5 average.

## Remediation Map

If weak on:

- why DevOps exists → revisit sections 3–8
- flow / queues / bottlenecks → revisit sections 9–16 and OBS-D00-011
- feedback loops → revisit sections 16–20 and OBS-D00-011
- CI/CD → revisit sections 21–24
- DORA metrics → revisit sections 25–30 and EXP-D00-010
- ownership / toil → revisit sections 31–34 and EXP-D00-010
- observability / security / shift left-right → revisit sections 35–39
- change / recovery → revisit sections 40–46
- DevOps vs SRE vs platform engineering → revisit sections 48–50
- Senior/SRE/Architect reasoning → revisit sections 52–56
- batch-size reasoning → complete EXP-D00-009

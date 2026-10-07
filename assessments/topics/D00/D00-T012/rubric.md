# D00-T012 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- reliability is broader than uptime/availability
- availability, durability, resilience, fault tolerance, and recoverability are distinct
- critical user journeys anchor reliability
- failure models and failure domains make reliability claims meaningful
- redundancy only helps when failures are sufficiently independent
- graceful degradation can preserve critical functionality
- failover requires detection, state, capacity, routing, and validation
- SLI measures behavior; SLO sets a target; SLA is a formal commitment
- error budgets represent allowed unreliability and should influence decisions
- 100% reliability is usually an inappropriate default
- reliability targets must reflect business value and cost
- observability and alert quality affect recovery speed
- change is a normal reliability risk
- capacity headroom enables recovery
- saturation can amplify failure
- load shedding/backpressure protect critical capacity
- backup success does not prove recovery
- RTO and RPO answer different questions
- runbooks, ownership, access, and validation affect recovery
- production readiness requires evidence

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T012

Critical misconception override: no competency if the learner believes reliability = uptime, replicas automatically guarantee resilience, backup = recovery, failover automation guarantees recovery, RTO = RPO, SLI/SLO/SLA are interchangeable, or all services should target maximum reliability.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Critical user journey / success criteria | 10 |
| Reliability-property reasoning | 10 |
| Failure domains / blast radius / redundancy | 15 |
| Graceful degradation / dependency criticality | 10 |
| Capacity headroom / saturation | 10 |
| Detection / response / recovery timeline | 10 |
| SLI / SLO / error-budget reasoning | 10 |
| Backup / RTO / RPO / recovery validation | 10 |
| Change safety / rollback vs roll-forward | 5 |
| Senior / SRE / Architect target design | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- define checkout reliability from user success, correctness, and latency
- distinguish availability from broader reliability
- identify correlated application/database failure domains
- degrade noncritical recommendation functionality
- quantify incident timing separately for detection/response/recovery
- recognize insufficient headroom after node loss
- improve alerts toward user-impact signals
- distinguish SLI, SLO, SLA, and error budget
- reject untested backups as proof of recovery
- separate RTO from RPO
- account for schema compatibility before rollback
- require practiced runbooks and clear ownership
- use production-readiness evidence rather than assumptions

## Follow-Up Evaluation

- L1: defines reliability concepts
- L2: connects user journeys, dependencies, failure domains, and recovery
- L3: diagnoses reliability incidents and recovery gaps
- L4: connects SLO/error-budget behavior to operations
- L5: designs reliability/cost/complexity trade-offs

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

- reliability properties / user journeys → revisit sections 3–11 and OBS-D00-016
- failure models / domains / redundancy → revisit sections 12–20 and EXP-D00-019
- detection / response / recovery / MTTR → revisit sections 21–26 and EXP-D00-020
- SLI / SLO / SLA / error budget → revisit sections 27–32 and EXP-D00-019
- dependency / end-to-end reliability → revisit sections 33–35 and OBS-D00-016
- health / observability / alerts → revisit sections 36–39 and EXP-D00-020
- change / rollback / roll-forward → revisit sections 40–42 and EXP-D00-020
- capacity / saturation / load shedding → revisit sections 43–47 and EXP-D00-020
- backup / RTO / RPO / DR → revisit sections 48–53 and EXP-D00-020
- runbooks / incident readiness / toil → revisit sections 54–58
- Senior/SRE/Architect reasoning → revisit sections 62–64

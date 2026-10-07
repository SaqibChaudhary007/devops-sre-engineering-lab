# D00-T013 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- SRE applies software-engineering methods to reliability and operations
- SRE is broader than monitoring or on-call
- SRE and DevOps overlap but are not identical concepts
- user journeys and service boundaries come before metrics
- SLIs measure behavior; SLOs set targets; SLAs are formal commitments
- error budgets represent allowed unreliability and should influence risk decisions
- 100% reliability is usually not the right default
- page/ticket/dashboard decisions depend on urgency and actionability
- on-call should be sustainable and feed engineering improvement
- toil is multi-dimensional, not simply unpleasant work
- automation should follow understanding and safety boundaries
- mitigation and permanent correction are different
- recovery must be validated against user impact
- postmortems should create systemic learning
- blameless does not mean accountability-free
- release engineering is part of reliability
- canarying/progressive delivery reduces initial exposure but does not prove correctness
- capacity/headroom and overload protection belong to SRE
- production readiness includes operational readiness and ownership

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T013

Critical misconception override: no competency if the learner believes SRE = monitoring/on-call, SLI/SLO/SLA are interchangeable, error budget = permission to be careless, every alert should page, toil = any disliked work, automation is always safer, mitigation must wait for perfect root cause, blameless = no accountability, or canary = proof of correctness.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| User journey / service boundary / SLI | 10 |
| SLO / SLA / error-budget reasoning | 15 |
| Alert quality / page-ticket-dashboard | 10 |
| Incident timeline / mitigation / validation | 15 |
| Toil / automation / on-call sustainability | 15 |
| Safe change / progressive delivery | 10 |
| Postmortem / blameless learning / action items | 10 |
| Production readiness / ownership | 5 |
| Capacity / dependency reliability | 5 |
| Senior / SRE / Architect target design | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- define checkout success from the user perspective
- select SLIs that reflect user-visible behavior
- distinguish SLO from SLA
- use error-budget health as a decision signal rather than a universal freeze rule
- replace raw CPU paging with user-impact-aware alerting
- distinguish pages, tickets, and dashboards
- separate mitigation from permanent correction
- identify repeated restart work as likely toil
- design automation only after defining safe conditions
- use on-call pain as engineering feedback
- use limited exposure and meaningful telemetry for rollout
- reject canary success as proof of correctness
- convert weak postmortem actions into specific improvements
- treat production readiness as an operational gate

## Follow-Up Evaluation

- L1: defines SRE concepts
- L2: connects user journeys, SLOs, alerting, toil, and incidents
- L3: operates through incidents and reliability trade-offs
- L4: designs SRE policy and sustainable operating practices
- L5: designs organization-scale SRE and risk-management trade-offs

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

- SRE purpose / SRE vs DevOps → revisit sections 3–8
- service boundaries / user journeys → revisit sections 8–9 and OBS-D00-017
- SLI / SLO / SLA / error budget → revisit sections 10–21 and OBS-D00-017
- alerting / paging / on-call → revisit sections 22–28 and OBS-D00-017 / EXP-D00-022
- toil / automation → revisit sections 29–32 and EXP-D00-021
- incident response / mitigation → revisit sections 33–37 and EXP-D00-022
- postmortems / blameless learning → revisit sections 38–40 and EXP-D00-022
- release engineering / progressive delivery → revisit sections 41–44 and EXP-D00-021 / EXP-D00-022
- capacity / overload / dependencies → revisit sections 45–48
- production readiness / ownership → revisit sections 49–54 and EXP-D00-022
- Senior/SRE/Architect reasoning → revisit sections 57–59

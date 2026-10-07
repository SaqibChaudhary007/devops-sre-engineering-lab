# D00-T014 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- observability is a capability for understanding system behavior
- monitoring and observability are complementary
- telemetry is evidence, not the same thing as observability
- instrumentation creates useful telemetry
- metrics, logs, traces, and events answer different questions
- the three-pillars model is useful but incomplete
- context and correlation are essential
- request/correlation/trace IDs are related but not universal synonyms
- structured logging improves filtering and correlation
- metric dimensions add context but increase cardinality/cost
- unbounded identifiers are poor metric labels
- aggregation can hide localized failures
- averages can hide tail latency
- percentiles/distributions improve latency understanding
- golden signals, RED, and USE are heuristics
- black-box and white-box evidence answer different questions
- business/dependency/queue signals matter
- change markers improve timeline reasoning
- sampling trades completeness for volume/cost
- retention is a value/cost/governance decision
- telemetry can contain sensitive production data
- instrumentation has overhead
- dashboards should answer questions
- alerts should carry operational context
- evidence-first troubleshooting starts from impact, not commands
- correlation creates hypotheses; validation establishes confidence

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T014

Critical misconception override: no competency if the learner believes observability = dashboards, telemetry = observability, monitoring and observability are mutually exclusive, all identifiers are safe metric labels, averages are sufficient for latency, correlation proves causation, queue depth alone proves health, or collecting everything forever is best practice.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| User-centered impact / service scope | 10 |
| Metrics / logs / traces / events mapping | 10 |
| Correlation identity / structured logging | 10 |
| Cardinality / metric-label design | 15 |
| Latency / aggregation / regional analysis | 10 |
| Queue / dependency / change-marker reasoning | 10 |
| Hypothesis ranking / evidence-first investigation | 15 |
| Sampling / retention / cost / security | 10 |
| Dashboard / alert redesign | 5 |
| Senior / SRE / Architect target design | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- start from checkout user impact
- map evidence across metrics/logs/traces/events
- propagate context across services
- reject unbounded identifiers as metric labels
- use distributions/percentiles rather than averages alone
- segment by region/version/endpoint when useful
- include queue age, producer/consumer rate, retry volume, and DLQ evidence
- use deployment markers as hypotheses, not proof
- rank multiple hypotheses rather than jump to one cause
- balance sampling/retention with cost and privacy
- redesign dashboards around operational questions
- alert on user-impact conditions with context
- validate recovery from end-to-end evidence

## Follow-Up Evaluation

- L1: defines observability concepts
- L2: connects signal types, context, and correlation
- L3: investigates incidents using evidence
- L4: designs SRE observability practices and policies
- L5: designs architecture/governance/cost trade-offs

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

- observability vs monitoring / telemetry → revisit sections 3–7
- metrics / logs / traces / events → revisit sections 8–13 and OBS-D00-018
- context / IDs / spans / structured logging → revisit sections 14–20 and OBS-D00-018
- dimensions / cardinality → revisit sections 22–24 and EXP-D00-023
- aggregation / percentiles / latency distributions → revisit sections 25–28 and EXP-D00-023
- golden signals / RED / USE → revisit sections 30–34
- black-box / white-box / business / dependency / queues → revisit sections 35–42
- change markers / time / causation → revisit sections 43–46 and EXP-D00-024
- sampling / retention / telemetry cost → revisit sections 47–50 and EXP-D00-023
- signal quality / blind spots / security / overhead → revisit sections 51–56
- evidence-first troubleshooting → revisit sections 57–59 and EXP-D00-024
- dashboards / alerts / alert context → revisit sections 60–63 and EXP-D00-024
- Senior/SRE/Architect reasoning → revisit sections 68–70

# D00-T014 Assessment Package — Observability Foundations

This package evaluates whether the learner can reason about observability as an engineering capability built from instrumentation, telemetry, context, correlation, and evidence-driven investigation.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Observability Scenario](applied-scenario.md)
3. [Senior / SRE / Architect Follow-Ups](interview-followups.md)
4. [Teach-Back Assessment](teach-back.md)
5. [Rubric & Remediation Guide](rubric.md)

## Recommended Order

Knowledge Check
→ Applied Scenario
→ Follow-Ups
→ Teach-Back
→ Rubric Review

## Topic Competency Guidance

Recommended minimum:

- Knowledge Check: 80%
- Applied Scenario: 75%
- Follow-Up Depth: FD-3
- Reasoning Level: at least L3
- Teach-Back: 4/5 average
- No critical misconception around observability vs monitoring, telemetry vs observability, signal correlation, cardinality, tail latency, sampling/retention, correlation vs causation, or evidence-first troubleshooting

## Critical Misconceptions

A learner should not leave this topic believing that:

- observability means dashboards only
- telemetry automatically means the system is observable
- monitoring and observability are mutually exclusive
- metrics, logs, and traces are always the complete observability model
- request ID, correlation ID, and trace ID are universal synonyms
- more metric labels are always better
- averages are sufficient for latency analysis
- correlation proves root cause
- queue depth alone defines queue health
- more telemetry is always better
- collecting everything forever is mature observability
- telemetry is harmless from a security/privacy perspective
- instrumentation has zero overhead
- random commands are a valid first troubleshooting step

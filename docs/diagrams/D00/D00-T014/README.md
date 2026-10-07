# D00-T014 Visual / Diagram Package — Observability Foundations

This package provides reusable diagrams for **00.14 — Observability Foundations**.

## Diagram Set

1. [DIA-D00-077 — System → Instrumentation → Telemetry → Correlation → Insight](DIA-D00-077-system-instrumentation-telemetry-correlation-insight.md)
2. [DIA-D00-078 — Metrics vs Logs vs Traces vs Events](DIA-D00-078-metrics-logs-traces-events.md)
3. [DIA-D00-079 — User Journey → Trace → Spans → Logs / Metrics](DIA-D00-079-user-journey-trace-spans-logs-metrics.md)
4. [DIA-D00-080 — RED vs USE vs Golden Signals](DIA-D00-080-red-use-golden-signals.md)
5. [DIA-D00-081 — Change Marker → Symptom → Dependency → Root-Cause Hypothesis](DIA-D00-081-change-symptom-dependency-hypothesis.md)
6. [DIA-D00-082 — Cardinality / Sampling / Retention / Cost Trade-Off](DIA-D00-082-cardinality-sampling-retention-cost.md)

## Learning Progression

~~~text
System Behavior
→ Instrumentation
→ Telemetry
→ Context
→ Correlation
→ Interpretation
→ Hypothesis
→ Validation
→ Action
~~~

## Design Rules

- stay provider-neutral
- distinguish monitoring, telemetry, observability, and troubleshooting
- show metrics/logs/traces/events as complementary signals
- preserve context and correlation identity across distributed flows
- show that averages can hide tail latency
- show RED, USE, and golden signals as heuristics rather than complete architectures
- treat correlation as hypothesis evidence, not proof of causation
- show cardinality, sampling, retention, privacy, and cost as architecture trade-offs
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Detailed Prometheus, OpenTelemetry, ELK, Instana, Grafana, query languages, tracing backends, sampling algorithms, telemetry pipelines, and vendor-specific implementation belong to later domains.

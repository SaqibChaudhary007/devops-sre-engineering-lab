# D00-T014 Source Verification — Observability Foundations

## Verification Goal

Verify the core claims in **00.14 — Observability Foundations** against authoritative observability, tracing, metrics, and cloud operational guidance.

Primary source families used:

- OpenTelemetry documentation and specification
- Prometheus documentation
- W3C Trace Context Recommendation
- Google SRE material
- Microsoft Azure Well-Architected observability guidance

## Verification Status

**Result:** Core claims verified with important nuances around observability vs monitoring, instrumentation, telemetry, signal types, context propagation, correlation, cardinality, latency distributions, sampling, retention, security/privacy, cost, and evidence-first troubleshooting.

**Evidence level:** E2 — supported by first-party standards/documentation and authoritative operational guidance.

This topic remains at the D00 mental-model level. Detailed OpenTelemetry SDK/Collector configuration, PromQL, log-query languages, sampling algorithms, native histogram internals, cardinality engineering, tracing backend design, profiling, exemplars, and vendor-specific observability implementation belong to later domains.

---

# Primary / Authoritative Sources

## 1. OpenTelemetry — Observability Primer

- https://opentelemetry.io/docs/concepts/observability-primer/
- https://opentelemetry.io/docs/what-is-opentelemetry/

Supports:

- observability is about understanding a system from its externally visible outputs
- instrumentation is required to emit useful telemetry
- traces, metrics, and logs are core observability signals
- observability supports troubleshooting of both known and novel problems
- telemetry and observability are related but not identical concepts

### Verified nuance

The canonical topic is correct to separate:

~~~text
Telemetry
→ emitted evidence

Observability
→ capability to understand system behavior from useful telemetry + context + analysis
~~~

Do not equate "having telemetry" with "being observable."

---

## 2. OpenTelemetry — Signals and Context

- https://opentelemetry.io/docs/concepts/signals/
- https://opentelemetry.io/docs/concepts/
- https://opentelemetry.io/docs/specs/status/

Supports:

- OpenTelemetry supports traces, metrics, logs, and baggage
- profiles are emerging / under active development
- context propagation is a shared mechanism for correlating distributed telemetry
- different signals reveal different aspects of system behavior

### Verified nuance

The common "three pillars" model is useful but incomplete.

At D00, teach metrics/logs/traces first, while recognizing events, baggage/context, profiles, topology, metadata, and business signals may also matter.

---

## 3. OpenTelemetry — Logging and Trace Correlation

- https://opentelemetry.io/docs/specs/otel/logs/

Supports:

- logs can carry trace and span context
- trace/span identifiers improve correlation between logs and traces
- correlation across signals increases observability value in distributed systems
- standardized source/context fields improve analysis

### Verified nuance

"Request ID," "correlation ID," and "trace ID" are related identity concepts but not universal synonyms.

The durable lesson is to preserve stable identifiers that connect related evidence across a workflow.

---

## 4. W3C Trace Context

- https://www.w3.org/TR/trace-context/

Supports:

- distributed trace context should be propagated across service boundaries
- traceparent identifies the incoming request's trace position
- tracestate can carry vendor-specific trace information
- standardized trace context helps preserve interoperability across distributed systems

### Verified nuance

At D00, teach:

~~~text
Trace Context
→ propagated identity
→ connected spans
→ reconstruct distributed request path
~~~

Do not overfit the topic to one tracing vendor.

---

## 5. Prometheus — Instrumentation and Labels

- https://prometheus.io/docs/practices/instrumentation/
- https://prometheus.io/docs/practices/naming/

Supports:

- labels add dimensional context to metrics
- each unique label combination creates a separate time series
- excessive/high-cardinality labels increase resource and storage cost
- user IDs, email addresses, and other unbounded values are risky metric labels
- instrumentation itself has performance cost, though usually justified when designed carefully

### Verified nuance

The exact acceptable cardinality depends on the telemetry platform and scale.

Prometheus guidance contains practical thresholds and rules of thumb; do not teach those values as universal observability laws.

The general principle is:

~~~text
More Dimensions
→ More Diagnostic Context
→ More Series / Cost / Complexity
~~~

---

## 6. Prometheus — Histograms, Summaries, and Quantiles

- https://prometheus.io/docs/practices/histograms/

Supports:

- latency should be treated as a distribution rather than only an average
- quantiles / percentiles describe positions within observed distributions
- histograms and summaries represent distributions differently
- aggregation behavior matters when choosing metric representations

### Verified nuance

At D00, retain only:

> Averages can hide tail behavior, and percentiles/distributions preserve more information about user experience.

Detailed histogram/summary/native-histogram implementation belongs later.

---

## 7. Microsoft Azure Well-Architected — Monitoring / Observability Architecture

- https://learn.microsoft.com/en-us/azure/well-architected/design-guides/monitoring
- https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/observability

Supports:

- instrumentation generates telemetry
- telemetry commonly includes metrics, logs, traces, and events
- correlation should connect evidence across components and layers
- structured telemetry and consistent context improve analysis
- telemetry should align with user/business flows
- dashboards and alerts should support operational decisions
- telemetry pipelines need intentional storage, retention, scaling, and governance
- excessive logging can create noise and cost
- missing correlation/context creates troubleshooting blind spots

### Verified nuance

Observability architecture is not only an agent/backend choice.

It includes:

~~~text
Instrumentation
→ Collection
→ Transport
→ Storage
→ Correlation
→ Analysis
→ Visualization
→ Alerting
→ Retention / Governance
~~~

At D00 we keep this conceptual rather than product-specific.

---

## 8. Azure — Structured Telemetry, Business Context, and Correlation

- https://learn.microsoft.com/en-us/azure/well-architected/design-guides/monitoring

Supports:

- telemetry should include useful source/environment/deployment/dependency context
- structured telemetry improves queryability and filtering
- correlation IDs help connect distributed activity
- business KPIs should be considered alongside technical indicators
- timestamps should be consistent enough to aid cross-service correlation

### Verified nuance

Telemetry should include context that helps answer operational questions, but sensitive or high-cardinality fields require careful governance.

---

## 9. Security / Privacy / Governance of Telemetry

- https://learn.microsoft.com/en-us/azure/well-architected/design-guides/monitoring
- https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/observability

Supports:

- telemetry can include regulated/sensitive information
- access controls, classification, retention, and governance matter
- logs should not be assumed harmless
- telemetry volume and retention should reflect actual use and policy needs

### Verified nuance

Observability data must be designed under the same security/privacy thinking as other production data.

Do not log secrets or sensitive payloads merely because troubleshooting might be easier.

---

## 10. Monitoring, Alerts, and Actionability

- https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/principles
- https://sre.google/sre-book/monitoring-distributed-systems/

Supports:

- monitoring should focus on meaningful operational conditions
- alerts should be actionable
- dashboards should be aligned with operational and business questions
- user-visible latency, traffic, errors, and saturation are useful service-level signals

### Verified nuance

Golden signals are a useful SRE mental model, not a complete observability architecture.

Similarly, RED and USE are useful frameworks for particular questions, not universal schemas for every system.

---

# Verified Claim Map

| Topic claim | Verification | Primary source family |
|---|---|---|
| Observability helps understand internal behavior from external evidence | Verified | OpenTelemetry |
| Monitoring and observability are complementary | Verified at mental-model level | OTel / Azure |
| Telemetry is not the same as observability | Verified | OpenTelemetry |
| Instrumentation creates telemetry | Verified | OpenTelemetry / Azure |
| Metrics/logs/traces/events answer different questions | Verified | OpenTelemetry / Azure |
| "Three pillars" is useful but incomplete | Verified with current OTel signal model | OpenTelemetry |
| Context and correlation are essential | Verified | OTel / W3C / Azure |
| Trace context enables cross-service correlation | Verified | W3C Trace Context |
| Structured logs improve filtering/correlation | Verified | OTel / Azure |
| Metric dimensions improve context but increase cost/cardinality | Verified | Prometheus |
| High-cardinality unbounded labels are risky | Verified | Prometheus |
| Aggregation can hide local behavior | Verified at mental-model level | Prometheus / Azure |
| Averages can hide tail latency | Verified | Prometheus distributions/quantiles |
| Percentiles describe tail behavior better than averages alone | Verified | Prometheus |
| Golden Signals are useful but incomplete | Verified at mental-model level | Google SRE |
| RED and USE are scoped methods, not full observability architectures | Verified at mental-model level | Method definitions / monitoring practice |
| Black-box and white-box signals answer different questions | Verified at mental-model level | SRE monitoring practice |
| Business signals should complement technical signals | Verified | Azure |
| Queue depth alone may be insufficient | Verified at mental-model level | Operational monitoring practice |
| Change markers improve incident correlation | Verified | Azure |
| Correlation is evidence, not proof of causation | Verified as reasoning principle | Operational practice |
| Sampling trades completeness for cost/volume | Verified | OpenTelemetry / Azure |
| Retention is a value/cost/governance trade-off | Verified | Azure |
| More telemetry is not always better | Verified | Azure / Prometheus |
| Telemetry can contain sensitive data | Verified | Azure |
| Instrumentation has overhead | Verified | Prometheus / Azure |
| Dashboards should answer operational questions | Verified | Azure |
| Alerts should be actionable and contextual | Verified | Azure / Google SRE |

---

# Verified Nuances / Corrections

## 1. Observability Is a Capability, Not a Tool

Do not define observability as:

~~~text
Prometheus + Grafana + Logs
~~~

A better model is:

~~~text
Instrumentation
→ Telemetry
→ Context
→ Correlation
→ Analysis
→ Operational Understanding
~~~

Tools implement parts of the capability.

## 2. Monitoring vs Observability Is Not a War

Avoid teaching:

~~~text
Monitoring = old
Observability = new
~~~

A stronger model is:

~~~text
Monitoring
→ detect known/important conditions

Observability
→ investigate broader system behavior

Troubleshooting
→ form and validate decisions
~~~

They overlap and reinforce each other.

## 3. "Three Pillars" Is Pedagogical, Not Complete

Metrics, logs, and traces are useful foundational signals.

But modern observability can also use:

- events
- profiles
- topology
- business signals
- change metadata
- baggage/context

## 4. Identity Terms Need Scope

Request ID, correlation ID, and trace ID are not universally defined the same way across all systems.

Teach the invariant:

> Related telemetry should preserve identifiers that allow evidence to be correlated across components and time.

## 5. Cardinality Is a Platform Economics Problem

High cardinality creates more distinct time series and greater resource cost.

Do not hard-code one universal numerical threshold.

The safe D00 rule is:

> Unbounded identifiers such as user IDs, request IDs, emails, or random UUIDs are generally poor metric-label choices.

## 6. Percentiles Need Careful Interpretation

A percentile is a position in a distribution.

At D00, use percentiles to teach tail latency awareness.

Do not yet teach aggregation mathematics or backend-specific percentile semantics.

## 7. Golden Signals / RED / USE Are Heuristics

Golden signals:

~~~text
Latency
Traffic
Errors
Saturation
~~~

RED:

~~~text
Rate
Errors
Duration
~~~

USE:

~~~text
Utilization
Saturation
Errors
~~~

These are useful starting frameworks.

They do not replace workload-specific user, business, dependency, queue, and correctness signals.

## 8. Correlation Is Not Root Cause

A release marker and an error spike at the same time create a strong hypothesis.

They do not prove the release caused the failure.

Hypotheses still require safe validation.

## 9. Sampling Is Selective Evidence

Sampling reduces telemetry volume and cost but can remove rare-event evidence.

The right policy depends on:

- signal value
- traffic volume
- debugging requirements
- cost
- compliance

Detailed sampling algorithms come later.

## 10. Retention Is Not "Keep Everything"

Long retention may support trend analysis, audits, and incident comparison.

But it also increases:

- storage cost
- privacy exposure
- governance burden
- indexing/query complexity

## 11. Telemetry Is Production Data

Logs, traces, attributes, and baggage may include sensitive information.

Telemetry design must include:

- access control
- data minimization
- retention
- classification
- secret avoidance

## 12. Observability Has Overhead

Instrumentation, agents, network export, storage, and queries consume resources.

More detail must be justified by operational value.

## 13. Dashboards Should Be Question-Driven

A dashboard should answer a concrete question such as:

- is the user journey healthy?
- what changed?
- which dependency is degraded?
- where is saturation increasing?

Panel count is not observability maturity.

## 14. Observability Maturity Is Operational Usefulness

A mature system is not the one with the most tools.

It is the one where engineers can quickly:

~~~text
Detect
→ Scope
→ Correlate
→ Hypothesize
→ Validate
→ Recover
~~~

with trustworthy evidence.

---

# Evidence Decision

The following D00-T014 areas are now eligible for **DOC-VERIFIED** status:

- observability definition and purpose
- monitoring vs observability mental model
- telemetry vs observability distinction
- instrumentation
- metrics / logs / traces / events
- context and correlation
- request/correlation/trace identity at foundation level
- trace context propagation
- spans at foundation level
- structured logging
- dimensions / labels / attributes
- cardinality risk
- aggregation trade-offs
- averages vs tail latency
- percentiles / distributions at foundation level
- traffic / errors / saturation
- golden-signals preview
- RED / USE previews
- black-box / white-box distinction at foundation level
- business / dependency / queue signals
- change markers
- sampling trade-offs
- retention trade-offs
- telemetry cost
- signal quality / noisy telemetry
- telemetry gaps / blind spots
- ephemeral-workload evidence durability
- security/privacy considerations
- instrumentation overhead
- evidence-first troubleshooting
- dashboards and alert context
- correlation vs causation
- observability maturity

The following remain intentionally preview-level pending later domains:

- Prometheus metric-type internals
- native histograms
- PromQL
- OpenTelemetry SDK configuration
- OpenTelemetry Collector pipelines
- tail/head sampling algorithms
- baggage governance
- profiling
- exemplar implementation
- trace-storage architecture
- log-index design
- query languages
- multi-tenant observability platforms
- telemetry SLOs
- cost-at-scale optimization
- vendor-specific observability implementation

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured exercises:

- map a user journey to metrics/logs/traces/events
- distinguish monitoring from observability questions
- design structured log fields
- design correlation identity
- identify dangerous metric cardinality
- compare average and percentile latency
- classify black-box vs white-box evidence
- build a symptom → dependency → resource investigation path
- add change markers to an incident timeline
- review a dashboard and alert set for signal quality

These become the D00-T014 practical package.

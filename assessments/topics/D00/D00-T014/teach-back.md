# D00-T014 — Teach-Back Assessment

## Goal

Demonstrate that you can explain observability as an evidence system for operating and troubleshooting production services.

## Task A — Beginner

Explain:

- observability
- monitoring
- telemetry
- instrumentation

Keep the differences clear.

## Task B — Signal Types

Explain:

~~~text
Metrics
Logs
Traces
Events
~~~

and what question each helps answer.

## Task C — Context and Correlation

Explain:

- request ID
- correlation/workflow ID
- trace ID
- span

Then explain why identity must propagate across services.

## Task D — Cardinality

Explain why:

~~~text
service
region
status
~~~

are often useful labels while:

~~~text
user_id
request_id
email
random_uuid
~~~

are usually dangerous metric labels.

## Task E — Tail Latency

Explain why average latency is insufficient.

Explain p95/p99 at a conceptual level.

## Task F — RED / USE / Golden Signals

Explain what each framework is for and why none is a full observability architecture.

## Task G — Incident Investigation

Teach this sequence:

~~~text
Impact
→ Scope
→ Timeline
→ Changes
→ User Signals
→ Dependencies
→ Resources
→ Logs / Traces
→ Hypothesis
→ Safe Validation
~~~

## Task H — Correlation vs Causation

Explain why:

~~~text
Deployment Marker
+ Error Spike
~~~

creates a hypothesis, not proof.

## Task I — Sampling / Retention / Cost

Explain how observability balances:

- diagnostic value
- completeness
- cost
- privacy
- runtime overhead

## Task J — Architect

Explain what observability standards you would require before a service is production-ready.

## Scoring

Score 1–5 for:

- correctness
- clarity
- observability/monitoring distinction
- telemetry/correlation reasoning
- cardinality/economics reasoning
- incident-investigation reasoning
- security/privacy awareness
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

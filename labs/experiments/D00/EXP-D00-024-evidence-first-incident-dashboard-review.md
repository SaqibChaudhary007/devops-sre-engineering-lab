---
id: EXP-D00-024
domain: D00
topics:
  - D00-T014
level: L2-L3
type: experiment
status: draft
estimated_time: 60-80m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# EXP-D00-024 — Evidence-First Incident Investigation and Dashboard Review

## Objective

Practice observability-driven troubleshooting using user impact, timelines, change markers, service/dependency/resource signals, logs, traces, and safe hypothesis validation.

## Safety

This is a local reasoning exercise.

No production access, live incident manipulation, or destructive testing is required.

## Scenario

A checkout service has the following symptoms:

~~~text
14:00 — checkout p95 latency starts rising
14:03 — payment dependency latency rises
14:05 — retry volume increases
14:07 — queue age increases
14:08 — checkout error rate increases
14:10 — deployment marker appears for Order Service v42
14:12 — CPU remains normal
14:14 — one region shows much worse latency than others
~~~

Available evidence:

- request success ratio
- p50 / p95 / p99 latency
- payment dependency latency
- retry count
- queue depth and oldest-message age
- regional metrics
- structured application logs
- distributed traces
- deployment markers
- node/resource metrics

## 1. Start with Impact

Do not begin with random commands.

Define:

- what users are experiencing
- which journey is affected
- whether all users or one region are affected
- when impact started
- what SLI is degraded

## 2. Build the Timeline

Create:

~~~text
User Impact
→ Dependency Change
→ Retry Increase
→ Queue Growth
→ Error Increase
→ Deployment Marker
→ Regional Divergence
~~~

Explain which signals moved first and why ordering matters.

## 3. Generate Hypotheses

Create at least four ranked hypotheses, for example:

- payment dependency slowdown
- regional network issue
- Order Service deployment regression
- retry amplification
- queue-consumer slowdown

For each hypothesis, write:

~~~text
Evidence Supporting
Evidence Missing
Evidence Contradicting
Next Safe Check
~~~

## 4. Correlation vs Causation

The deployment marker appears after latency had already started rising.

Explain why:

~~~text
Deployment Correlated with Incident
~~~

does not automatically mean:

~~~text
Deployment Caused Incident
~~~

Use the timeline to refine the hypothesis.

## 5. Metrics Investigation Path

Use a progressive path:

~~~text
User Impact
→ Service RED Signals
→ Dependency Signals
→ Queue Signals
→ Resource USE Signals
→ Detailed Diagnostics
~~~

Explain why jumping directly to CPU can miss the real problem.

## 6. Logs

Use structured logs to answer:

- which service reports timeouts?
- which dependency is involved?
- which region is affected?
- which version is involved?
- do request/trace IDs connect related records?

Explain which missing log fields would create blind spots.

## 7. Traces

Use a conceptual slow trace:

~~~text
Checkout
├── API = 50 ms
├── Auth = 40 ms
├── Order = 80 ms
├── Payment = 4.5 s
└── Database = 30 ms
~~~

Explain what the trace suggests and what it does not yet prove.

## 8. Queue Evidence

Suppose:

~~~text
Queue depth = moderate
Oldest message age = rising
Consumer rate = falling
~~~

Explain why queue age and consumer rate can be more informative than depth alone.

## 9. Regional Comparison

Compare:

~~~text
Region A = normal
Region B = degraded
Region C = normal
~~~

Explain how regional segmentation reduces the investigation scope.

## 10. Dashboard Review

Review a dashboard that currently shows only:

- CPU
- memory
- disk
- node count

Redesign it using:

~~~text
User Impact
→ Service Behavior
→ Dependencies
→ Queues
→ Resources
→ Changes
→ Diagnostics
~~~

Include:

- checkout success
- p95 latency
- error rate
- payment latency
- retry rate
- queue age
- region
- release/version marker

## 11. Alert Context

Design an alert payload that includes:

- affected service
- user journey
- symptom
- start time
- region
- version
- dependency
- dashboard/reference link
- next investigation question

Explain why context reduces time-to-understand.

## 12. Recovery Validation

Assume payment latency returns to normal.

Do not stop there.

Validate:

- checkout success restored
- p95 latency acceptable
- error rate normal
- retry volume normal
- queue age falling
- no region remains degraded
- user journey works end to end

## 13. Senior Engineer Connection

Use:

~~~text
Impact
→ Scope
→ Timeline
→ Changes
→ Service Signals
→ Dependencies
→ Resources
→ Logs / Traces
→ Hypothesis
→ Safe Validation
~~~

## 14. SRE Connection

Connect observability to:

- SLI/SLO
- paging
- MTTR
- error-budget impact
- recovery validation
- missing telemetry remediation

## 15. Architect Connection

Ask:

- which signals should be standardized?
- what context must propagate across services?
- which change events must be visible?
- what dashboard hierarchy should every service have?
- which telemetry gaps should block production readiness?

## Validation Checklist

- [ ] Started from user impact
- [ ] Built a timeline
- [ ] Ranked hypotheses
- [ ] Distinguished correlation from causation
- [ ] Used service/dependency/resource evidence progressively
- [ ] Used structured logs and trace reasoning
- [ ] Interpreted queue evidence correctly
- [ ] Reduced scope with regional comparison
- [ ] Improved dashboard hierarchy
- [ ] Added useful alert context
- [ ] Validated recovery against the user journey

## Teach-Back

Explain:

> "Observability-driven troubleshooting starts with impact and evidence, narrows the search through correlated signals, forms hypotheses, and validates them safely."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

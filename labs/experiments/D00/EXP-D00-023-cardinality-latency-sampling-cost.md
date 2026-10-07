---
id: EXP-D00-023
domain: D00
topics:
  - D00-T014
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

# EXP-D00-023 — Cardinality, Tail Latency, Sampling, and Telemetry Cost

## Objective

Practice observability design trade-offs involving metric dimensions, cardinality, latency distributions, sampling, retention, and cost.

## Safety

This is a local reasoning exercise.

No production telemetry system, paid observability backend, or load generation is required.

## Scenario

A checkout service emits:

~~~text
request_count
request_latency_ms
payment_errors
queue_depth
~~~

A proposed metric design adds labels:

~~~text
service
region
endpoint
status
version
user_id
request_id
email
random_uuid
~~~

The team also stores every trace forever and keeps debug logs enabled continuously.

## 1. Classify Metric Dimensions

Classify each label as:

~~~text
Usually Useful
Potentially Useful with Care
High-Cardinality Risk
Should Not Be a Metric Label
~~~

Explain your reasoning.

## 2. Cardinality Mental Model

Use:

~~~text
Unique Label Combinations
→ More Time Series
→ More Memory / Storage / Query Work
→ More Cost / Complexity
~~~

Explain why user IDs, request IDs, email addresses, and random UUIDs are generally poor metric-label choices at scale.

## 3. Preserve Context Without High-Cardinality Metrics

For high-cardinality identifiers, decide whether they belong better in:

- logs
- traces
- events
- exemplars
- business data outside telemetry

Explain why the same context can be valuable in one signal type but dangerous in another.

## 4. Average vs Tail Latency

Use this simplified latency sample:

~~~text
90 requests = 100 ms
9 requests = 500 ms
1 request = 10 seconds
~~~

Explain:

- what the average can hide
- why p95/p99 thinking matters
- why latency should be treated as a distribution

Do not perform backend-specific histogram calculations.

## 5. Aggregation Trade-Off

Compare:

~~~text
Global latency
Regional latency
Endpoint latency
Version latency
~~~

Explain how broad aggregation can hide a localized failure.

Then explain how over-segmentation can create noise and cost.

## 6. Sampling Decision

Assume trace volume is too high to retain fully.

Compare:

~~~text
Keep All Traces
Sample Some Traces
Keep Error / Slow Traces Preferentially
~~~

At D00, discuss only conceptual trade-offs:

- cost
- completeness
- rare-event visibility
- debugging value

Do not design a production sampling algorithm.

## 7. Retention Decision

Compare:

~~~text
7 days
30 days
180 days
Forever
~~~

For:

- debug logs
- high-value security/audit events
- request metrics
- traces

Explain how value, cost, privacy, and investigation needs affect retention.

## 8. Telemetry Cost Review

Identify major cost sources:

- ingestion
- storage
- indexing
- query compute
- network transfer
- agent/runtime overhead
- engineering maintenance

Explain why collecting everything forever is not a mature design.

## 9. Security / Privacy Review

Review these fields:

~~~text
access_token
password
email
customer_id
request_payload
trace_id
service_version
~~~

Classify them as:

~~~text
Never Emit
Sensitive / Govern Carefully
Usually Safe Operational Context
Depends on Payload
~~~

Explain why telemetry is production data.

## 10. Signal-Quality Review

A dashboard has 70 panels, but nobody knows which ones matter during incidents.

Redesign the hierarchy:

~~~text
User Impact
→ Service Behavior
→ Dependencies
→ Resources
→ Detailed Diagnostics
~~~

Explain why panel count is not observability maturity.

## 11. Senior Engineer Connection

Use:

~~~text
Question
→ Required Context
→ Signal Type
→ Cardinality
→ Retention
→ Cost
→ Operational Value
~~~

## 12. SRE Connection

Connect observability economics to:

- alert quality
- SLO operation
- incident investigation
- MTTR
- recovery validation

## 13. Architect Connection

Decide:

- which telemetry deserves high detail
- which dimensions should be standardized
- which identifiers belong outside metrics
- where sampling is acceptable
- how retention should differ by signal
- what telemetry cost is justified

## Validation Checklist

- [ ] Identified high-cardinality metric labels
- [ ] Moved unbounded context to safer signal types
- [ ] Explained average vs tail latency
- [ ] Explained aggregation trade-offs
- [ ] Explained sampling trade-offs
- [ ] Designed retention reasoning
- [ ] Reviewed telemetry cost
- [ ] Reviewed privacy/security risks
- [ ] Improved dashboard hierarchy

## Teach-Back

Explain:

> "Observability design is a trade-off between diagnostic value, cardinality, retention, sampling, cost, privacy, and runtime overhead."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

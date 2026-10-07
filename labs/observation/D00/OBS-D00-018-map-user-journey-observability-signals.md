---
id: OBS-D00-018
domain: D00
topics:
  - D00-T014
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# OBS-D00-018 — Map a User Journey to Metrics, Logs, Traces, and Events

## Objective

Map one user journey to the telemetry and context needed to observe it end to end.

## Why This Matters

A system can emit large amounts of telemetry and still be difficult to investigate if the evidence is disconnected, lacks context, or does not represent the user journey.

## Safety

This is a local reasoning exercise only.

No production access, agent installation, live tracing, or disruptive testing is required.

## Scenario

Use this journey:

~~~text
Customer
→ Checkout API
→ Authentication
→ Order Service
→ Payment Provider
→ Database
→ Queue
→ Fulfillment Worker
~~~

The user goal is:

~~~text
Complete checkout correctly and within acceptable time.
~~~

## 1. Define the User-Centered Question

Write the primary operational question:

> Can the customer complete checkout successfully, correctly, and within the expected time?

Then define what evidence would help answer it.

## 2. Map Metrics

For each component, identify useful metrics such as:

- request rate
- error rate
- latency
- saturation
- queue depth
- oldest-message age
- retry rate
- dependency timeout rate

Classify each metric as:

~~~text
User Outcome
Service Behavior
Dependency Behavior
Resource Behavior
~~~

## 3. Map Logs

Design useful structured log fields:

~~~text
timestamp
service
environment
version
request_id
trace_id
operation
status
duration_ms
dependency
error_type
~~~

Explain why free-form text alone can make correlation harder.

## 4. Map Traces

Design a conceptual trace:

~~~text
Checkout Trace
├── API Span
├── Authentication Span
├── Order Span
├── Payment Span
├── Database Span
└── Queue Publish Span
~~~

For each span, identify:

- operation
- service
- start/end time
- status
- important attributes

## 5. Map Events

Add operational events such as:

- deployment
- configuration change
- feature-flag change
- scaling event
- node restart
- dependency incident

Explain how events improve timeline correlation.

## 6. Correlation Identity

Decide where to use:

- request ID
- trace ID
- correlation/workflow ID

Explain why they are related but not universal synonyms.

## 7. Black Box vs White Box

Classify these signals:

- successful checkout ratio
- synthetic checkout probe
- database pool utilization
- payment dependency latency
- queue age
- API latency

Use:

~~~text
Black Box
White Box
Can Support Both Perspectives
~~~

## 8. Business Signals

Add business-level evidence:

- completed checkout count
- payment success rate
- order creation rate
- fulfillment acceptance rate

Explain why technical metrics can look healthy while business outcomes fail.

## 9. Missing-Telemetry Review

Assume:

~~~text
- no trace propagation
- no release markers
- unstructured logs
- metrics aggregated across all regions
~~~

Explain the investigation blind spots created by each gap.

## 10. Senior Engineer Connection

Use:

~~~text
User Journey
→ Metrics
→ Logs
→ Traces
→ Events
→ Context
→ Correlation
→ Hypothesis
~~~

## 11. SRE Connection

Connect the journey to:

- SLI
- user-impact signals
- alert context
- dependency telemetry
- recovery validation

## 12. Architect Connection

Ask:

- which context must be standardized?
- which identifiers must propagate?
- which signals should be retained longer?
- what sensitive data must never be emitted?
- what telemetry is mandatory before production launch?

## Validation Checklist

- [ ] Mapped metrics to the user journey
- [ ] Designed structured log fields
- [ ] Designed a conceptual distributed trace
- [ ] Added change/events to the timeline
- [ ] Defined correlation identities
- [ ] Distinguished black-box and white-box evidence
- [ ] Added business signals
- [ ] Identified telemetry blind spots

## Teach-Back

Explain:

> "Observability becomes useful when telemetry from the same user journey can be connected through context, identity, and time."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

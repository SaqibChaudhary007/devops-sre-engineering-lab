---
id: EXP-D00-031
domain: D00
topics:
  - D00-T018
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

# EXP-D00-031 — Slow Dependency, Retry Amplification, Backpressure, and Graceful Degradation

## Objective

Practice reasoning about slow dependencies, timeout boundaries, retries, overload, backpressure, load shedding, and graceful degradation without running disruptive tests.

## Safety

This is a conceptual experiment.

Do not generate traffic, overload dependencies, disable production services, or intentionally exhaust resources.

## Scenario

A checkout service depends synchronously on a payment API.

Normal behavior:

~~~text
Payment latency = 200 ms
Checkout latency = acceptable
Retry volume = low
~~~

Degraded behavior:

~~~text
Payment latency = 8 seconds
Checkout requests wait
Caller timeouts begin
Retries increase
Database connections remain occupied longer
Queue age rises
Users see slow or failed checkout
~~~

## 1. Identify the Failure Mode

Classify the payment dependency as:

- unavailable?
- slow?
- intermittent?
- partial?
- transient?
- unknown?

Explain what evidence is needed before choosing a response.

## 2. Define Timeout Boundaries

Map conceptual timeout layers:

~~~text
User / Client
→ API Gateway
→ Checkout Service
→ Payment Client
→ Payment Provider
~~~

Ask:

- which timeout is shortest?
- does an inner timeout exceed the outer budget?
- can work continue after the caller already gave up?

## 3. Model Retry Amplification

Assume multiple layers can retry.

Map:

~~~text
Client Retry
+ Gateway Retry
+ Service Retry
→ More Calls to Payment
~~~

Explain why retries at multiple layers can multiply work.

## 4. Classify Retry Eligibility

For each error type, choose:

~~~text
Retry Candidate
Do Not Retry
Retry Only with Idempotency / Operation Identity
Needs More Evidence
~~~

Examples:

- connection reset
- invalid request
- payment timeout with unknown completion status
- authentication failure
- rate-limit response

## 5. Add Backoff and Jitter

Design a conceptual retry policy with:

- bounded attempts
- backoff
- jitter
- timeout budget
- stop condition

Explain how this reduces synchronized retry pressure.

## 6. Add Backpressure

Model:

~~~text
Payment Saturated
→ Checkout Detects / Receives Signal
→ Admission Reduced
→ Less New Work
→ Dependency Has Recovery Space
~~~

Explain why upstream systems must respect the signal.

## 7. Add Load Shedding

Classify work as:

~~~text
Critical
Lower Priority
Optional
Deferrable
~~~

Decide what can be rejected or deferred during overload.

Explain why serving fewer requests can preserve useful service.

## 8. Design Graceful Degradation

Consider optional features:

- recommendations
- loyalty enrichment
- analytics event
- notification

Decide which can be skipped while preserving checkout correctness.

## 9. Fail-Fast Review

Ask:

- when is waiting no longer useful?
- when is the dependency known to be unhealthy?
- when should the system reject instead of waiting?

Explain the trade-off between early rejection and long resource occupancy.

## 10. Circuit-Breaker Preview

Conceptually model:

~~~text
Failure Threshold
→ Stop Some Calls
→ Recovery Window
→ Probe
→ Resume Carefully
~~~

Then answer:

- when would this help?
- when could it be unnecessary?
- what other isolation or queueing mechanisms may already exist?

## 11. Recovery Validation

Assume payment latency improves.

Do not declare recovery immediately.

Validate:

- checkout latency
- error rate
- retry volume
- queue age
- connection utilization
- successful payment outcome
- user-facing SLO

## 12. Senior Engineer Connection

Use:

~~~text
Failure Mode
→ Timeout Budget
→ Retry Policy
→ Backpressure
→ Degradation
→ Recovery Validation
~~~

## 13. SRE Connection

Connect:

- overload
- error budget
- graceful degradation
- retries
- SLOs
- saturation
- recovery

## 14. Architect Connection

Decide:

- which layer owns retries
- how timeout budgets compose
- where backpressure originates
- what functionality can degrade
- where isolation is needed
- what failure mode a circuit breaker would actually address

## Validation Checklist

- [ ] Classified the slow-dependency failure mode
- [ ] Mapped timeout boundaries
- [ ] Modeled multi-layer retry amplification
- [ ] Classified retry eligibility
- [ ] Designed bounded retry behavior
- [ ] Added backpressure
- [ ] Added load shedding
- [ ] Designed graceful degradation
- [ ] Reviewed fail-fast behavior
- [ ] Reviewed circuit-breaker applicability
- [ ] Defined recovery validation evidence

## Teach-Back

Explain:

> "A slow dependency can be more dangerous than a clean failure because it consumes resources while retries and waiting amplify load. Good failure handling bounds waiting, retries, admission, and degraded behavior."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

---
id: EXP-D00-029
domain: D00
topics:
  - D00-T017
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

# EXP-D00-029 — Feedback Loops, Delays, Retry Amplification, and Autoscaling

## Objective

Practice identifying reinforcing and balancing loops, delays, oscillation, retry amplification, and autoscaling behavior as system-level feedback.

## Safety

This is a conceptual modeling exercise.

Do not generate artificial traffic, trigger autoscaling in production, or intentionally overload any dependency.

## Scenario

A checkout system behaves like this:

~~~text
Traffic rises
→ Payment latency rises
→ Checkout requests time out
→ Clients retry
→ Payment traffic rises further
→ More requests time out
~~~

At the same time:

~~~text
CPU rises
→ Autoscaler observes high CPU
→ New replicas start
→ Startup takes time
→ CPU later falls
→ Scale-down begins
→ Traffic rises again
~~~

## 1. Identify the Reinforcing Loop

Model:

~~~text
Latency ↑
→ Timeouts ↑
→ Retries ↑
→ Load ↑
→ Latency ↑
~~~

Explain why this is reinforcing.

## 2. Identify the Balancing Loop

Model:

~~~text
Load ↑
→ Capacity Added
→ Load per Instance ↓
~~~

Explain why this is balancing in intent.

## 3. Add Delay

Add realistic delays:

- metric collection delay
- autoscaler evaluation interval
- scheduling delay
- container startup delay
- warm-up delay

Explain why delayed feedback can produce over-correction.

## 4. Model Oscillation

Use:

~~~text
High Load
→ Scale Up
→ Delayed Effect
→ Too Much Capacity
→ Scale Down
→ Delayed Effect
→ Too Little Capacity
→ Scale Up
~~~

Explain which settings or relationships could contribute.

## 5. Retry Amplification

Assume:

~~~text
1 original request
+ 3 retry layers
+ overlapping timeout windows
~~~

Do not calculate a universal production number.

Instead, explain how retries at multiple layers can multiply total work and hide the original bottleneck.

## 6. Add Backpressure

Redesign the system conceptually:

~~~text
Downstream Saturated
→ Signal / Reject / Slow Admission
→ Upstream Reduces Work
→ Queue Growth Slows
→ Dependency Recovers
~~~

Explain why backpressure works only if upstream components respect it.

## 7. Add Retry Bounds

Add:

- max attempts
- backoff
- jitter
- timeout budget
- retry eligibility
- stop condition

Explain how these can weaken the reinforcing loop.

## 8. Add Queue Evidence

Assume:

~~~text
Queue depth = stable
Oldest message age = rising
Consumer throughput = falling
~~~

Explain why the queue may still be unhealthy despite stable depth.

## 9. Autoscaling Signal Review

Compare these possible signals:

- CPU
- queue age
- request rate
- end-to-end latency
- dependency saturation

Explain why scaling on the wrong signal may not improve the real bottleneck.

## 10. Local vs Global Optimization

A team proposes:

~~~text
"Increase API replicas by 5x."
~~~

Explain:

- when this helps
- when it does nothing
- when it can worsen downstream overload

## 11. Stability Review

For the whole system, ask:

- what is the feedback signal?
- how delayed is it?
- how strong is the corrective action?
- what is the downstream constraint?
- what happens after correction?

## 12. Senior Engineer Connection

Use:

~~~text
Signal
→ Delay
→ Action
→ System Response
→ Feedback
→ Stability / Amplification
~~~

## 13. SRE Connection

Connect:

- retries
- autoscaling
- backpressure
- overload
- SLO impact
- graceful degradation

## 14. Architect Connection

Decide:

- where retries belong
- which layer should own backpressure
- what metric should drive scaling
- what delays must be modeled
- what guardrail reduces oscillation

## Validation Checklist

- [ ] Identified a reinforcing loop
- [ ] Identified a balancing loop
- [ ] Added realistic delays
- [ ] Explained oscillation
- [ ] Modeled retry amplification
- [ ] Added backpressure
- [ ] Added bounded retry behavior
- [ ] Interpreted queue evidence
- [ ] Reviewed autoscaling signals
- [ ] Compared local and global optimization
- [ ] Reviewed system stability

## Teach-Back

Explain:

> "Feedback loops, delays, and corrective actions can stabilize or destabilize a production system, so retries, autoscaling, and backpressure must be designed as interacting system behaviors."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

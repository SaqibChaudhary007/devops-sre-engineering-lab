---
id: EXP-D00-017
domain: D00
topics:
  - D00-T011
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

# EXP-D00-017 — Retry, Duplicate Work, Idempotency, and Retry Amplification

## Objective

Reason about safe retries, duplicate side effects, idempotency, exponential backoff, jitter, circuit breakers, and multi-layer retry amplification.

## Safety

This is a local reasoning exercise. No load generation, traffic flooding, production access, or live failure injection is required.

## Scenario

~~~text
Client
→ API Gateway
→ Order Service
→ Payment Service
~~~

Current retry policy:

~~~text
Client: up to 3 attempts
API Gateway: up to 3 attempts
Order Service: up to 3 attempts to Payment
~~~

The business operation is:

~~~text
Charge customer 100
~~~

## 1. Calculate Amplification

Work out the maximum number of downstream payment attempts that one original client request could produce if all layers exhaust their attempts.

Explain why small retry counts at multiple layers can multiply.

## 2. Safe vs Unsafe Retry

Classify each operation as Naturally Idempotent, Requires Idempotency Key, Usually Unsafe to Blindly Retry, or Context-Dependent:

- set profile status = ACTIVE
- charge card 100
- create shipment
- get product details
- reserve inventory
- delete a resource by stable identifier
- increment loyalty points by 100
- replace configuration with version 7

Explain the reasoning.

## 3. Duplicate Side Effect Scenario

~~~text
Attempt 1
→ Payment succeeds
→ Response lost

Caller
→ Times out
→ Retries

Attempt 2
→ Payment succeeds again
~~~

Explain the correctness failure.

Redesign conceptually:

~~~text
Logical Request ID
→ Payment service checks prior result
→ Existing result returned
→ Side effect not repeated
~~~

## 4. Retry Ownership

Compare:

~~~text
Model A
Every layer retries independently

Model B
One selected layer owns retries
Downstream layers return explicit failures
~~~

Discuss observability, amplification, latency, duplicate risk, and policy clarity.

## 5. Backoff

Compare immediate retries with a delayed sequence such as:

~~~text
1s
2s
4s
~~~

Explain why waiting can reduce pressure on a struggling dependency.

## 6. Jitter

Assume many clients all retry at identical intervals.

Explain how synchronized retry waves can overload a recovering dependency.

Then explain conceptually how jitter spreads retry attempts over time.

## 7. Retry Budget

Design a simple bounded retry policy.

Define:

- which layer owns retries
- maximum extra retry traffic
- when retries stop
- what metric shows retry pressure
- what happens when the dependency is clearly overloaded

## 8. Circuit Breaker Interaction

Model:

~~~text
Failures increase
→ retries continue within limits
→ circuit threshold reached
→ circuit opens
→ calls fail fast
→ dependency gets recovery time
→ probe later
~~~

Explain what the circuit breaker protects and what it does not repair.

## 9. Cascading Failure Loop

Analyze:

~~~text
Dependency slows
→ requests take longer
→ more work stays in flight
→ timeouts increase
→ retries increase
→ downstream load increases
→ dependency slows further
~~~

Identify where timeout policy, retry caps, backoff, jitter, circuit breaker, and load shedding can interrupt the loop.

## 10. Senior Engineer Connection

Use:

~~~text
Failure Type
→ Operation Semantics
→ Request Identity
→ Retry Owner
→ Retry Limit
→ Backoff / Jitter
→ Dependency State
→ Evidence
~~~

## 11. SRE Connection

Connect retry amplification to error rate, latency, saturation, queue depth, dependency health, and recovery time.

## 12. Architect Connection

Design principles:

- retries are bounded
- retry ownership is explicit
- unsafe side effects use request identity
- overload is not treated like simple packet loss
- retry traffic is measured separately from original traffic

## Validation Checklist

- [ ] Calculated retry amplification
- [ ] Classified retry-safe vs retry-unsafe operations
- [ ] Explained duplicate side effects
- [ ] Designed idempotency/request identity conceptually
- [ ] Compared retry ownership models
- [ ] Explained backoff and jitter
- [ ] Defined a retry budget
- [ ] Connected circuit breaker to retry policy
- [ ] Analyzed cascading failure

## Teach-Back

Explain: Retries are additional load. They are safe only when operation semantics, duplicate handling, retry ownership, and dependency health are understood.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

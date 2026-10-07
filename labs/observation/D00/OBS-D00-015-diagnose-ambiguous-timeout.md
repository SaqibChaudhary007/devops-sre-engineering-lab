---
id: OBS-D00-015
domain: D00
topics:
  - D00-T011
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# OBS-D00-015 — Diagnose an Ambiguous Timeout

## Objective

Build the mental habit of treating a timeout as **uncertainty**, not proof that a remote operation failed.

## Why This Matters

A caller can stop waiting without knowing whether the remote side never received the request, is still processing, completed the operation, completed it but lost the response, or became unreachable during the request.

## Safety

This is a local reasoning exercise only. No cloud account, production system, network manipulation, or destructive command is required.

## Scenario

~~~text
Checkout
→ Charge Request
→ Payment Service
~~~

The checkout service waits two seconds and records a timeout. The customer sees that payment status is unknown.

## 1. Enumerate Possible Realities

List at least five explanations for the timeout. For each, answer:

- did the business side effect occur?
- can the caller know for certain?
- is immediate retry safe?

Start with:

1. request never reached payment service
2. request reached payment service but processing is slow
3. charge succeeded but response was lost
4. payment service failed before the side effect
5. downstream provider is slow

## 2. Caller View vs Remote Reality

Complete:

| Caller observation | Possible remote reality | Certainty |
|---|---|---|
| Timeout | Request never arrived | ? |
| Timeout | Operation still running | ? |
| Timeout | Charge completed | ? |
| Timeout | Response lost | ? |
| Timeout | Remote process crashed | ? |

Explain why one caller symptom can map to several realities.

## 3. Retry Decision

Compare:

~~~text
A: Timeout → Retry immediately
B: Timeout → Retry with same logical request identity
C: Timeout → Query status / reconcile before another side effect
~~~

Discuss duplicate risk, user impact, latency, complexity, and operational safety.

## 4. Request Identity

Design a conceptual idempotency key such as:

~~~text
checkout-order-12345-payment-attempt
~~~

Explain how one logical identity can help detect repeated requests.

## 5. Evidence Timeline

Build a timeline:

~~~text
T0 Checkout sends request
T1 Payment service receives request
T2 Provider processes
T3 Payment service records result
T4 Response sent
T5 Caller timeout expires
~~~

Create three alternate timelines where the timeout occurs for different reasons.

## 6. Failure Classification

Classify each as Known Failure, Ambiguous Outcome, Transient Failure, Deterministic Failure, Dependency Failure, or Unknown:

- DNS lookup fails before request is sent
- connection cannot be established
- server returns explicit validation error
- caller times out with no response
- provider returns overload response
- response connection drops after remote commit

## 7. Troubleshooting Sequence

~~~text
Impact
→ Request Identity
→ Timeline
→ Caller Evidence
→ Remote Evidence
→ Dependency Evidence
→ Side-Effect State
→ Retry Decision
→ Reconciliation
~~~

Explain why this is stronger than starting with random commands.

## 8. Senior Engineer Connection

Ask what is unknown, whether the operation could already have succeeded, whether retry is safe, whether state can be reconciled first, and whether request identity exists.

## 9. SRE Connection

Connect ambiguous timeouts to error rate, latency, duplicate work, retry amplification, user-visible uncertainty, and incident correlation.

## 10. Architect Connection

Decide which operations need idempotency, status reconciliation, explicit retry ownership, and user-facing ambiguous-state handling.

## Validation Checklist

- [ ] Explained why timeout does not prove non-execution
- [ ] Distinguished caller observation from remote reality
- [ ] Evaluated retry safety
- [ ] Designed request identity
- [ ] Built multiple possible timelines
- [ ] Classified ambiguous vs known failures
- [ ] Used an evidence-first troubleshooting sequence

## Teach-Back

Explain: A timeout tells me the result did not arrive in time; it does not tell me whether the remote business operation happened.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

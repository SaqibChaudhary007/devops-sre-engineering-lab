---
id: DIA-D00-021
domain: D00
topic: D00-T004
title: Stateful vs Stateless Scaling
type: comparison-diagram
status: published
---

# DIA-D00-021 — Stateful vs Stateless Scaling

## Purpose

Explain why state placement affects replaceability, failover and horizontal scaling.

## Local Stateful Instances

~~~mermaid
flowchart TB
    U1[User] --> LB1[Load Balancer]
    LB1 --> A[Instance A<br/>Local Session]
    LB1 --> B[Instance B<br/>Different Local Session]
~~~

Potential problem:

~~~text
Request 1 → A
Request 2 → B
→ expected local state may be missing
~~~

## Stateless Application Tier with Shared State

~~~mermaid
flowchart TB
    U2[User] --> LB2[Load Balancer]
    LB2 --> C[Instance A]
    LB2 --> D[Instance B]
    C --> S[(Shared State Store)]
    D --> S
~~~

## Key Lesson

"Stateless instance" does not mean "the system has no state."

It means the application instance does not own unique local state required for future requests.

## Trade-Off

Externalizing state improves replaceability but adds a shared dependency whose:

- latency
- capacity
- availability
- security

must be designed.

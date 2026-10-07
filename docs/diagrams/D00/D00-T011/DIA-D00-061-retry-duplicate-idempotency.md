---
id: DIA-D00-061
domain: D00
topic: D00-T011
title: Retry Duplicate Idempotency Key
type: correctness-diagram
status: published
---

# DIA-D00-061 — Retry → Duplicate → Idempotency Key

## Purpose

Show how response loss can turn a retry into a duplicate business side effect, and how logical request identity can reduce that risk.

## Without Request Identity

~~~mermaid
flowchart LR
    C1[Caller] --> R1[Attempt 1]
    R1 --> S1[Charge Succeeds]
    S1 --> LOST[Response Lost]
    LOST --> T1[Caller Times Out]
    T1 --> R2[Attempt 2]
    R2 --> S2[Charge Succeeds Again]
    S2 --> DUP[Duplicate Business Effect]
~~~

## With Logical Request Identity

~~~mermaid
flowchart LR
    C2[Caller + Request ID] --> X1[Attempt 1]
    X1 --> STORE[Service Records Result by Request ID]
    STORE --> LOST2[Response Lost]
    LOST2 --> T2[Caller Times Out]
    T2 --> X2[Retry with Same Request ID]
    X2 --> LOOKUP[Find Existing Result]
    LOOKUP --> SAME[Return Existing Result]
~~~

## Key Lesson

Idempotency is about protecting the **business effect** of a repeated logical operation, not merely replaying network traffic.

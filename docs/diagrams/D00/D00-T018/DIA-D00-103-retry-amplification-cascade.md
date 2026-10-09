---
id: DIA-D00-103
domain: D00
topic: D00-T018
title: Dependency Failure Retry Saturation Cascading Failure
type: failure-propagation-diagram
status: published
---

# DIA-D00-103 — Dependency Failure → Retry → Saturation → Cascading Failure

## Purpose

Show how a degraded dependency can trigger reinforcing behavior that expands failure.

~~~mermaid
flowchart LR
    A[Dependency Slows / Fails] --> B[Requests Wait / Timeout]
    B --> C[Retries Increase]
    C --> D[Traffic / Work Amplifies]
    D --> E[Queues + Resource Saturation]
    E --> F[More Latency + Errors]
    F --> G[Cascading Failure]
    F --> C

    H[Backoff / Jitter / Retry Limits] -.Reduce amplification.-> C
    I[Load Shedding / Backpressure] -.Protect capacity.-> E
~~~

## Key Lesson

Retries can help with some transient failures, but uncontrolled retries can become a reinforcing loop that increases load and widens impact.

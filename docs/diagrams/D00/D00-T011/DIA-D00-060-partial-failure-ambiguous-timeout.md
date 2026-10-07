---
id: DIA-D00-060
domain: D00
topic: D00-T011
title: Partial Failure and Ambiguous Timeout
type: failure-diagram
status: published
---

# DIA-D00-060 — Partial Failure & Ambiguous Timeout

## Purpose

Show why one timeout can correspond to several different remote realities.

~~~mermaid
flowchart LR
    CALLER[Caller Sends Request] --> PATH{What Happened?}
    PATH --> A[Request Never Arrived]
    PATH --> B[Remote Still Processing]
    PATH --> C[Operation Completed]
    PATH --> D[Response Lost]
    PATH --> E[Remote / Dependency Failed]

    A --> TIMEOUT[Caller Sees Timeout]
    B --> TIMEOUT
    C --> TIMEOUT
    D --> TIMEOUT
    E --> TIMEOUT
~~~

## Key Lesson

~~~text
Timeout
≠
Proof of Non-Execution
~~~

A timeout tells the caller that the result did not arrive within the deadline.

It does not, by itself, reveal the remote-side truth.

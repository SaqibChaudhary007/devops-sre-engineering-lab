---
id: DIA-D00-099
domain: D00
topic: D00-T017
title: Dependency Chain Cascading Failure Blast Radius
type: cascading-failure-diagram
status: published
---

# DIA-D00-099 — Dependency Chain → Cascading Failure → Blast Radius

## Purpose

Show how one degraded dependency can propagate through technical and human parts of a system.

~~~mermaid
flowchart LR
    DEP[Dependency Slows] --> APP[Application Latency]
    APP --> RETRY[Retries Increase]
    RETRY --> DB[Shared Resource Pressure]
    DB --> QUEUE[Queue Delay]
    QUEUE --> ERR[Errors / User Impact]
    ERR --> ALERT[Alert Volume]
    ALERT --> HUMAN[On-Call Cognitive Load]
    HUMAN --> SLOW[Slower Response]
    SLOW --> ERR
~~~

## Shared Failure-Domain Check

~~~text
Two Replicas
+ Same Database
+ Same Region
+ Same Credential
+ Same Pipeline
→ May Still Share One Effective Failure Domain
~~~

## Key Lesson

Cascading failure is often produced by interacting conditions, shared dependencies, and feedback loops rather than one isolated component failure.

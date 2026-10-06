---
id: DIA-D00-022
domain: D00
topic: D00-T004
title: Request Path and Failure Propagation
type: troubleshooting-diagram
status: published
---

# DIA-D00-022 — Request Path & Failure Propagation

## Purpose

Connect architecture directly to production troubleshooting.

~~~mermaid
flowchart LR
    U[User] --> LB[Load Balancer]
    LB --> APP[Application]
    APP --> CACHE[(Cache)]
    APP --> DB[(Database)]
    APP --> PAY[External Payment API]

    DB -. high latency .-> APP
    PAY -. slow / timeout .-> APP
    APP -. waiting / queueing .-> LB
    LB -. slow responses .-> U
~~~

## Failure Propagation Example

~~~text
Database slows
      ↓
Application waits
      ↓
Workers remain occupied
      ↓
Requests queue
      ↓
End-to-end latency rises
      ↓
Users report "website slow"
~~~

## Important Lesson

> The component showing the symptom may not be the root cause.

## Senior Engineer Questions

For each hop:

- what can fail?
- what can be slow?
- what changed?
- what evidence exists?
- what is the next dependency?
- where does state live?

## SRE Questions

- which SLI is affected?
- where is latency accumulating?
- is there saturation?
- is failure propagating?
- can the system degrade gracefully?

## Architect Question

How should boundaries, timeouts, async paths, caches and failure isolation be designed so one slow dependency does not unnecessarily take down the whole user journey?

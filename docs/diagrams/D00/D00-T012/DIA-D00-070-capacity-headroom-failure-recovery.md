---
id: DIA-D00-070
domain: D00
topic: D00-T012
title: Capacity Headroom Failure Failover Degradation
type: capacity-reliability-diagram
status: published
---

# DIA-D00-070 — Capacity Headroom → Failure → Failover / Degradation

## Purpose

Show why spare capacity is part of recovery design.

~~~mermaid
flowchart LR
    NORMAL[Normal Load<br/>Uses Part of Safe Capacity] --> FAIL[Node / Dependency Failure]
    FAIL --> LESS[Less Available Capacity]
    LESS --> CHECK{Enough Headroom?}

    CHECK -->|Yes| MOVE[Failover / Reschedule / Redistribute]
    MOVE --> STABLE[Service Remains Acceptable]

    CHECK -->|No| SAT[Saturation]
    SAT --> LAT[Latency / Errors / Retries]
    LAT --> CHOICE{Protection Available?}
    CHOICE -->|Yes| DEG[Load Shed / Degrade / Backpressure]
    DEG --> CORE[Preserve Critical Service]
    CHOICE -->|No| OUT[Wider Outage]
~~~

## Reliability Lesson

Headroom supports:

- failover
- rescheduling
- traffic spikes
- retry load
- maintenance
- recovery

## Key Lesson

Redundancy without enough spare capacity may not be recoverable under real load.

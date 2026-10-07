---
id: DIA-D00-056
domain: D00
topic: D00-T010
title: Desired Replicas Scheduler Nodes Reconciliation
type: control-loop-diagram
status: published
---

# DIA-D00-056 — Desired Replicas → Scheduler → Nodes → Reconciliation

## Purpose

Show the orchestration control loop from desired replicas to placement and recovery.

~~~mermaid
flowchart LR
    DESIRED[Desired State<br/>Replicas = 4] --> CTRL[Controller / Reconciliation]
    OBS[Observed State<br/>Replicas = 3] --> CTRL
    CTRL --> NEED[Replacement Needed]
    NEED --> SCHED[Scheduler]
    SCHED --> CAP{Suitable Node?}
    CAP -->|Yes| NODE[Node]
    NODE --> RUN[New Workload Instance]
    RUN --> OBS2[Observed State Moves Toward 4]
    CAP -->|No| PENDING[Pending / Unschedulable]
~~~

## Key Lesson

Reconciliation can be working correctly even when desired state cannot be reached.

Capacity, constraints, image availability, networking, storage, policy, and dependencies still matter.

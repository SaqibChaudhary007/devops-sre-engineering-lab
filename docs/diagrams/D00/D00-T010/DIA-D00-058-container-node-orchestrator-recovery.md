---
id: DIA-D00-058
domain: D00
topic: D00-T010
title: Container Failure vs Node Failure vs Orchestrator Recovery
type: failure-recovery-diagram
status: published
---

# DIA-D00-058 — Container Failure vs Node Failure vs Orchestrator Recovery

## Purpose

Compare failure blast radius and show the limits of orchestrator recovery.

~~~mermaid
flowchart TB
    CFAIL[Container / Process Failure] --> ONE[One Workload Instance Affected]
    NFAIL[Node Failure] --> MANY[Multiple Workload Instances Affected]

    ONE --> CTRL1[Controller Detects Difference]
    MANY --> CTRL2[Controller Detects Larger Difference]

    CTRL1 --> REC1[Restart / Replace]
    CTRL2 --> SCHED[Reschedule Replacements]

    REC1 --> CHECK1{Dependencies Healthy?}
    SCHED --> CAP{Capacity + Storage + Network Available?}

    CHECK1 -->|Yes| REST1[Service Restored]
    CHECK1 -->|No| EXT1[Application / Dependency Fix Needed]

    CAP -->|Yes| REST2[Replacement Workloads Start]
    CAP -->|No| EXT2[Recovery Blocked / Human or Platform Action Needed]
~~~

## Blast Radius

~~~text
Single container failure
→ usually one instance

Node failure
→ potentially many instances together

Shared platform / control-plane failure
→ potentially broader impact
~~~

## Key Lesson

Self-healing means automated restoration **within defined platform capabilities**.

It does not remove the need for capacity, healthy dependencies, storage, networking, correct configuration, and a functioning control plane.

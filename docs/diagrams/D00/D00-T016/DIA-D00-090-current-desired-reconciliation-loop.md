---
id: DIA-D00-090
domain: D00
topic: D00-T016
title: Current State Desired State Reconciliation Loop
type: control-loop-diagram
status: published
---

# DIA-D00-090 — Current State ↔ Desired State → Reconciliation Loop

## Purpose

Show reconciliation as an iterative control loop that repeatedly compares actual state with intended state.

~~~mermaid
flowchart LR
    DESIRED[Desired State] --> COMPARE[Compare]
    CURRENT[Observed Current State] --> COMPARE
    COMPARE --> MATCH{Match?}
    MATCH -->|Yes| WAIT[Observe Again Later]
    MATCH -->|No| DECIDE[Decide Bounded Change]
    DECIDE --> ACT[Act]
    ACT --> MEASURE[Measure / Re-read State]
    MEASURE --> CURRENT
    WAIT --> CURRENT
~~~

## Key Lesson

~~~text
Observe
→ Compare
→ Act
→ Observe Again
~~~

Reconciliation is iterative and can operate with delayed or stale observations.

It is a control-system pattern, not a Kubernetes-only concept.

---
id: DIA-D00-101
domain: D00
topic: D00-T018
title: Fault Error Failure Impact Detection Recovery
type: failure-lifecycle-diagram
status: published
---

# DIA-D00-101 — Fault → Error → Failure → Impact → Detection → Recovery

## Purpose

Show a foundation-level chain from an initiating condition to visible impact and recovery.

~~~mermaid
flowchart LR
    A[Assumption / Expected Condition] --> B[Fault / Stressor]
    B --> C[Error / Degraded State]
    C --> D[Failure Mode]
    D --> E[User / System Impact]
    E --> F[Detection]
    F --> G[Containment]
    G --> H[Recovery]
    H --> I[Validation]
    I --> J[Learning]
~~~

## Key Lesson

A fault does not automatically equal user-visible failure. Failure thinking follows the path from changed conditions to impact, then asks how the system detects, contains, recovers and learns.

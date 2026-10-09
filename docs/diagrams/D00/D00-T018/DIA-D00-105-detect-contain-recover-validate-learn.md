---
id: DIA-D00-105
domain: D00
topic: D00-T018
title: Detect Contain Recover Validate Learn
type: recovery-loop-diagram
status: published
---

# DIA-D00-105 — Detect → Contain → Recover → Validate → Learn

## Purpose

Show the operational sequence for reducing impact and proving recovery.

~~~mermaid
flowchart LR
    A[Impact / Symptom] --> B[Detect]
    B --> C[Scope + Evidence]
    C --> D[Contain]
    D --> E[Recover]
    E --> F[Validate End-to-End]
    F --> G{Healthy?}
    G -- No --> C
    G -- Yes --> H[Learn / Improve]
    H --> I[Prevention + Better Detection + Safer Recovery]
~~~

## Key Lesson

During active impact, containment can be more urgent than perfect root-cause certainty. Recovery is not complete until the user and system outcomes are validated.

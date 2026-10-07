---
id: DIA-D00-074
domain: D00
topic: D00-T013
title: Toil Automation Engineering Capacity
type: engineering-capacity-diagram
status: published
---

# DIA-D00-074 — Toil → Automation → Engineering Capacity

## Purpose

Show how recurring operational work can consume engineering capacity and how carefully designed automation can reduce that load.

~~~mermaid
flowchart LR
    GROWTH[Service Growth] --> MANUAL[Repeated Manual Work]
    MANUAL --> TOIL[Toil Increases]
    TOIL --> LESS[Less Engineering Capacity]
    TOIL --> REVIEW{Understood + Safe to Automate?}
    REVIEW -->|Yes| AUTO[Build Automation]
    AUTO --> OBS[Observe + Validate]
    OBS --> REDUCE[Reduce Repetition]
    REDUCE --> MORE[More Engineering Capacity]
    REVIEW -->|No| HUMAN[Keep Human Judgment / Improve Process First]
~~~

## Toil Characteristics

~~~text
Manual
Repetitive
Automatable
Tactical
Limited Enduring Value
Scales with Service Growth
~~~

## Key Lesson

Automation should follow understanding.

Unsafe automation can increase blast radius instead of reducing toil.

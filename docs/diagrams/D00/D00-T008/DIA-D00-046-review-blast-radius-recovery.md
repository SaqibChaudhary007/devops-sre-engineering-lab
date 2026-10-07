---
id: DIA-D00-046
domain: D00
topic: D00-T008
title: IaC Change Risk Review Blast Radius Recovery
type: risk-diagram
status: published
---

# DIA-D00-046 — IaC Change Risk: Review → Blast Radius → Recovery

## Purpose

Show the production reasoning required before approving infrastructure change.

~~~mermaid
flowchart LR
    INTENT[Change Intent] --> PLAN[Plan / Preview]
    PLAN --> REVIEW[Review]
    REVIEW --> RISK[Risk Analysis]

    RISK --> SEC[Security]
    RISK --> DATA[Data]
    RISK --> COST[Cost]
    RISK --> DEP[Dependencies]
    RISK --> BR[Blast Radius]

    BR --> APPLY[Apply]
    APPLY --> OBS[Observe]
    OBS --> DECIDE{Healthy?}
    DECIDE -->|Yes| DONE[Continue]
    DECIDE -->|No| RECOVER[Rollback / Roll Forward / Failover / Restore]
~~~

## Review Questions

- what is created, updated, replaced, or deleted?
- what can fail?
- what becomes public?
- what gets more expensive?
- what data can be lost?
- what depends on this resource?
- how do we recover?

## Key Lesson

A syntactically valid infrastructure change is not automatically operationally safe.

Recovery must be designed before apply.

---
id: DIA-D00-033
domain: D00
topic: D00-T006
title: Elasticity and Autoscaling Loop
type: scaling-diagram
status: published
---

# DIA-D00-033 — Elasticity & Autoscaling Loop

## Purpose

Show how cloud capacity can adapt to demand—and where scaling can fail.

~~~mermaid
flowchart LR
    TRAFFIC[Demand / Traffic] --> METRIC[Metric / Signal]
    METRIC --> POLICY[Autoscaling Policy]
    POLICY --> SCALE[Add / Remove Capacity]
    SCALE --> APP[Application Tier]
    APP --> OBS[Observed Performance]
    OBS --> METRIC
~~~

## Constraints Around the Loop

~~~mermaid
flowchart TB
    QUOTA[Quota / Limit] --> SCALE2[Scaling Decision]
    COST[Budget / Cost] --> SCALE2
    STATE[State Model] --> SCALE2
    DB[Database Capacity] --> SCALE2
    ZONE[Failure-Domain Capacity] --> SCALE2
~~~

## Key Lesson

Autoscaling is not magic.

It only works when:

- signals are meaningful
- the tier can scale
- state allows scaling
- quotas allow growth
- dependencies can absorb load
- cost is acceptable

## Architecture Connection

~~~text
Scalability
→ can capacity increase?

Elasticity
→ can capacity adjust with demand?
~~~

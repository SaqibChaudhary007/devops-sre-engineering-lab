---
id: DIA-D00-075
domain: D00
topic: D00-T013
title: Error Budget Change Velocity Reliability Trade-Off
type: risk-tradeoff-diagram
status: published
---

# DIA-D00-075 — Error Budget → Change Velocity / Reliability Trade-Off

## Purpose

Show error-budget thinking as a shared mechanism for balancing product change and service reliability.

~~~mermaid
flowchart TB
    SLO[SLO] --> EB[Error Budget]
    EB --> STATE{Budget State}

    STATE -->|Healthy| NORMAL[Normal Controlled Delivery]
    STATE -->|Burning Fast| CAUTION[Increase Caution<br/>Investigate Reliability]
    STATE -->|Near / Beyond Policy Threshold| POLICY[Apply Explicit Team Policy]

    NORMAL --> CHANGE[Product Change]
    CAUTION --> REL[Prioritize Reliability Work]
    POLICY --> DECISION[Risk / Release Decision]
~~~

## Key Lesson

~~~text
SRE Goal
≠ Zero Change

SRE Goal
= Safe, Sustainable Velocity
~~~

The exact action at each budget state is organizational policy, not a universal standard.

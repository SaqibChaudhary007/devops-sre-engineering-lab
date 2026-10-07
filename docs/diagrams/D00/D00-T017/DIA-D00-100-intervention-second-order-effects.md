---
id: DIA-D00-100
domain: D00
topic: D00-T017
title: Intervention First Order Second Order New State
type: intervention-effects-diagram
status: published
---

# DIA-D00-100 — Intervention → First-Order Effect → Second-Order Effect → New System State

## Purpose

Show why architecture changes should be evaluated beyond their immediate intended benefit.

~~~mermaid
flowchart LR
    PROB[Observed Problem] --> INT[Architecture Intervention]
    INT --> FIRST[First-Order Effect]
    FIRST --> BEHAV[Changed System Behavior]
    BEHAV --> SECOND[Second-Order Effect]
    SECOND --> NEW[New System State]
    NEW --> MEASURE[Measure Again]
    MEASURE --> NEXT{New Bottleneck / Risk?}
    NEXT -->|Yes| REVIEW[Re-evaluate System]
    NEXT -->|No| STABLE[Accept / Continue Monitoring]
~~~

## Example

~~~text
Add Cache
→ Database Load Decreases
→ Traffic Capacity Increases
→ Downstream Payment Load Increases
→ New Bottleneck May Appear
~~~

## Key Lesson

Architecture is an intervention in a dynamic system.

Successful first-order effects can create new constraints, risks, or opportunities elsewhere.

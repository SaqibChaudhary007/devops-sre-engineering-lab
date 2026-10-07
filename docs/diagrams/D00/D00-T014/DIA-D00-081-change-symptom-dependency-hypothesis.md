---
id: DIA-D00-081
domain: D00
topic: D00-T014
title: Change Marker Symptom Dependency Root-Cause Hypothesis
type: incident-correlation-diagram
status: published
---

# DIA-D00-081 — Change Marker → Symptom → Dependency → Root-Cause Hypothesis

## Purpose

Show how observability evidence narrows an incident investigation without confusing correlation with proof.

~~~mermaid
flowchart LR
    IMPACT[User Symptom] --> TIME[Build Timeline]
    TIME --> CHANGE[Change Markers]
    TIME --> SERVICE[Service Signals]
    TIME --> DEP[Dependency Signals]
    TIME --> RES[Resource Signals]

    CHANGE --> HYP[Ranked Hypotheses]
    SERVICE --> HYP
    DEP --> HYP
    RES --> HYP

    HYP --> CHECK[Safe Validation]
    CHECK --> CONFIRM{Evidence Supports?}
    CONFIRM -->|Yes| ACTION[Mitigate / Correct]
    CONFIRM -->|No| NEXT[Refine Hypothesis]
    NEXT --> HYP
~~~

## Key Lesson

~~~text
Correlation
→ hypothesis

Validation
→ confidence
~~~

A deployment marker and an error spike occurring together do not, by themselves, prove causation.

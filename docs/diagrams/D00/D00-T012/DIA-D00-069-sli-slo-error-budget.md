---
id: DIA-D00-069
domain: D00
topic: D00-T012
title: SLI SLO Error Budget Mental Model
type: service-level-diagram
status: published
---

# DIA-D00-069 — SLI → SLO → Error Budget Mental Model

## Purpose

Separate measured service behavior, reliability targets, and allowed unreliability.

~~~mermaid
flowchart LR
    USER[Important User Journey] --> SLI[SLI<br/>Measured Service Behavior]
    SLI --> SLO[SLO<br/>Target for the SLI]
    SLO --> EB[Error Budget<br/>Allowed Unreliability]
    EB --> DECIDE[Operational / Change Decisions]
~~~

## Example

~~~text
SLI
→ successful checkout ratio

SLO
→ 99.9% successful checkout over a defined window

Error Budget
→ allowed unreliability implied by that SLO
~~~

## Key Lesson

SLI, SLO, SLA, and error budget are related but not interchangeable.

The purpose of an error budget is to inform decisions about risk, change, and reliability work.

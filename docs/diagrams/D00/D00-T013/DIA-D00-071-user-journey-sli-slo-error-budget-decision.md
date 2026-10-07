---
id: DIA-D00-071
domain: D00
topic: D00-T013
title: User Journey SLI SLO Error Budget Decision
type: service-level-diagram
status: published
---

# DIA-D00-071 — User Journey → SLI → SLO → Error Budget → Decision

## Purpose

Show how SRE turns a user need into a measurable reliability objective and then into an operational decision signal.

~~~mermaid
flowchart LR
    U[Important User Journey] --> G[Define Good Event]
    G --> SLI[SLI<br/>Measured Behavior]
    SLI --> SLO[SLO<br/>Target]
    SLO --> EB[Error Budget<br/>Allowed Unreliability]
    EB --> DECIDE{Reliability State}
    DECIDE --> HEALTHY[Healthy<br/>Normal Controlled Change]
    DECIDE --> RISK[Budget Burning Too Fast<br/>Reduce Avoidable Risk / Improve Reliability]
~~~

## Key Lesson

~~~text
User Need
→ Measurement
→ Objective
→ Risk Signal
→ Engineering Decision
~~~

Error-budget response depends on explicit organizational policy rather than one universal freeze rule.

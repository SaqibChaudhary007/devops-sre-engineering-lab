---
id: DIA-D00-082
domain: D00
topic: D00-T014
title: Cardinality Sampling Retention Cost Trade-Off
type: observability-economics-diagram
status: published
---

# DIA-D00-082 — Cardinality / Sampling / Retention / Cost Trade-Off

## Purpose

Show the main economics and governance trade-offs behind observability design.

~~~mermaid
flowchart TB
    NEED[Operational Need] --> CONTEXT[More Context / Detail]
    CONTEXT --> CARD[Higher Cardinality]
    CONTEXT --> VOLUME[More Telemetry Volume]

    CARD --> COST[More Storage / Memory / Query Cost]
    VOLUME --> COST

    VOLUME --> SAMPLE{Sampling?}
    SAMPLE -->|More Sampling| LESS[Lower Cost / Less Complete Evidence]
    SAMPLE -->|Less Sampling| MORE[More Complete Evidence / Higher Cost]

    NEED --> RET[Retention Decision]
    RET --> LONG[Longer Retention<br/>More History / More Cost / More Governance]
    RET --> SHORT[Shorter Retention<br/>Lower Cost / Less History]

    COST --> DECIDE[Architecture Trade-Off]
    LESS --> DECIDE
    MORE --> DECIDE
    LONG --> DECIDE
    SHORT --> DECIDE
~~~

## Additional Constraints

~~~text
Diagnostic Value
+ Security / Privacy
+ Runtime Overhead
+ Cost
+ Retention
+ Sampling
+ Cardinality
→ Observability Architecture Decision
~~~

## Key Lesson

More telemetry is not automatically better observability.

The goal is enough trustworthy evidence to operate the service effectively at an acceptable cost and risk.

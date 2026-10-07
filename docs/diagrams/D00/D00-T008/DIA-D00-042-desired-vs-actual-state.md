---
id: DIA-D00-042
domain: D00
topic: D00-T008
title: Desired State vs Actual State
type: state-model-diagram
status: published
---

# DIA-D00-042 — Desired State vs Actual State

## Purpose

Show the difference between intended infrastructure and runtime reality.

~~~mermaid
flowchart LR
    DESIRED[Desired State<br/>What should exist] --> COMPARE[Compare / Evaluate]
    ACTUAL[Actual State<br/>What does exist] --> COMPARE
    COMPARE --> DIFF{Difference?}
    DIFF -->|No| STABLE[No managed change]
    DIFF -->|Yes| ACTION[Plan / Reconcile / Investigate]
~~~

## Drift Example

~~~text
Desired:
HTTPS only

Actual:
HTTPS + public SSH
~~~

The mismatch is drift.

## Key Lesson

The repository expresses intent.

The platform expresses current reality.

During troubleshooting and change review, engineers need both.

---
id: DIA-D00-098
domain: D00
topic: D00-T017
title: Local Optimization vs Global Outcome
type: optimization-tradeoff-diagram
status: published
---

# DIA-D00-098 — Local Optimization vs Global Outcome

## Purpose

Show why improving one component does not guarantee improvement of the end-to-end system.

~~~mermaid
flowchart LR
    USER[User Demand] --> API[API]
    API --> DB[Database]
    DB --> QUEUE[Queue]
    QUEUE --> WORKER[Worker]
    WORKER --> OUT[Completed Outcome]

    API -. Local Optimization: Faster API .-> MORE[More Downstream Work]
    MORE --> DB
    DB --> SAT[Database Saturation]
    SAT --> LAT[End-to-End Latency Rises]
    LAT --> OUT
~~~

## Key Lesson

~~~text
Local Improvement
≠
Global Improvement
~~~

The active bottleneck and full flow must be re-measured after an intervention because constraints can migrate.

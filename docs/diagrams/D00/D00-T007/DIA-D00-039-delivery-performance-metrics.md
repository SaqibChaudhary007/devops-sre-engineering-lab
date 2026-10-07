---
id: DIA-D00-039
domain: D00
topic: D00-T007
title: Delivery Performance Throughput Instability Recovery
type: metrics-diagram
status: published
---

# DIA-D00-039 — Delivery Performance: Throughput, Instability & Recovery

## Purpose

Visualize the current DORA five-metric model used in D00-T007.

~~~mermaid
flowchart TB
    PERF[Software Delivery Performance]

    PERF --> THR[Throughput]
    PERF --> INST[Instability]

    THR --> LT[Change Lead Time]
    THR --> DF[Deployment Frequency]
    THR --> FDRT[Failed Deployment Recovery Time]

    INST --> CFR[Change Fail Rate]
    INST --> RWR[Deployment Rework Rate]
~~~

## Historical Context

DORA was widely taught using four key metrics.

The current model adds **deployment rework rate** and uses **failed deployment recovery time** rather than the older broader MTTR/time-to-restore wording.

## Interpretation Rule

~~~text
Metric
→ evidence about the delivery system

Metric
≠ business objective by itself
~~~

## Anti-Gaming Examples

~~~text
Max deployment frequency
→ may create meaningless deployments

Drive change fail rate to zero
→ may create giant approval queues

Minimize lead time at all costs
→ may reduce validation quality
~~~

## Key Lesson

Use the metrics together to understand flow and instability, not as isolated targets.

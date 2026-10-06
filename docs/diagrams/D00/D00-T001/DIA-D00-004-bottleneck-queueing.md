
---
id: DIA-D00-004
domain: D00
topic: D00-T001
title: Bottleneck and Queueing Mental Model
type: performance-diagram
status: published
---

# DIA-D00-004 — Bottleneck & Queueing Mental Model

## Purpose

Explain what happens when workload arrives faster than a component can process it.

~~~mermaid
flowchart LR
    W[Incoming Work<br/>100 units/s] --> Q[Queue]
    Q --> B[Bottleneck Component<br/>Processes 60 units/s]
    B --> O[Completed Work<br/>60 units/s]

    W -. 40 units/s accumulate .-> Q
~~~

## Progression

~~~mermaid
flowchart LR
    D[Demand exceeds capacity] --> Q[Queue grows]
    Q --> W[Waiting time grows]
    W --> L[Latency increases]
    L --> T[Timeouts / Poor User Experience]
~~~

## Core Relationship

~~~text
Arrival Rate > Processing Rate
        ↓
Queue Growth
        ↓
Higher Waiting Time
        ↓
Higher Latency
~~~

## Senior Engineer Question

Should you increase capacity immediately?

Not necessarily. First identify the real bottleneck and why demand exceeds effective processing capacity.

## SRE Connection

Queue depth may be an early signal, while user-facing latency or errors show the reliability consequence.

## Architect Connection

Possible solutions can include changing capacity, parallelism, workload shaping, caching, asynchronous processing or architecture—but each has trade-offs.

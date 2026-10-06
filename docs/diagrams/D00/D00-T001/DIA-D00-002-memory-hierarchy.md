
---
id: DIA-D00-002
domain: D00
topic: D00-T001
title: Memory and Storage Hierarchy
type: hierarchy-diagram
status: published
---

# DIA-D00-002 — Memory & Storage Hierarchy

## Purpose

Explain why computers use several storage/memory layers instead of one universal storage type.

~~~mermaid
flowchart TB
    R[Registers<br/>Tiny / Extremely Fast]
    L1[L1 Cache]
    L2[L2 Cache]
    L3[L3 Cache]
    RAM[RAM<br/>Active Working Memory]
    SSD[SSD / NVMe<br/>Persistent Storage]
    REM[Remote / External Storage<br/>Potentially Higher Latency]

    R --> L1 --> L2 --> L3 --> RAM --> SSD --> REM
~~~

## Mental Model

Moving downward generally means:

~~~text
Capacity tends to increase
Latency tends to increase
Cost per unit of fast access tends to decrease
~~~

This is a conceptual model. Real hardware designs vary.

## Key Lesson

The CPU cannot treat all data access as equally fast. Where data resides affects performance.

## Senior Engineer Question

Why might a workload spend little CPU time while still responding slowly?

Because it may be waiting on a slower layer such as RAM, storage, network or another dependency.

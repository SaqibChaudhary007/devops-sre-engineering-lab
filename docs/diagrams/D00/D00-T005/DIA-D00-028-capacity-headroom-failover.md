---
id: DIA-D00-028
domain: D00
topic: D00-T005
title: Capacity Headroom and Failover
type: capacity-diagram
status: published
---

# DIA-D00-028 — Capacity, Headroom & Failover

## Purpose

Show why normal utilization is not enough for resilience planning.

## Normal Operation

~~~mermaid
flowchart LR
    TRAFFIC[Traffic] --> A[Instance A<br/>~45% Load]
    TRAFFIC --> B[Instance B<br/>~45% Load]
~~~

Each instance has unused capacity.

~~~text
Capacity
= current workload
+ spare headroom
~~~

## After One Instance Fails

~~~mermaid
flowchart LR
    TRAFFIC2[Same Traffic] --> SURVIVOR[Instance B<br/>~90% Demand]
    FAILED[Instance A<br/>Unavailable]
~~~

The survivor may still work, but only if all critical dependencies also have enough headroom.

## Capacity Chain

~~~text
Application CPU
+ Memory
+ Network
+ Storage
+ Database
+ Connections
+ Downstream Services
= effective failover capacity
~~~

## Key Lesson

Low utilization during normal operation does not prove sufficient failover capacity.

## SRE Connection

Capacity planning must include:

- growth
- spikes
- failure reserve
- maintenance reserve
- dependency limits

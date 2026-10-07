---
id: DIA-D00-067
domain: D00
topic: D00-T012
title: Failure Domain Blast Radius Redundancy Placement
type: reliability-architecture-diagram
status: published
---

# DIA-D00-067 — Failure Domain → Blast Radius → Redundancy Placement

## Purpose

Show why replica count alone is weak reliability evidence unless replicas are placed across sufficiently independent failure domains.

## Correlated Placement

~~~mermaid
flowchart TB
    FD1[Failure Domain: Node / Zone A] --> R1[Replica 1]
    FD1 --> R2[Replica 2]
    FD1 --> R3[Replica 3]
    FD1 --> FAIL1[Shared Failure]
    FAIL1 --> ALL[All Replicas Affected]
~~~

## Independent Placement

~~~mermaid
flowchart TB
    A[Failure Domain A] --> X1[Replica 1]
    B[Failure Domain B] --> X2[Replica 2]
    C[Failure Domain C] --> X3[Replica 3]

    A --> F[Failure in A]
    F --> X1
    B --> SURVIVE[Other Replicas Remain]
    C --> SURVIVE
~~~

## Reliability Model

~~~text
Redundancy
+ Failure-Domain Independence
+ Capacity
+ Detection
+ Failover
→ Useful Resilience
~~~

## Key Lesson

More copies do not automatically mean more reliability.

The blast radius depends on what those copies share.

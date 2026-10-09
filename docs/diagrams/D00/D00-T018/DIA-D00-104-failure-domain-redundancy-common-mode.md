---
id: DIA-D00-104
domain: D00
topic: D00-T018
title: Failure Domain Redundancy Common Mode Failure Blast Radius
type: resilience-boundary-diagram
status: published
---

# DIA-D00-104 — Failure Domain → Redundancy → Common-Mode Failure → Blast Radius

## Purpose

Show why redundancy only improves resilience when replicas do not share the same critical failure conditions.

~~~mermaid
flowchart TB
    FD[Shared Failure Domain] --> A[Replica A]
    FD --> B[Replica B]

    A --> S[Service]
    B --> S

    X[Shared Dependency / Config / Credential / Capacity Constraint] --> A
    X --> B

    X --> C[Common-Mode Failure]
    C --> BR[Expanded Blast Radius]

    I1[Independent Failure Domain] --> C1[Replica C]
    I2[Independent Failure Domain] --> C2[Replica D]
    C1 --> R[Reduced Correlated Risk]
    C2 --> R
~~~

## Key Lesson

Two replicas are not automatically independent. Shared infrastructure, configuration, credentials, dependencies or capacity can cause both to fail together.

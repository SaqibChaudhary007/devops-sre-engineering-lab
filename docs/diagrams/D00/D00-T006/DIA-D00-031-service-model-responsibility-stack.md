---
id: DIA-D00-031
domain: D00
topic: D00-T006
title: IaaS vs PaaS vs SaaS Responsibility Stack
type: comparison-diagram
status: published
---

# DIA-D00-031 — IaaS vs PaaS vs SaaS Responsibility Stack

## Purpose

Show how responsibility shifts as abstraction increases.

~~~mermaid
flowchart LR
    subgraph I[IaaS]
        I1[Customer: OS / Runtime / App / Data / Config]
        I2[Provider: Physical / Virtualization]
    end

    subgraph P[PaaS]
        P1[Customer: App / Data / Config / Identity]
        P2[Provider: Runtime / OS / Physical Platform]
    end

    subgraph S[SaaS]
        S1[Customer: Users / Data Use / Config / Governance]
        S2[Provider: Application Platform / Runtime / Infrastructure]
    end
~~~

## Direction of Abstraction

~~~text
More customer-operated layers
IaaS
  ↓
PaaS
  ↓
SaaS
More provider-operated layers
~~~

## Important Lesson

Responsibility shifts.

It does not disappear.

Customers still retain responsibilities around:

- identity
- data
- configuration
- integrations
- governance
- business usage

Exact boundaries vary by service.

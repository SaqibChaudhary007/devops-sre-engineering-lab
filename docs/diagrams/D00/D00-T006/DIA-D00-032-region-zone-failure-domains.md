---
id: DIA-D00-032
domain: D00
topic: D00-T006
title: Region Zone Resource Failure Domains
type: reliability-diagram
status: published
---

# DIA-D00-032 — Region / Zone / Resource Failure Domains

## Purpose

Show how cloud resources are placed within provider-defined failure boundaries.

~~~mermaid
flowchart TB
    PROVIDER[Cloud Provider]
    PROVIDER --> REGION[Region]

    REGION --> ZA[Zone A]
    REGION --> ZB[Zone B]

    ZA --> A1[App Instance A1]
    ZA --> A2[App Instance A2]
    ZB --> B1[App Instance B1]
    ZB --> B2[App Instance B2]

    A1 --> DB[(Shared / Managed Dependency)]
    A2 --> DB
    B1 --> DB
    B2 --> DB
~~~

## Questions to Ask

~~~text
Are redundant instances in different hosts?
Different zones?
Is state replicated?
Is the database also zone-resilient?
Can remaining capacity handle failure?
~~~

## Key Lesson

Multiple instances reduce only the failure risks they are actually separated from.

## Important Nuance

Provider definitions and guarantees for regions/zones differ.

Multi-zone also does not automatically equal disaster recovery.

---
id: DIA-D00-034
domain: D00
topic: D00-T006
title: Cloud Responsibility Cost Governance Triangle
type: architecture-tradeoff-diagram
status: published
---

# DIA-D00-034 — Cloud Responsibility / Cost / Governance Triangle

## Purpose

Show why cloud architecture is not only a technical scaling decision.

~~~mermaid
flowchart TB
    ARCH[Cloud Architecture]
    ARCH --> RESP[Responsibility]
    ARCH --> COST[Cost]
    ARCH --> GOV[Governance]

    RESP --> ID[Identity / Data / Configuration]
    COST --> USE[Usage / Scale / Transfer / Managed Services]
    GOV --> POLICY[Policy / Quotas / Tags / Review]
~~~

## Responsibility Questions

- who operates the infrastructure layer?
- who owns data?
- who configures identity?
- who handles application recovery?

## Cost Questions

- what scales with demand?
- what is always on?
- what is replicated?
- what grows across regions/zones?

## Governance Questions

- who may create resources?
- which regions/services are allowed?
- which quotas/budgets apply?
- how are ownership and criticality tagged?

## Key Lesson

Cloud speed is safe only when responsibility, cost, and governance evolve with it.

## Architect Connection

The technically possible design is not always the operationally sustainable design.

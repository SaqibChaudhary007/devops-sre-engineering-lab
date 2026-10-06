---
id: DIA-D00-019
domain: D00
topic: D00-T004
title: Monolith vs Microservices
type: comparison-diagram
status: published
---

# DIA-D00-019 — Monolith vs Microservices

## Purpose

Compare deployment boundaries without implying one architecture is universally better.

## Monolith

~~~mermaid
flowchart TB
    C1[Client] --> MONO[Single Deployable Application]
    MONO --> DB1[(Data Store)]

    subgraph MONOBOX[Inside Application]
        AUTH[Auth]
        ORD[Orders]
        INV[Inventory]
        PAY[Payments]
    end
~~~

## Microservices

~~~mermaid
flowchart TB
    C2[Client] --> ENTRY[Gateway / Entry Point]
    ENTRY --> AUTH2[Auth Service]
    ENTRY --> ORD2[Order Service]
    ENTRY --> INV2[Inventory Service]
    ORD2 --> PAY2[Payment Service]

    AUTH2 --> D1[(Auth Data)]
    ORD2 --> D2[(Order Data)]
    INV2 --> D3[(Inventory Data)]
    PAY2 --> D4[(Payment Data)]
~~~

## Trade-Off View

~~~text
Monolith
+ simpler operations
+ fewer remote calls
- broader deployment boundary

Microservices
+ independent deploy/scale boundaries
+ clearer service ownership when designed well
- network/distributed-system complexity
- more observability and operational burden
~~~

## Key Lesson

> Choose architecture from requirements and constraints, not trend or status.

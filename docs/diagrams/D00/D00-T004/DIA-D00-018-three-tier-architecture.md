---
id: DIA-D00-018
domain: D00
topic: D00-T004
title: Three-Tier Architecture
type: layered-architecture-diagram
status: published
---

# DIA-D00-018 — Three-Tier Architecture

## Purpose

Show separation between presentation, application logic and data responsibilities.

~~~mermaid
flowchart TB
    U[User]

    subgraph P[Presentation Tier]
        UI[Web / Mobile / UI]
    end

    subgraph A[Application Tier]
        API[API / Business Logic]
    end

    subgraph D[Data Tier]
        DB[(Database / Data Store)]
    end

    U --> UI
    UI --> API
    API --> DB
~~~

## Responsibility Model

~~~text
Presentation
→ interaction with user

Application
→ business rules / orchestration

Data
→ persistence / retrieval
~~~

## Why Separation Helps

It can improve:

- maintainability
- ownership
- scaling choices
- security boundaries
- troubleshooting clarity

## Trade-Off

More tiers also create more communication paths and failure points.

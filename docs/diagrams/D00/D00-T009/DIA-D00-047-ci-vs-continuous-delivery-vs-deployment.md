---
id: DIA-D00-047
domain: D00
topic: D00-T009
title: CI vs Continuous Delivery vs Continuous Deployment
type: comparison-diagram
status: published
---

# DIA-D00-047 — CI vs Continuous Delivery vs Continuous Deployment

## Purpose

Clarify the boundary between integration, releasability, and automatic production promotion.

~~~mermaid
flowchart LR
    CODE[Code Change] --> CI[Continuous Integration]
    CI --> BUILD[Build + Validate]
    BUILD --> CD[Continuous Delivery]
    CD --> READY[Releasable / Production-Ready]
    READY --> DECISION{Production Decision?}
    DECISION -->|Deliberate decision| PROD1[Production]
    DECISION -->|Automatic when conditions pass| PROD2[Continuous Deployment]
~~~

## Key Distinction

~~~text
CI
→ integrate and validate frequently

Continuous Delivery
→ keep software releasable through a repeatable process

Continuous Deployment
→ automatically promote validated change to production
~~~

## Important Nuance

Continuous delivery should be taught provider-neutrally.

Some systems use explicit approvals; others use different release controls.

The key concept is **releasability**, not one vendor's UI.

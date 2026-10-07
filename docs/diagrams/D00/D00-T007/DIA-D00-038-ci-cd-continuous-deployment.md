---
id: DIA-D00-038
domain: D00
topic: D00-T007
title: CI vs Continuous Delivery vs Continuous Deployment
type: comparison-diagram
status: published
---

# DIA-D00-038 — CI vs Continuous Delivery vs Continuous Deployment

## Purpose

Separate three concepts that are often collapsed into "CI/CD."

## Continuous Integration

~~~mermaid
flowchart LR
    CHANGE[Code Change] --> VCS[Version Control]
    VCS --> BUILD[Build]
    BUILD --> TEST[Test / Validate]
    TEST --> FEEDBACK[Fast Feedback]
~~~

Core idea:

> Integrate frequently and validate quickly.

## Continuous Delivery

~~~mermaid
flowchart LR
    CHANGE2[Change] --> BUILD2[Build]
    BUILD2 --> TEST2[Test]
    TEST2 --> PACKAGE[Package]
    PACKAGE --> READY[Production-Ready]
    READY --> DECISION[Explicit Production Decision]
~~~

Core idea:

> Keep software releasable through a reliable process.

## Continuous Deployment

~~~mermaid
flowchart LR
    CHANGE3[Change] --> VALIDATE[Required Validation]
    VALIDATE --> PROD[Automatic Production Deployment]
~~~

Core idea:

> Validated change can automatically reach production.

## Key Lesson

A pipeline product does not prove any of these practices are mature.

The outcomes are:

- frequent integration
- reliable validation
- repeatability
- safe promotion
- feedback
- recovery

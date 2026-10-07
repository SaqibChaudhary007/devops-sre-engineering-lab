---
id: DIA-D00-043
domain: D00
topic: D00-T008
title: Declarative vs Imperative
type: comparison-diagram
status: published
---

# DIA-D00-043 — Declarative vs Imperative

## Purpose

Distinguish two common infrastructure automation models without claiming one is universally superior.

## Declarative

~~~mermaid
flowchart LR
    INTENT[Describe Desired Result] --> ENGINE[Engine Determines Actions]
    ENGINE --> RESULT1[Target State]
~~~

Mental model:

> Describe **what** you want.

## Imperative

~~~mermaid
flowchart LR
    STEP1[Step 1] --> STEP2[Step 2]
    STEP2 --> STEP3[Step 3]
    STEP3 --> RESULT2[Result]
~~~

Mental model:

> Describe **how** to do it.

## Important Nuance

Real systems can combine both models.

Declarative intent can still be wrong.

Imperative automation can still be reliable when ordering and failure handling are designed carefully.

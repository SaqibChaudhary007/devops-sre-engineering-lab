---
id: DIA-D00-092
domain: D00
topic: D00-T016
title: Partial Failure Rollback Roll Forward Compensation
type: workflow-recovery-diagram
status: published
---

# DIA-D00-092 — Partial Failure → Rollback / Roll-Forward / Compensation

## Purpose

Show that multi-step automation can fail after some work has already succeeded and therefore needs explicit recovery reasoning.

~~~mermaid
flowchart LR
    START[Workflow Starts] --> A[Step A Succeeds]
    A --> B[Step B Succeeds]
    B --> C[Step C Fails]
    C --> STATE[Inspect Current State]
    STATE --> DECIDE{Safe Recovery Path?}

    DECIDE --> RB[Rollback]
    DECIDE --> RF[Roll-Forward]
    DECIDE --> COMP[Compensating Action]
    DECIDE --> MAN[Manual Reconciliation]

    RB --> VALIDATE[Validate Final State]
    RF --> VALIDATE
    COMP --> VALIDATE
    MAN --> VALIDATE
~~~

## Key Lesson

Rollback is not universal.

External side effects, incompatible data changes, or downstream state can make roll-forward or compensation safer than returning to an old state.

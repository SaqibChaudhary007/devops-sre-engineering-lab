---
id: DIA-D00-089
domain: D00
topic: D00-T016
title: Trigger Preconditions State Action Validation Feedback
type: automation-lifecycle-diagram
status: published
---

# DIA-D00-089 — Trigger → Preconditions → State → Action → Validation → Feedback

## Purpose

Show that automation should evaluate conditions and state before acting, then validate the actual outcome afterward.

~~~mermaid
flowchart LR
    T[Trigger] --> I[Intent]
    I --> P{Preconditions Met?}
    P -->|No| STOP[Stop / Escalate]
    P -->|Yes| S[Read Current State]
    S --> A[Bounded Action]
    A --> V[Validate Postconditions]
    V --> OK{Desired Outcome Achieved?}
    OK -->|Yes| F[Record Feedback / Audit]
    OK -->|No| R[Recover / Retry Policy / Escalate]
~~~

## Key Lesson

A trigger starts evaluation.

It does not prove that the action is safe.

Automation should validate the intended outcome rather than treating process completion alone as success.

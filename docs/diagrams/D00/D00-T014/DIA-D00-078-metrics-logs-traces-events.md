---
id: DIA-D00-078
domain: D00
topic: D00-T014
title: Metrics vs Logs vs Traces vs Events
type: signal-comparison-diagram
status: published
---

# DIA-D00-078 — Metrics vs Logs vs Traces vs Events

## Purpose

Show how major observability signals answer different questions and become stronger when correlated.

~~~mermaid
flowchart TB
    Q[Operational Question]

    Q --> M[Metrics<br/>How much? How often? Trending?]
    Q --> L[Logs<br/>What happened?]
    Q --> T[Traces<br/>Where did this request spend time?]
    Q --> E[Events<br/>What changed at this moment?]

    M --> C[Correlated Investigation]
    L --> C
    T --> C
    E --> C
~~~

## Mental Model

~~~text
Metrics
→ trends / rates / distributions

Logs
→ event detail

Traces
→ request path and latency

Events
→ change / occurrence timeline
~~~

## Key Lesson

No single signal answers every operational question.

The value increases when signals carry enough shared context to be correlated.

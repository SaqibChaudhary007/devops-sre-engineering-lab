---
id: DIA-D00-095
domain: D00
topic: D00-T017
title: System Boundary Components Relationships Flows Outcome
type: systems-context-diagram
status: published
---

# DIA-D00-095 — System Boundary → Components → Relationships → Flows → Outcome

## Purpose

Show that the behavior of a system comes from interactions among components inside a chosen boundary and from influences crossing that boundary.

~~~mermaid
flowchart LR
    ENV[Environment / External Influences] --> BOUNDARY

    subgraph BOUNDARY[Chosen System Boundary]
        A[Component A]
        B[Component B]
        C[Component C]
        A -->|Flow / Dependency| B
        B -->|Flow / Dependency| C
        C -->|Feedback| A
    end

    BOUNDARY --> OUT[System Outcome]
~~~

## Key Lesson

A boundary is selected for the question being analyzed.

A component can appear healthy while relationships among components still produce a poor end-to-end outcome.

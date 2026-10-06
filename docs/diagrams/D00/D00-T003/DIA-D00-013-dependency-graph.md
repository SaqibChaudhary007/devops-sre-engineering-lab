---
id: DIA-D00-013
domain: D00
topic: D00-T003
title: Dependency Graph
type: relationship-diagram
status: published
---

# DIA-D00-013 — Dependency Graph

## Purpose

Show that applications depend not only on direct libraries but also on transitive dependencies and runtime services.

~~~mermaid
flowchart TB
    APP[Application]

    APP --> A[Direct Library A]
    APP --> B[Direct Library B]

    A --> C[Transitive Library C]
    A --> D[Transitive Library D]
    B --> D
    B --> E[Transitive Library E]

    APP --> RT[Language Runtime]
    APP --> DB[Database Service]
    APP --> API[External API]
~~~

## Key Terms

**Direct dependency** — explicitly selected by the application/team.

**Transitive dependency** — pulled in because another dependency requires it.

**Runtime dependency** — something the application needs while executing.

## Key Lesson

> Your software can fail because of something your team did not directly write.

## Security Connection

Dependency graphs affect:

- vulnerability exposure
- patching
- provenance
- upgrade risk

## Senior Engineer Connection

When behavior changes unexpectedly, ask whether the source changed, a direct dependency changed, or a transitive/runtime dependency changed.

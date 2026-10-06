# D00-T003 Visual / Diagram Package — Software Engineering Foundations

This package provides reusable diagrams for **00.03 — Software Engineering Foundations**.

## Diagram Set

1. [DIA-D00-011 — Source to Process Lifecycle](DIA-D00-011-source-to-process-lifecycle.md)
2. [DIA-D00-012 — Compiler vs Runtime-Driven Execution](DIA-D00-012-compiler-vs-runtime.md)
3. [DIA-D00-013 — Dependency Graph](DIA-D00-013-dependency-graph.md)
4. [DIA-D00-014 — Build-Time vs Runtime Dependencies](DIA-D00-014-buildtime-vs-runtime-dependencies.md)
5. [DIA-D00-015 — Build Once, Promote the Artifact](DIA-D00-015-build-once-promote.md)
6. [DIA-D00-016 — Build vs Startup vs Runtime Failure](DIA-D00-016-failure-stage-model.md)

## Learning Progression

~~~text
Source
  ↓
Build / Runtime Model
  ↓
Dependencies
  ↓
Artifact
  ↓
Configuration + Runtime
  ↓
Process
  ↓
Production Behavior
~~~

## Design Rules

- one primary concept per diagram
- beginner explanation before advanced interpretation
- terminology matches the canonical topic
- implementation-specific behavior is labeled as an example
- Mermaid remains editable, reviewable and version-controlled
- diagrams can be reused in GitHub, videos, articles and teach-back content

## Status

These are conceptual learning diagrams. Language/toolchain-specific details are intentionally simplified and expanded later in Git, CI/CD, container and language-specific contexts.

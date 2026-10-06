---
id: DIA-D00-011
domain: D00
topic: D00-T003
title: Source to Process Lifecycle
type: lifecycle-diagram
status: published
---

# DIA-D00-011 — Source to Process Lifecycle

## Purpose

Connect developer-authored source code to the process that eventually runs on an operating system.

~~~mermaid
flowchart TB
    REQ[Requirement / Change] --> SRC[Source Code]
    SRC --> DEP[Dependencies]
    DEP --> BUILD[Build / Package]
    BUILD --> ART[Versioned Artifact]
    ART --> CONF[Configuration]
    CONF --> RT[Runtime Environment]
    RT --> PROC[Running Process]
    PROC --> OS[Operating System]
    OS --> HW[CPU / Memory / Storage / Network]
~~~

## Beginner Interpretation

Source code is only one stage.

A production application also depends on:

- dependencies
- build/package steps
- artifact identity
- configuration
- runtime
- operating system

## Key Lesson

> Source code is not the same thing as the running application.

## Senior Engineer Connection

When a release fails, identify which lifecycle stage failed before selecting a troubleshooting action.

## SRE Connection

Every stage can affect reliability, especially artifact identity, configuration, runtime compatibility and deployment change.

## Architect Connection

Language/runtime and artifact choices create long-term operational, security, portability and supportability trade-offs.

---
id: DIA-D00-014
domain: D00
topic: D00-T003
title: Build-Time vs Runtime Dependencies
type: comparison-diagram
status: published
---

# DIA-D00-014 — Build-Time vs Runtime Dependencies

## Purpose

Show why successful builds do not guarantee successful execution.

~~~mermaid
flowchart LR
    SRC[Source] --> BT[Build-Time Dependencies]
    BT --> BUILD[Build]
    BUILD --> ART[Artifact]

    ART --> RT[Runtime Dependencies]
    RT --> PROC[Running Process]
~~~

## Build-Time Dependency Examples

- compiler
- build tool
- development headers
- code-generation tools

## Runtime Dependency Examples

- language runtime
- shared library
- database
- external API
- configuration
- secrets

## Failure Model

~~~text
Build-Time Dependency Missing
→ Build Fails

Runtime Dependency Missing
→ Artifact Can Exist
→ Startup or Runtime Fails
~~~

## Key Lesson

> A green build proves only that the build stage succeeded under its inputs.

It does not prove that all runtime conditions are healthy.

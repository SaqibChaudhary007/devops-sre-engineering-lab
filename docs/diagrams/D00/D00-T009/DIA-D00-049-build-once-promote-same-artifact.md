---
id: DIA-D00-049
domain: D00
topic: D00-T009
title: Build Once Promote Same Artifact
type: comparison-diagram
status: published
---

# DIA-D00-049 — Build Once / Promote Same Artifact

## Purpose

Compare rebuild-per-environment with promotion of the same identified artifact.

## Rebuild per Environment

~~~mermaid
flowchart LR
    SRC1[Commit A] --> B1[Build for Dev]
    SRC1 --> B2[Build for Staging]
    SRC1 --> B3[Build for Production]
    B1 --> A1[Artifact A1]
    B2 --> A2[Artifact A2]
    B3 --> A3[Artifact A3]
~~~

Risk:

> Same source revision can still produce different outputs if dependencies, base images, build tools, or external inputs change.

## Build Once / Promote

~~~mermaid
flowchart LR
    SRC2[Commit A] --> BUILD[Build Once]
    BUILD --> ART[Artifact X]
    ART --> DEV[Dev]
    DEV --> STAGE[Staging]
    STAGE --> PROD[Production]
~~~

## Key Lesson

Promoting the same identified artifact reduces **artifact uncertainty**.

It does not eliminate environment-specific differences in configuration, infrastructure, data, dependencies, or traffic.

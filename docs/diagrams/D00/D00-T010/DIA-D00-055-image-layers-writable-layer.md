---
id: DIA-D00-055
domain: D00
topic: D00-T010
title: Image Layers and Writable Container Layer
type: filesystem-lifecycle-diagram
status: published
---

# DIA-D00-055 — Image Layers + Writable Container Layer

## Purpose

Show the different lifecycle of immutable image content and runtime-writable container state.

~~~mermaid
flowchart TB
    BASE[Base Image Layer] --> RUNTIME[Runtime / Library Layer]
    RUNTIME --> DEP[Dependency Layer]
    DEP --> APP[Application Layer]
    APP --> IMAGE[Read-Only Image]
    IMAGE --> WRITE[Writable Container Layer]
    WRITE --> VIEW[Running Filesystem View]

    PERSIST[(Persistent / External Storage)] --> VIEW
~~~

## Lifecycle Model

~~~text
Image Layers
→ reusable packaged content
→ remain unchanged for the image

Writable Container Layer
→ tied to one container instance
→ should not be assumed durable

Persistent / External Storage
→ separate lifecycle
→ survives workload replacement when designed correctly
~~~

## Key Lesson

Replaceable compute and durable data are different architectural concerns.

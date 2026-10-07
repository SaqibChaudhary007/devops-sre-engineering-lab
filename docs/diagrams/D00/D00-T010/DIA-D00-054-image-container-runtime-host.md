---
id: DIA-D00-054
domain: D00
topic: D00-T010
title: Image Container Runtime Host
type: layered-architecture-diagram
status: published
---

# DIA-D00-054 — Image → Container → Runtime → Host

## Purpose

Separate the layers involved when a containerized workload runs.

~~~mermaid
flowchart TB
    SRC[Application Source] --> BUILD[Build]
    BUILD --> IMG[Container Image]
    IMG --> REG[Registry]
    REG --> RT[Container Runtime]
    RT --> CONT[Running Container Process]
    CONT --> KERNEL[Host Kernel]
    KERNEL --> RES[CPU / Memory / Storage / Network]
~~~

## Responsibility Boundaries

~~~text
Image
→ packaged application content

Runtime
→ creates/manages container execution

Container
→ running workload instance

Host Kernel
→ process, network, filesystem, and resource primitives

Infrastructure
→ physical/virtual compute and devices
~~~

## Key Lesson

Troubleshooting should ask which layer owns the failure before choosing tools or commands.

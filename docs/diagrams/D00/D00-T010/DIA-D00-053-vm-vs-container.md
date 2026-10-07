---
id: DIA-D00-053
domain: D00
topic: D00-T010
title: Virtual Machine vs Container
type: comparison-diagram
status: published
---

# DIA-D00-053 — Virtual Machine vs Container

## Purpose

Show the different isolation models of virtual machines and mainstream Linux containers.

## Virtual Machine

~~~mermaid
flowchart TB
    HW1[Physical / Cloud Hardware] --> HYP[Hypervisor]
    HYP --> GUEST1[Guest OS + Kernel]
    HYP --> GUEST2[Guest OS + Kernel]
    GUEST1 --> APP1[Application]
    GUEST2 --> APP2[Application]
~~~

## Container

~~~mermaid
flowchart TB
    HW2[Physical / Cloud Hardware] --> HOST[Host OS + Kernel]
    HOST --> RT[Container Runtime]
    RT --> C1[Containerized Process A]
    RT --> C2[Containerized Process B]
~~~

## Key Distinction

~~~text
VM
→ virtualizes a machine boundary
→ each guest normally has its own kernel

Container
→ isolates processes
→ mainstream Linux containers share the host kernel
~~~

## Key Lesson

"Container = lightweight VM" is an incomplete mental model.

The shared-kernel boundary changes security, host dependency, troubleshooting, startup behavior, and density.

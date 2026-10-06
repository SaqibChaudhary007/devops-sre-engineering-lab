---
id: DIA-D00-010
domain: D00
topic: D00-T002
title: Virtual Machine vs Container OS Model
type: comparison-diagram
status: published
---

# DIA-D00-010 — Virtual Machine vs Container OS Model

## Purpose

Build the OS-level mental model needed before studying containers and Kubernetes.

## Virtual Machine

~~~mermaid
flowchart TB
    VMAPP[Application]
    GUEST[Guest OS / Guest Kernel]
    VH[Virtual Hardware]
    HYP[Hypervisor]
    PHW[Physical Hardware]

    VMAPP --> GUEST --> VH --> HYP --> PHW
~~~

## Linux Container

~~~mermaid
flowchart TB
    C1[Container A Processes]
    C2[Container B Processes]
    ISO[Namespaces / cgroups / capabilities]
    HK[Shared Host Linux Kernel]
    HW[Physical or Virtual Hardware]

    C1 --> ISO
    C2 --> ISO
    ISO --> HK --> HW
~~~

## Core Difference

~~~text
Virtual Machine:
Workload commonly has a guest kernel.

Container:
Workload commonly shares the host kernel.
~~~

## Security Connection

The shared-kernel model makes kernel security and isolation boundaries important.

## Reliability Connection

A host-kernel problem can potentially affect multiple containers on that host.

## Architect Connection

VM vs container decisions involve trade-offs across isolation, density, startup speed, resource overhead, security, operational model, kernel requirements and failure domains.

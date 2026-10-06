---
id: DIA-D00-025
domain: D00
topic: D00-T005
title: Local vs Shared Storage
type: comparison-diagram
status: published
---

# DIA-D00-025 — Local vs Shared Storage

## Purpose

Show how storage placement changes dependency, persistence, and failure behavior.

## Local / Closely Coupled Storage

~~~mermaid
flowchart LR
    VM1[Compute Instance] --> LDISK[(Local / Instance Storage)]
~~~

Potential strengths:

- simple path
- potentially low latency

Potential concerns:

- lifecycle may be tied to compute
- failure can affect both compute and data
- exact persistence guarantees are platform-specific

## Shared / Remote Storage

~~~mermaid
flowchart TB
    A[Compute A] --> SHARED[(Shared / Remote Storage)]
    B[Compute B] --> SHARED
    C[Compute C] --> SHARED
~~~

Potential strengths:

- storage independent from one compute instance
- easier shared access/replacement scenarios

Potential concerns:

- network dependency
- shared bottleneck
- shared failure domain

## Access Models

~~~text
Block  → block device
File   → files/directories
Object → object/key + metadata API
~~~

## Key Lesson

Seeing a device inside a VM does not prove where the physical storage lives or how long it persists.

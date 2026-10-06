
---
id: DIA-D00-001
domain: D00
topic: D00-T001
title: Computer System Overview
type: concept-diagram
status: published
---

# DIA-D00-001 — Computer System Overview

## Purpose

Show the learner where CPU, memory, storage, network and I/O sit relative to an application and operating system.

~~~mermaid
flowchart TB
    U[User] --> A[Application]
    A --> OS[Operating System]

    OS --> CPU[CPU<br/>Executes Instructions]
    OS --> MEM[Memory / RAM<br/>Active Working State]
    OS --> IO[I/O Subsystem<br/>Moves Data]

    IO --> STO[Storage<br/>Persistent Data]
    IO --> NET[Network<br/>Remote Communication]
    IO --> DEV[Devices<br/>Input / Output]

    CPU <--> MEM
    MEM <--> IO
~~~

## Beginner Interpretation

- CPU performs computation.
- Memory holds active working data.
- Storage keeps persistent data.
- Network allows communication.
- The operating system coordinates resource access.

## Senior Engineer Question

If the application is slow, which of these layers could be responsible?

Answer: potentially any of them—or an external dependency beyond the diagram.

## SRE Connection

Infrastructure resource health is diagnostic information. User-facing latency, errors and availability determine reliability impact.

## Architect Connection

Architecture decisions eventually determine how much CPU, memory, storage and network capacity exists and where failure boundaries are placed.

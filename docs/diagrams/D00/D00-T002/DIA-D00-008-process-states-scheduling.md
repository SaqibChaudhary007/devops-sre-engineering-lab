---
id: DIA-D00-008
domain: D00
topic: D00-T002
title: Process States and CPU Scheduling
type: state-diagram
status: published
---

# DIA-D00-008 — Process States & CPU Scheduling

## Purpose

Show why a process can exist without actively consuming CPU.

~~~mermaid
stateDiagram-v2
    [*] --> Ready
    Ready --> Running: Scheduler selects
    Running --> Ready: Preempted / time slice
    Running --> Waiting: Wait for I/O / event / timer
    Waiting --> Ready: Event completes
    Running --> Terminated: Exit
    Terminated --> [*]
~~~

## Scheduler View

~~~mermaid
flowchart LR
    A[Runnable Process A] --> S[CPU Scheduler]
    B[Runnable Process B] --> S
    C[Runnable Process C] --> S
    S --> CPU1[CPU Core / Logical CPU]
    S --> CPU2[CPU Core / Logical CPU]
~~~

## Key Lesson

A process may be runnable, executing, sleeping, waiting or terminated.

> Process exists ≠ process is currently running on CPU.

## Senior Engineer Connection

Low CPU can coexist with high latency when a process is waiting on storage, networking, locks, timers or dependencies.

## Performance Connection

Excessive runnable work can create scheduling contention and waiting even when every process is technically alive.

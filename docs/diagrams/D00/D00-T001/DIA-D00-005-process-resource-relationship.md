
---
id: DIA-D00-005
domain: D00
topic: D00-T001
title: Process and Resource Relationship
type: relationship-diagram
status: published
---

# DIA-D00-005 — Process & Resource Relationship

## Purpose

Connect a program stored on disk with the running process learners observe in the practical lab.

~~~mermaid
flowchart TB
    F[Program / Executable<br/>Stored on Disk]
    OS[Operating System]
    P[Running Process<br/>PID + Execution State]

    F -->|Start| OS
    OS --> P

    P --> CPU[CPU Time]
    P --> MEM[Memory]
    P --> FILE[Files / Storage I/O]
    P --> SOCK[Sockets / Network I/O]

    CPU --> RESULT[Application Work]
    MEM --> RESULT
    FILE --> RESULT
    SOCK --> RESULT
~~~

## Mental Model

~~~text
Program
→ Start
→ Process
→ OS-managed resources
→ Useful work
~~~

## Practical Connection

Use with:

- OBS-D00-002 — Observe a Process
- EXP-D00-001 — Resource Consumption Experiment

## Key Lesson

A process can be running while spending much of its time waiting rather than actively consuming CPU.

## Troubleshooting Connection

For an unavailable service, early questions include:

1. Is the process running?
2. Is it listening where expected?
3. Does it have sufficient resources?
4. Is it waiting on a dependency?
5. Can users actually reach it?

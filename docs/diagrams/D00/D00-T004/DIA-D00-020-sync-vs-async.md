---
id: DIA-D00-020
domain: D00
topic: D00-T004
title: Synchronous vs Asynchronous Communication
type: comparison-diagram
status: published
---

# DIA-D00-020 — Synchronous vs Asynchronous Communication

## Purpose

Show how communication style changes waiting, coupling and operational behavior.

## Synchronous

~~~mermaid
sequenceDiagram
    participant A as Service A
    participant B as Service B
    A->>B: Request
    Note over A: Waits
    B-->>A: Response
    Note over A: Continues
~~~

## Asynchronous

~~~mermaid
flowchart LR
    P[Producer] --> Q[Queue / Broker]
    Q --> C[Consumer]
~~~

## Synchronous Risk

~~~text
Dependency slow
→ caller waits
→ worker/concurrency pressure
→ latency rises
→ users feel it
~~~

## Asynchronous Benefit

~~~text
Producer can hand off work
→ queue buffers
→ consumer processes later
~~~

## Asynchronous Costs

- retries
- ordering
- duplicate handling
- backlog
- delayed completion
- harder end-to-end tracing

## Key Lesson

Async communication reduces immediate waiting coupling, but it does not remove operational complexity.

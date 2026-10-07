---
id: DIA-D00-096
domain: D00
topic: D00-T017
title: Stock Flow Queue Accumulation
type: stock-flow-diagram
status: published
---

# DIA-D00-096 — Stock / Flow / Queue Accumulation

## Purpose

Show how accumulated state changes when inflow and outflow differ over time.

~~~mermaid
flowchart LR
    IN[Arrival / Inflow Rate] --> STOCK[Queue / Backlog / Stock]
    STOCK --> OUT[Processing / Outflow Rate]

    IN -. If Inflow > Outflow .-> GROW[Backlog Grows]
    OUT -. If Outflow > Inflow .-> DRAIN[Backlog Drains]

    GROW --> DELAY[Waiting Time / Age Increases]
    DRAIN --> RECOVER[System Recovers]
~~~

## Mental Model

~~~text
Stock
→ something accumulated

Flow
→ rate that changes the stock
~~~

## Key Lesson

Stable queue depth alone does not prove health.

Oldest-item age, arrival rate, and processing rate can reveal accumulating delay that one snapshot hides.

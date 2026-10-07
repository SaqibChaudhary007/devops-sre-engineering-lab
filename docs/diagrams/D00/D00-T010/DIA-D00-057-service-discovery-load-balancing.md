---
id: DIA-D00-057
domain: D00
topic: D00-T010
title: Service Discovery and Load Balancing Across Replicas
type: networking-diagram
status: published
---

# DIA-D00-057 — Service Discovery + Load Balancing Across Replicas

## Purpose

Show why clients should target a stable logical service rather than individual replaceable workload addresses.

~~~mermaid
flowchart LR
    CLIENT[Client] --> SERVICE[Stable Service Identity]
    SERVICE --> READY{Ready Replica Set}
    READY --> R1[Replica A]
    READY --> R2[Replica B]
    READY --> R3[Replica C]
    R4[Replica D<br/>Not Ready] -. excluded .-> READY
~~~

## Instance Identity vs Service Identity

~~~text
Instance Address
→ can change after replacement

Service Identity
→ stable logical access point
→ routes to currently eligible replicas
~~~

## Key Lesson

Service discovery exists because workload instances are replaceable.

Running is not enough; traffic should normally target instances that are ready to serve.

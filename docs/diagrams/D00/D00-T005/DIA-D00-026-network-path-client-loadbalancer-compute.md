---
id: DIA-D00-026
domain: D00
topic: D00-T005
title: Network Path Client Load Balancer Compute
type: network-foundation-diagram
status: published
---

# DIA-D00-026 — Network Path: Client → Load Balancer → Compute

## Purpose

Connect application reachability to infrastructure networking.

~~~mermaid
flowchart LR
    CLIENT[Client] --> DNS[DNS / Name Resolution]
    DNS --> LB[Load Balancer / Entry Point]
    LB --> VM1[Compute A]
    LB --> VM2[Compute B]
    VM1 --> DB[(Database / Dependency)]
    VM2 --> DB
~~~

## Infrastructure Path

~~~text
Name
→ Address
→ Route
→ Firewall
→ Load Balancer
→ Backend Interface
→ Listening Service
~~~

## Troubleshooting Connection

A healthy process can still be unreachable because of:

- wrong DNS
- missing route
- firewall rule
- load-balancer health/routing issue
- interface problem
- backend port mismatch

## Key Lesson

Network reachability is part of infrastructure health, not separate from it.

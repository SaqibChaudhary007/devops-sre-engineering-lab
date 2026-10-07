---
id: DIA-D00-065
domain: D00
topic: D00-T012
title: Reliability vs Availability vs Durability vs Resilience
type: comparison-diagram
status: published
---

# DIA-D00-065 — Reliability vs Availability vs Durability vs Resilience

## Purpose

Show that reliability is broader than uptime and includes several distinct service properties.

~~~mermaid
flowchart TB
    REL[Reliability<br/>Can users depend on acceptable service over time?]

    REL --> AV[Availability<br/>Is the service usable when needed?]
    REL --> DU[Durability<br/>Does committed data remain intact?]
    REL --> RE[Resilience<br/>Can the service absorb disruption and continue usefully?]
    REL --> RC[Recoverability<br/>Can acceptable service be restored safely and quickly?]
    REL --> CO[Correctness / Performance<br/>Is the result right and timely enough?]
~~~

## Mental Model

~~~text
Availability
≠
Durability
≠
Resilience
≠
Recoverability

All contribute to:
Reliable User Experience
~~~

## Key Lesson

A system can be "up" while still being unreliable because it is too slow, incorrect, stale beyond tolerance, or unable to recover.

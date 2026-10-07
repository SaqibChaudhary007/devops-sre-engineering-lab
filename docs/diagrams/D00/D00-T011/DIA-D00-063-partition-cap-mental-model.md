---
id: DIA-D00-063
domain: D00
topic: D00-T011
title: Partition Trade-Off CAP Mental Model
type: architecture-tradeoff-diagram
status: published
---

# DIA-D00-063 — Partition Trade-Off / CAP Mental Model

## Purpose

Teach CAP as a partition-time trade-off rather than as a permanent "choose two" slogan.

~~~mermaid
flowchart TB
    PART[Network Partition] --> SIDEA[Side A Still Running]
    PART --> SIDEB[Side B Still Running]

    SIDEA --> DECIDE{For Affected Operation}
    SIDEB --> DECIDE

    DECIDE --> CONSIST[Preserve One Coordinated View]
    DECIDE --> AVAIL[Keep Serving Both Sides]

    CONSIST --> REJECT[Reject / Pause Some Operations]
    AVAIL --> DIVERGE[Risk Divergence / Conflict]
~~~

## Key Lesson

During partition, affected operations face a trade-off between:

~~~text
Consistency
and
Availability
~~~

The correct choice depends on the operation's business correctness requirements.

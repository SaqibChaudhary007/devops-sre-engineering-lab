---
id: DIA-D00-062
domain: D00
topic: D00-T011
title: Replication Lag and Stale Read
type: state-diagram
status: published
---

# DIA-D00-062 — Replication → Lag → Stale Read

## Purpose

Show how replicated state can temporarily diverge and expose stale reads.

~~~mermaid
flowchart LR
    CLIENT[Client Write] --> LEADER[Leader / Primary]
    LEADER -->|Replicate| FOLLOWER[Replica / Follower]
    LEADER --> ACK[Write Acknowledged]
    ACK --> READ[Immediate Read]
    READ --> FOLLOWER
    FOLLOWER --> STALE{Replica Caught Up?}
    STALE -->|No| OLD[Older Value Returned]
    STALE -->|Yes| NEW[Latest Value Returned]
~~~

## Business Question

~~~text
Is temporary staleness acceptable for this operation?
~~~

Examples differ:

- recommendations may tolerate staleness
- payment or inventory correctness may require stronger guarantees

## Key Lesson

Consistency requirements come from business correctness, not from one universal architecture rule.

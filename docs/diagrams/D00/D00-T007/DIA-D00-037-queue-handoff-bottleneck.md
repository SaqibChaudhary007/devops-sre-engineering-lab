---
id: DIA-D00-037
domain: D00
topic: D00-T007
title: Queue Handoff Bottleneck Model
type: flow-diagram
status: published
---

# DIA-D00-037 — Queue / Handoff / Bottleneck Model

## Purpose

Show why total delivery time can be dominated by waiting rather than engineering work.

~~~mermaid
flowchart LR
    CODE[Code<br/>2h active] --> Q1[Queue<br/>8h wait]
    Q1 --> REVIEW[Review<br/>1h active]
    REVIEW --> Q2[Queue<br/>12h wait]
    Q2 --> TEST[Test<br/>2h active]
    TEST --> Q3[Approval Queue<br/>24h wait]
    Q3 --> DEPLOY[Deploy<br/>30m active]
~~~

## Flow Observation

~~~text
Active engineering time
≪
Total elapsed time
~~~

## Handoff Risk

~~~text
Team A
→ Team B
→ Team C
~~~

Each handoff may add:

- waiting
- lost context
- rework
- ambiguity

## Bottleneck Principle

If one stage can process three changes/day while upstream creates twenty:

~~~text
Making upstream faster
≠
higher system throughput
~~~

## Key Lesson

DevOps improvement starts by finding the system constraint, not by asking every team to work faster.

---
id: DIA-D00-097
domain: D00
topic: D00-T017
title: Reinforcing vs Balancing Feedback Loops
type: feedback-loop-diagram
status: published
---

# DIA-D00-097 — Reinforcing vs Balancing Feedback Loops

## Purpose

Compare feedback that amplifies change with feedback intended to counteract change.

~~~mermaid
flowchart TB
    subgraph REINFORCING[Reinforcing Loop]
        L1[Latency Rises] --> T1[Timeouts Rise]
        T1 --> R1[Retries Rise]
        R1 --> LOAD1[Load Rises]
        LOAD1 --> L1
    end

    subgraph BALANCING[Balancing Loop]
        LOAD2[Load Rises] --> OBS[Observe Signal]
        OBS --> SCALE[Add Capacity]
        SCALE --> DELAY[Provision / Warm-Up Delay]
        DELAY --> LOWER[Load per Instance Falls]
        LOWER --> OBS
    end
~~~

## Key Lesson

A balancing loop can still oscillate when the signal is noisy, the delay is long, or corrective action is too strong.

A reinforcing loop can turn a small disturbance into a cascading problem.

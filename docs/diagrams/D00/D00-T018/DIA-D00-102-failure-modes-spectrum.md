---
id: DIA-D00-102
domain: D00
topic: D00-T018
title: Failure Modes Spectrum
type: failure-classification-diagram
status: published
---

# DIA-D00-102 — Failure Modes: Down / Slow / Stale / Wrong / Partial / Intermittent

## Purpose

Show that failure is broader than complete outage.

~~~mermaid
flowchart TB
    S[Service / Dependency] --> D[Down / Unavailable]
    S --> L[Slow / Timeout-Prone]
    S --> ST[Stale Data]
    S --> W[Wrong / Incorrect Data]
    S --> P[Partial / Gray Failure]
    S --> I[Intermittent Failure]

    D --> O[User / System Outcome]
    L --> O
    ST --> O
    W --> O
    P --> O
    I --> O
~~~

## Key Lesson

A service can be reachable and still be failing. Slow, stale, incorrect, partial and intermittent behavior can be operationally significant failures.

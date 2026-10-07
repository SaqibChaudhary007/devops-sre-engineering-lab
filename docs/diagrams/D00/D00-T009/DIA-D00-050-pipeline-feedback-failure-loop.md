---
id: DIA-D00-050
domain: D00
topic: D00-T009
title: Pipeline Feedback and Failure Loop
type: troubleshooting-diagram
status: published
---

# DIA-D00-050 — Pipeline Feedback & Failure Loop

## Purpose

Show how a pipeline should react to failure with evidence rather than reflexive reruns.

~~~mermaid
flowchart LR
    RUN[Pipeline Run] --> CHECK[Stage / Check]
    CHECK --> RESULT{Pass?}
    RESULT -->|Yes| NEXT[Continue]
    RESULT -->|No| CLASSIFY[Classify Failure]
    CLASSIFY --> TRANSIENT{Transient?}
    TRANSIENT -->|Yes| RETRY[Controlled Retry]
    TRANSIENT -->|No / Unknown| INVESTIGATE[Investigate]
    RETRY --> EVIDENCE[Preserve Evidence]
    INVESTIGATE --> EVIDENCE
    EVIDENCE --> FIX[Fix / Recover]
    FIX --> LEARN[Improve Pipeline / System]
~~~

## Failure Categories

~~~text
Deterministic
Transient
Flaky / Untrusted
Concurrency Conflict
Unknown
~~~

## Key Lesson

A failed pipeline should produce evidence.

Blind reruns can hide flaky tests, race conditions, shared-environment conflicts, or real defects.

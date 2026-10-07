---
id: DIA-D00-068
domain: D00
topic: D00-T012
title: Detect Contain Recover Validate Learn
type: recovery-lifecycle-diagram
status: published
---

# DIA-D00-068 — Detect → Contain → Recover → Validate → Learn

## Purpose

Show recovery as an operational lifecycle rather than a single failover event.

~~~mermaid
flowchart LR
    FAIL[Failure / Degradation] --> DETECT[Detect]
    DETECT --> TRIAGE[Understand Impact]
    TRIAGE --> CONTAIN[Contain Blast Radius]
    CONTAIN --> RECOVER[Recover Service]
    RECOVER --> VALIDATE[Validate User Journey]
    VALIDATE --> LEARN[Learn / RCA]
    LEARN --> IMPROVE[Improve Design / Operations]
    IMPROVE --> READY[Prepare for Next Failure]
~~~

## Time Dimensions

~~~text
Failure Start
→ Detection Time
→ Response Time
→ Recovery Time
→ Validation
~~~

## Key Lesson

A service is not recovered merely because infrastructure changed state.

Recovery should be validated against the user journey and followed by learning.

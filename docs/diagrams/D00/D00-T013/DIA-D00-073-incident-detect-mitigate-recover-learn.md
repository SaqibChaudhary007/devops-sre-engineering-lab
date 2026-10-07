---
id: DIA-D00-073
domain: D00
topic: D00-T013
title: Incident Detect Mitigate Recover Learn
type: incident-lifecycle-diagram
status: published
---

# DIA-D00-073 — Incident: Detect → Mitigate → Recover → Learn

## Purpose

Show the difference between restoring acceptable service and permanently correcting the underlying problem.

~~~mermaid
flowchart LR
    IMPACT[User Impact Begins] --> DETECT[Detect]
    DETECT --> TRIAGE[Triage]
    TRIAGE --> MITIGATE[Mitigate<br/>Reduce User Impact]
    MITIGATE --> RECOVER[Recover]
    RECOVER --> VALIDATE[Validate User Journey]
    VALIDATE --> RCA[Deep Diagnosis / Contributing Factors]
    RCA --> ACTION[Engineering Actions]
    ACTION --> IMPROVE[Improve System / Operations]
~~~

## Key Distinction

~~~text
Mitigation
→ restore acceptable service

Permanent Correction
→ reduce recurrence / remove underlying weakness
~~~

## Key Lesson

Do not wait for perfect root-cause certainty before taking a safe, evidence-based mitigation that reduces user harm.

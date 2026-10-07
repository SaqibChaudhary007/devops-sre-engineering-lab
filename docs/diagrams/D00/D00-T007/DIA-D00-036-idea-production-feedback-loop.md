---
id: DIA-D00-036
domain: D00
topic: D00-T007
title: Idea Production Feedback Loop
type: lifecycle-diagram
status: published
---

# DIA-D00-036 — Idea → Production → Feedback Loop

## Purpose

Show that software delivery is a loop rather than a one-way pipeline.

~~~mermaid
flowchart LR
    IDEA[Idea] --> PLAN[Plan]
    PLAN --> CODE[Code]
    CODE --> REVIEW[Review]
    REVIEW --> BUILD[Build]
    BUILD --> TEST[Test]
    TEST --> RELEASE[Release]
    RELEASE --> DEPLOY[Deploy]
    DEPLOY --> OPERATE[Operate]
    OPERATE --> OBSERVE[Observe]
    OBSERVE --> LEARN[Learn]
    LEARN --> IDEA
~~~

## Feedback Sources

~~~text
Review
→ code/design feedback

Build/Test
→ technical validation

Deploy
→ release feedback

Production
→ latency/errors/capacity/user behavior

Incidents
→ operational learning
~~~

## Key Lesson

A delivery system is incomplete if it moves change forward but does not return useful information to the people who create and operate the system.

## SRE Connection

Production telemetry and incidents are part of engineering feedback, not separate operational concerns.

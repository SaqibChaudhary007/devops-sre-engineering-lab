---
id: DIA-D00-044
domain: D00
topic: D00-T008
title: Plan Apply Infrastructure Lifecycle
type: lifecycle-diagram
status: published
---

# DIA-D00-044 — Plan → Apply → Infrastructure Lifecycle

## Purpose

Show how infrastructure intent becomes runtime change and where review risk appears.

~~~mermaid
flowchart LR
    CODE[Definition] --> PLAN[Plan / Preview]
    PLAN --> REVIEW[Review]
    REVIEW --> APPLY[Apply]
    APPLY --> API[Provider / Platform API]
    API --> LIFE[Resource Lifecycle]
    LIFE --> CREATE[Create]
    LIFE --> UPDATE[Update]
    LIFE --> REPLACE[Replace]
    LIFE --> DELETE[Delete]
~~~

## Risk Gradient

~~~text
No Change
< Update
< Create
< Replace / Delete
~~~

The exact risk depends on state, dependencies, data, and architecture.

## Key Lesson

A plan is a change proposal.

It reduces uncertainty but does not guarantee successful or safe execution.

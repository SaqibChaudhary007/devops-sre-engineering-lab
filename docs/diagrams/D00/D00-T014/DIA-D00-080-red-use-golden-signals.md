---
id: DIA-D00-080
domain: D00
topic: D00-T014
title: RED vs USE vs Golden Signals
type: observability-framework-diagram
status: published
---

# DIA-D00-080 — RED vs USE vs Golden Signals

## Purpose

Compare three common monitoring heuristics and show that each answers a different class of operational question.

~~~mermaid
flowchart TB
    OBS[Operational Question]

    OBS --> RED[RED<br/>Rate<br/>Errors<br/>Duration]
    OBS --> USE[USE<br/>Utilization<br/>Saturation<br/>Errors]
    OBS --> GOLD[Golden Signals<br/>Latency<br/>Traffic<br/>Errors<br/>Saturation]

    RED --> SERVICE[Request / Service Behavior]
    USE --> RESOURCE[Resource Behavior]
    GOLD --> OVERVIEW[Service + Capacity Overview]
~~~

## Key Lesson

~~~text
RED
→ request-driven service questions

USE
→ resource bottleneck questions

Golden Signals
→ broad service-health overview
~~~

These are useful heuristics, not complete observability architectures.

Workload-specific business, dependency, correctness, and queue signals may still be required.

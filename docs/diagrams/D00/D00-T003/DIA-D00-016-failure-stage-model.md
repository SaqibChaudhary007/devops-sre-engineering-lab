---
id: DIA-D00-016
domain: D00
topic: D00-T003
title: Build vs Startup vs Runtime Failure
type: troubleshooting-diagram
status: published
---

# DIA-D00-016 — Build vs Startup vs Runtime Failure

## Purpose

Help learners classify software failures before choosing a troubleshooting action.

~~~mermaid
flowchart LR
    SRC[Source + Dependencies] --> BUILD[Build]
    BUILD -->|Failure| BF[Build Failure]
    BUILD -->|Success| ART[Artifact]

    ART --> START[Application Startup]
    START -->|Failure| SF[Startup Failure]
    START -->|Success| RUN[Running Application]

    RUN -->|Failure during operation| RF[Runtime Failure]
~~~

## Typical Examples

### Build Failure

- compiler error
- dependency resolution failure
- test failure
- packaging error

### Startup Failure

- missing configuration
- missing runtime library
- permission denied
- port already in use
- required secret missing

### Runtime Failure

- database timeout
- external dependency failure
- memory/resource exhaustion
- unexpected input
- operational bug

## Troubleshooting Rule

~~~text
Identify Failure Stage
        ↓
Collect Stage-Specific Evidence
        ↓
Form Hypotheses
        ↓
Test Safely
        ↓
Mitigate / Fix
~~~

## Key Lesson

Do not rebuild a valid artifact to solve a missing production configuration unless evidence shows the artifact itself is wrong.

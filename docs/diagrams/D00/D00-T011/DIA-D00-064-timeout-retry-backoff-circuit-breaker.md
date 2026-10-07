---
id: DIA-D00-064
domain: D00
topic: D00-T011
title: Timeout Retry Backoff Circuit Breaker Failure Loop
type: resilience-diagram
status: published
---

# DIA-D00-064 — Timeout + Retry + Backoff + Circuit Breaker Failure Loop

## Purpose

Show how resilience controls can either reduce or amplify a dependency failure depending on how they are combined.

~~~mermaid
flowchart LR
    CALL[Call Dependency] --> SLOW{Slow / Failing?}
    SLOW -->|No| OK[Return Result]
    SLOW -->|Yes| WAIT[Timeout]
    WAIT --> CLASSIFY{Retry Appropriate?}
    CLASSIFY -->|No| FAIL[Fail / Degrade]
    CLASSIFY -->|Yes| BACKOFF[Backoff + Jitter]
    BACKOFF --> BUDGET{Retry Budget Available?}
    BUDGET -->|No| FAIL
    BUDGET -->|Yes| CIRCUIT{Circuit Open?}
    CIRCUIT -->|Yes| FAST[Fail Fast]
    CIRCUIT -->|No| CALL
~~~

## Failure Amplification Risk

~~~text
Slow Dependency
→ Longer Requests
→ More In-Flight Work
→ Timeouts
→ Retries
→ More Load
→ Slower Dependency
~~~

## Key Lesson

Timeouts, retries, backoff, jitter, circuit breakers, and load shedding are coordinated controls.

Poor combinations can worsen the outage they were intended to survive.

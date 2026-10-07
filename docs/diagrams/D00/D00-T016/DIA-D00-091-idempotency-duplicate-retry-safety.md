---
id: DIA-D00-091
domain: D00
topic: D00-T016
title: Idempotency Duplicate Execution Retry Safety
type: retry-safety-diagram
status: published
---

# DIA-D00-091 — Idempotency / Duplicate Execution / Retry Safety

## Purpose

Show why retries must consider side effects and duplicate execution before an operation is repeated.

~~~mermaid
flowchart TB
    FAIL[Operation Fails / Outcome Unknown] --> CLASSIFY{Failure Type?}
    CLASSIFY --> TRANSIENT[Transient / Retry Candidate]
    CLASSIFY --> PERM[Permanent / Invalid / Authorization]
    PERM --> STOP[Stop / Escalate]

    TRANSIENT --> SIDE{Safe to Repeat?}
    SIDE -->|Idempotent / Protected| POLICY[Bounded Retry Policy]
    SIDE -->|Side-Effect Sensitive| RECON[Reconcile State / Use Operation Identity / Human Review]

    POLICY --> BACKOFF[Backoff + Jitter]
    BACKOFF --> BUDGET[Respect Timeout / Attempt Budget]
    BUDGET --> RETRY[Retry]
    RETRY --> VALIDATE[Validate Outcome]
~~~

## Key Lesson

Idempotency does not guarantee success.

It reduces repeated-effect risk.

Retries should be bounded, conditioned on failure type and side effects, and validated after execution.

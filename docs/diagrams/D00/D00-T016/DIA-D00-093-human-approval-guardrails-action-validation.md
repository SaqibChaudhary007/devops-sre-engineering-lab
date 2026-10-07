---
id: DIA-D00-093
domain: D00
topic: D00-T016
title: Human Approval Guardrails Automated Action Validation
type: approval-boundary-diagram
status: published
---

# DIA-D00-093 — Human Approval → Guardrails → Automated Action → Validation

## Purpose

Show human approval as an intentional automation boundary for high-impact, irreversible, unusual, or uncertain actions.

~~~mermaid
flowchart LR
    REQ[Requested Automation] --> RISK{Impact / Reversibility / Confidence}
    RISK -->|Low Risk| GUARD[Guardrail Checks]
    RISK -->|Higher Risk / Uncertain| HUMAN[Human Review / Approval]
    HUMAN --> GUARD
    GUARD --> ALLOW{Allowed?}
    ALLOW -->|No| STOP[Stop / Record Reason]
    ALLOW -->|Yes| ACT[Automated Action]
    ACT --> VALID[Validate Outcome]
    VALID --> AUDIT[Audit / Feedback]
~~~

## Key Lesson

Human-in-the-loop is not failed automation.

It is a legitimate design boundary when context, impact, uncertainty, or irreversibility require judgment.

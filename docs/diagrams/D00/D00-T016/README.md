# D00-T016 Visual / Diagram Package — Automation Mental Models

This package provides reusable diagrams for **00.16 — Automation Mental Models**.

## Diagram Set

1. [DIA-D00-089 — Trigger → Preconditions → State → Action → Validation → Feedback](DIA-D00-089-trigger-preconditions-state-action-validation-feedback.md)
2. [DIA-D00-090 — Current State ↔ Desired State → Reconciliation Loop](DIA-D00-090-current-desired-reconciliation-loop.md)
3. [DIA-D00-091 — Idempotency / Duplicate Execution / Retry Safety](DIA-D00-091-idempotency-duplicate-retry-safety.md)
4. [DIA-D00-092 — Partial Failure → Rollback / Roll-Forward / Compensation](DIA-D00-092-partial-failure-recovery-options.md)
5. [DIA-D00-093 — Human Approval → Guardrails → Automated Action → Validation](DIA-D00-093-human-approval-guardrails-action-validation.md)
6. [DIA-D00-094 — Automation Blast Radius: Scope / Rate / Identity / Environment / Stop Conditions](DIA-D00-094-automation-blast-radius-guardrails.md)

## Learning Progression

~~~text
Trigger
→ Intent
→ Preconditions
→ State
→ Action
→ Validation
→ Feedback
→ Recovery
~~~

## Design Rules

- stay provider-neutral
- show automation as state-aware, not just command execution
- distinguish repeatability from idempotency
- show retries as bounded policy rather than automatic reaction
- show reconciliation as an iterative control-loop pattern
- show partial failure as expected workflow behavior
- include human approval where impact, irreversibility, or uncertainty is high
- show blast radius as something bounded by scope, rate, permissions, environment, and stop conditions
- show outcome validation rather than exit-code-only success
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Deep workflow engines, distributed locking, broker delivery semantics, controller-runtime internals, GitOps implementation, cloud automation APIs, policy engines, autonomous remediation, and AI-agent orchestration belong to later domains.

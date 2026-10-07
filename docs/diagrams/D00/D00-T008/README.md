# D00-T008 Visual / Diagram Package — Infrastructure as Code Mental Model

This package provides reusable diagrams for **00.08 — Infrastructure as Code Mental Model**.

## Diagram Set

1. [DIA-D00-041 — Manual Infrastructure vs Infrastructure as Code](DIA-D00-041-manual-vs-infrastructure-as-code.md)
2. [DIA-D00-042 — Desired State vs Actual State](DIA-D00-042-desired-vs-actual-state.md)
3. [DIA-D00-043 — Declarative vs Imperative](DIA-D00-043-declarative-vs-imperative.md)
4. [DIA-D00-044 — Plan → Apply → Infrastructure Lifecycle](DIA-D00-044-plan-apply-lifecycle.md)
5. [DIA-D00-045 — IaC State / Dependency / Locking Model](DIA-D00-045-state-dependency-locking.md)
6. [DIA-D00-046 — IaC Change Risk: Review → Blast Radius → Recovery](DIA-D00-046-review-blast-radius-recovery.md)

## Learning Progression

~~~text
Manual Change
   ↓
Desired State
   ↓
Declarative / Imperative Model
   ↓
Plan / Apply / Lifecycle
   ↓
State / Dependencies / Locking
   ↓
Review / Blast Radius / Recovery
~~~

## Design Rules

- stay provider-neutral
- do not imply every IaC system has a user-managed state file
- do not imply remote state always provides locking
- distinguish preview from guaranteed execution
- make replacement/delete risk visible
- connect infrastructure change to security, cost, reliability, and recovery
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Deep Terraform, Ansible, Bicep, CloudFormation, GitOps, policy-as-code, testing, and provider implementation belong to later domains.

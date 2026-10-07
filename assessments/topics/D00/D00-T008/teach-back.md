# D00-T008 — Teach-Back Assessment

## Goal

Demonstrate that you can explain Infrastructure as Code without reducing it to Terraform or syntax.

## Task A — Beginner

Explain:

- what IaC is
- why it exists
- why it is more than a tool

Use one simple analogy.

## Task B — Engineer

Explain:

~~~text
Desired State
→ Definition
→ Plan
→ Apply
→ Actual State
~~~

Then explain where drift can appear.

## Task C — Declarative vs Imperative

Explain the difference and give one situation where each may be appropriate.

Then explain why declarative does not automatically mean safe.

## Task D — State

Explain:

- why Terraform needs state
- why state files are not universal to all IaC systems
- why remote state does not automatically guarantee locking

## Task E — Senior Engineer

Explain why this statement is unsafe:

> "The plan is clean, so production is safe."

Include:

- replacement
- delete
- dependencies
- quotas
- permissions
- API/provider behavior
- runtime health

## Task F — SRE

Explain how IaC changes should connect to:

- SLOs
- incidents
- blast radius
- rollback/failover
- emergency changes
- recovery

## Task G — Architect

Explain how you would decide:

- state boundaries
- ownership
- module boundaries
- environment separation
- policy
- apply permissions
- recovery strategy

## GitOps Challenge

Explain why:

~~~text
IaC
≠
GitOps
~~~

Then describe what GitOps adds.

## Recovery Challenge

Explain why:

> "Revert Git" is not the same as infrastructure rollback.

## Scoring

Score 1–5 for:

- correctness
- clarity
- desired/actual-state reasoning
- state/drift reasoning
- plan/apply risk reasoning
- reliability awareness
- architecture/ownership trade-off awareness

Target: average 4/5 with no critical misconception.

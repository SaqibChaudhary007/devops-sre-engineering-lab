---
id: D00-T008
domain: D00
title: Infrastructure as Code Mental Model
level:
  - L1
  - L2
  - L3
priority: P1
status: draft
estimated_time:
  theory: 5-7h
  practical: 1-2h
  assessment: 1-2h
prerequisites:
  required:
    - D00-T001
    - D00-T002
    - D00-T003
    - D00-T004
    - D00-T005
    - D00-T006
    - D00-T007
  recommended: []
evidence_status:
  - RESEARCHED
certifications: []
content_series:
  - How It Really Works
  - Why Does It Exist
  - Under the Hood
  - Five Levels
  - Architecture With Saqib
---

# 00.08 — Infrastructure as Code Mental Model

## Start Here

Infrastructure as Code (IaC) addresses a simple operational problem:

> How do we make infrastructure changes repeatable, reviewable, traceable, automatable, and safer than one-off manual actions?

IaC means expressing infrastructure intent in machine-readable definitions that can be versioned, reviewed, validated, and applied through automation.

IaC is not Terraform only, not YAML, not a cloud template, and not guaranteed correctness.

The mental model is:

~~~text
Intent
→ Definition
→ Review
→ Validation
→ Plan
→ Apply
→ Observe
→ Improve
~~~

This topic stays provider-neutral. Deep Terraform, Ansible, Bicep, CloudFormation, GitOps, policy-as-code, and provider implementation come later.

---

# 1. What You Will Learn

You should be able to explain:

- why IaC exists
- desired state vs actual state
- declarative vs imperative approaches
- idempotence
- drift
- plan/apply
- resource lifecycle
- dependency graphs
- state and remote state
- locking/concurrency
- variables, outputs, and modules
- environment separation
- ownership boundaries
- providers/plugins/APIs
- import/adoption
- destroy risk
- rollback limitations
- validation/testing
- policy as code
- secrets handling
- CI/CD and GitOps relationships
- security, cost, blast radius, and recovery
- Senior/SRE/Architect reasoning

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)
- [00.02 — Operating System Mental Model](../00-02-operating-system-mental-model/README.md)
- [00.03 — Software Engineering Foundations](../00-03-software-engineering-foundations/README.md)
- [00.04 — Application Architecture Fundamentals](../00-04-application-architecture-fundamentals/README.md)
- [00.05 — Infrastructure Foundations](../00-05-infrastructure-foundations/README.md)
- [00.06 — Cloud Mental Models](../00-06-cloud-mental-models/README.md)
- [00.07 — DevOps Foundations](../00-07-devops-foundations/README.md)

You should already understand infrastructure resources, cloud APIs, environments, automation, version control, CI/CD at a high level, change risk, blast radius, and production feedback.

---

# 3. Why IaC Exists

Manual infrastructure often looks like:

~~~text
Ticket
→ Human Login
→ Click / Command
→ Resource Changed
~~~

This can create undocumented changes, drift, inconsistent environments, weak auditability, slow recovery, and dependence on individual knowledge.

IaC changes the model:

~~~text
Infrastructure Definition
→ Review
→ Validation
→ Automated Execution
→ Infrastructure Change
~~~

---

# 4. Core Mental Model

~~~text
Desired Infrastructure
        ↓
Infrastructure Definition
        ↓
IaC Engine
        ↓
Provider / Platform API
        ↓
Actual Infrastructure
~~~

The implementation varies by tool, but the operating principle stays similar.

---

# 5. Desired State

Desired state describes what you want.

Example:

~~~text
2 app instances
1 load balancer
1 database
1 private network
~~~

Desired state expresses intent. It does not guarantee the platform can reach that state successfully.

---

# 6. Actual State

Actual state is what currently exists.

~~~text
Desired: 2 instances
Actual:  1 instance
~~~

Differences can come from failed creation, manual change, deletion, provider error, drift, or external dependencies.

---

# 7. Reconciliation

A reconciliation-oriented model compares desired and actual state and attempts to reduce the difference.

~~~text
Desired
→ Compare
→ Difference
→ Action
→ Actual moves toward Desired
~~~

Not every IaC tool continuously reconciles; some act only when explicitly run.

---

# 8. Declarative vs Imperative

Declarative:

~~~text
Describe what you want.
~~~

Imperative:

~~~text
Describe the steps to perform.
~~~

Real systems may combine both.

Declarative is not automatically better; the right model depends on lifecycle, failure handling, state complexity, and operational requirements.

---

# 9. Idempotence

An idempotent operation can be repeated without continually changing the result once the desired state is reached.

~~~text
Run 1 → create
Run 2 → no meaningful change
Run 3 → no meaningful change
~~~

Idempotence is important for safe, repeatable automation.

---

# 10. Configuration Drift

Drift means actual infrastructure differs from the managed definition.

Example:

~~~text
Code:
Allow HTTPS

Manual Change:
Also allow SSH from anywhere
~~~

Now code and reality differ.

Drift creates security, audit, troubleshooting, and future-change risk.

---

# 11. Version Control

Version control makes infrastructure changes:

- reviewable
- traceable
- collaborative
- auditable
- comparable over time

A common workflow is:

~~~text
Change
→ Commit
→ Review
→ Merge
→ Apply
~~~

---

# 12. Diff vs Runtime Effect

A code diff shows definition changes.

Example:

~~~text
instance_count: 2 → 4
disk_size: 100 GB → 200 GB
~~~

But a code diff does not always reveal exact runtime impact.

That is why a change plan matters.

---

# 13. Plan / Preview

A plan estimates intended infrastructure actions.

~~~text
Definition
+ Current State
→ Planned Actions
~~~

Typical actions:

~~~text
Create
Update
Replace
Delete
No Change
~~~

A plan reduces uncertainty. It does not guarantee success.

---

# 14. Apply

Apply turns approved intent into real infrastructure changes.

~~~text
Reviewed Intent
→ IaC Engine
→ Provider API
→ Resource Change
~~~

Apply is where blast radius becomes real.

---

# 15. Resource Lifecycle

Resources generally move through operations such as:

~~~text
Create
Read
Update
Replace
Delete
~~~

Changing one property may update in place; another may force replacement.

---

# 16. Replacement Risk

Replacement can be much riskier than update.

Questions include:

- where is state?
- is downtime possible?
- will identity or address change?
- can data be preserved?
- what depends on this resource?

A harmless-looking definition change may be destructive at runtime.

---

# 17. Dependency Graph

Resources depend on one another.

~~~text
Network
  ↓
Subnet
  ↓
VM
  ↓
Application
~~~

IaC systems often use dependency information to determine valid ordering.

---

# 18. Explicit vs Implicit Dependencies

Implicit dependency:

~~~text
VM references Subnet ID
→ VM depends on Subnet
~~~

Explicit dependency:

~~~text
Dependency declared manually
~~~

Explicit dependencies are useful when inference is insufficient, but overuse can make configurations harder to maintain.

---

# 19. State Tracking

Some IaC tools maintain state mapping definitions to real resources.

~~~text
Code Resource
↕
IaC State
↕
Real Resource
~~~

State can hold identity, attributes, dependencies, and previous configuration.

---

# 20. Why State Matters

If state is stale, missing, corrupted, or concurrently modified, the tool may make incorrect assumptions.

Possible effects:

- duplicate creation
- accidental replacement
- failed plans
- unexpected deletion
- ownership confusion

State is part of the operational architecture.

---

# 21. Remote State

Teams commonly place shared state in a remote backend/service for collaboration, backup, locking, access control, and CI/CD execution.

State should not be treated as an unimportant local file.

---

# 22. Locking and Concurrency

Two concurrent applies can conflict.

~~~text
Engineer A Apply
        ↘
      Shared State
        ↗
Engineer B Apply
~~~

Locking helps protect shared mutation, though it does not solve every coordination problem.

---

# 23. State Security

State may contain resource IDs, topology details, configuration values, metadata, and sometimes sensitive material.

Protect it with:

- access control
- encryption
- backup
- secure storage
- auditability

---

# 24. Variables and Outputs

Variables let definitions accept inputs.

~~~text
environment = production
instance_count = 4
~~~

Outputs expose useful results such as endpoints or resource IDs.

Both help composition, but careless outputs can expose sensitive data.

---

# 25. Modules / Reusable Components

Modules package reusable patterns.

~~~text
Network Module
Application Module
Database Module
~~~

Benefits:

- reuse
- standardization
- shared improvement
- less duplication

Risks:

- hidden complexity
- over-generalization
- tight coupling
- difficult upgrades

---

# 26. Module Versioning

Reusable modules evolve.

Without controlled versions:

~~~text
Module changes
→ consumers may change unexpectedly
~~~

Versioning supports controlled adoption.

---

# 27. Environment Separation

Development, QA, staging, and production may use related definitions but different requirements.

Production may need different scale, controls, data boundaries, availability, and security.

IaC should reduce uncontrolled differences without pretending every environment is identical.

---

# 28. Parameterization vs Duplication

Too much duplication causes drift.

Too much parameterization creates giant definitions full of switches.

Good IaC balances reuse, clarity, and ownership.

---

# 29. Ownership Boundaries

One IaC state/package should have a clear ownership boundary.

A single state controlling an entire organization can create huge blast radius.

Possible separation boundaries include environment, service, platform layer, team, and lifecycle.

There is no universal split.

---

# 30. Blast Radius

IaC can change many resources quickly.

That is powerful and dangerous.

A single bad apply may affect one resource, one service, one environment, multiple environments, or a whole account/subscription/project.

Blast radius should be intentionally controlled.

---

# 31. Review

IaC review should ask:

- what changes?
- why?
- what will be replaced?
- what is deleted?
- what permissions change?
- what is the cost impact?
- where is state?
- what is the recovery path?

---

# 32. Validation and Testing

Validation can include formatting, syntax, schema, static analysis, plan inspection, policy checks, integration tests, and post-deployment checks.

Correct syntax does not prove safe infrastructure behavior.

---

# 33. Policy as Code — Preview

Policy as code evaluates infrastructure changes against defined rules.

~~~text
IaC Change
→ Policy
→ Allow / Warn / Deny
~~~

Examples include requiring encryption/tags, restricting regions, blocking public storage, or restricting instance types.

---

# 34. Secrets

Plaintext secrets should not be casually embedded in infrastructure definitions.

Safer patterns can use secret managers, protected CI/CD variables, encrypted stores, or identity-based access.

The exact pattern depends on the tool and platform.

---

# 35. Provider / Plugin Mental Model

IaC engines often use provider/plugin components to talk to platform APIs.

~~~text
IaC Definition
→ Engine
→ Provider / Plugin
→ Platform API
~~~

Provider versions and API behavior can change plans and execution.

---

# 36. API Dependency

A correct definition can still fail because of authentication, authorization, API outage, rate limits, quotas, invalid requests, provider changes, or regional capacity.

IaC correctness and platform availability are different concerns.

---

# 37. Import / Adoption

Existing manually created resources may need to be adopted.

~~~text
Existing Resource
+ Definition
+ Import / Mapping
→ Managed Resource
~~~

Incorrect adoption can produce dangerous plans.

---

# 38. Destroy

Destroy removes infrastructure.

Production destructive actions need strong safeguards, limited permissions, review, and recovery planning.

IaC makes deletion repeatable too.

---

# 39. Rollback Is Not Simple

Reverting code does not guarantee infrastructure returns safely.

Reasons include resource replacement, data migrations, irreversible operations, changed IDs/endpoints, external state, and dependent resources.

Infrastructure recovery must be designed, not assumed.

---

# 40. Roll Forward

Sometimes recovery means correcting the definition and applying a new change.

~~~text
Bad Change
→ Fix Definition
→ Validate
→ Apply Correction
~~~

Rollback vs roll-forward depends on the failure mode.

---

# 41. Mutable vs Immutable Infrastructure

IaC can update existing resources or support replacement-based workflows.

~~~text
Update Existing
~~~

versus

~~~text
Create New
→ Validate
→ Shift Traffic
→ Remove Old
~~~

IaC and immutable infrastructure are related, but not identical.

---

# 42. CI/CD Integration

A common IaC workflow is:

~~~text
Commit
→ Validate
→ Plan
→ Review
→ Approve
→ Apply
→ Observe
~~~

Production normally needs stronger controls than lower environments.

---

# 43. GitOps — Preview

A simplified GitOps mental model is:

~~~text
Git Desired State
→ Automated Reconciliation
→ Runtime Environment
~~~

IaC and GitOps overlap but are not identical.

Deep GitOps belongs to D21.

---

# 44. Observability for IaC

Infrastructure change should produce evidence such as who changed what, when, the plan, apply result, resource events, errors, and post-change health.

Change events should be correlatable with incidents.

---

# 45. Security Perspective

Security questions include:

- who can plan?
- who can apply?
- who can destroy?
- where are credentials stored?
- who can read state?
- are permissions least-privilege?
- are destructive actions protected?
- is every change auditable?

Automation power increases the importance of access control.

---

# 46. Cost Perspective

IaC can create expensive infrastructure quickly.

Review should consider resource count, size, storage, transfer, replication, multi-zone/multi-region use, managed-service cost, and orphaned resources.

A valid plan can still be financially unsafe.

---

# 47. Senior Engineer Perspective

A senior engineer asks:

- what is desired?
- what exists?
- what will the plan do?
- what gets replaced or deleted?
- where is state?
- who owns it?
- what drift exists?
- what is the blast radius?
- how do we recover?

Evidence comes before execution.

---

# 48. SRE Perspective

An SRE asks:

- can this change affect SLOs?
- how do we correlate it with incidents?
- what is the recovery path?
- what failure domain changes?
- can emergency changes be reconciled back into code?
- could automation repeat damage?

Infrastructure change is production change.

---

# 49. Architect Perspective

An architect asks:

- what should be managed as code?
- how should state be partitioned?
- what is the ownership boundary?
- what should be standardized?
- where is autonomy required?
- how are secrets and policies handled?
- what must be recoverable?
- how large can blast radius be?
- what provider lock-in is acceptable?

IaC architecture is partly organizational architecture.

---

# 50. Common Beginner Mistakes

## Mistake 1

"IaC means Terraform."

Terraform is one implementation tool.

## Mistake 2

"Declarative means safe."

Wrong intent can still be expressed declaratively.

## Mistake 3

"A clean plan guarantees success."

Plans reduce uncertainty but do not model every runtime outcome.

## Mistake 4

"Reverting Git rolls infrastructure back."

Stateful or irreversible changes may prevent simple rollback.

## Mistake 5

"Manual changes are harmless."

Manual changes create drift unless reconciled.

## Mistake 6

"One giant state is simpler."

It may create unacceptable blast radius and ownership problems.

## Mistake 7

"IaC guarantees reproducibility."

Provider APIs, versions, quotas, external dependencies, and mutable external state still matter.

---

# 51. Five-Level Explanation

## L1 — Foundation

IaC describes infrastructure in files/code so it can be created and changed consistently.

## L2 — Engineer

IaC combines version control, automation, desired state, reusable definitions, and platform APIs.

## L3 — Senior Engineer

Safe IaC requires reasoning about state, drift, dependencies, plan/apply behavior, replacement, concurrency, ownership, and recovery.

## L4 — SRE

Infrastructure changes must be observable, failure-aware, recoverable, and connected to service reliability.

## L5 — Architect

IaC architecture balances standardization, autonomy, state boundaries, policy, security, provider capabilities, cost, blast radius, and organizational ownership.

---

# 52. What You Must Retain

Before moving on, retain:

- IaC is an operating model, not one tool
- desired state and actual state can differ
- declarative and imperative models are different
- idempotence matters
- drift is a production risk
- version control makes infrastructure changes reviewable
- plans reduce uncertainty but do not guarantee success
- replacement can be riskier than update
- dependencies affect ordering
- state is operationally important
- remote state requires access control and locking
- modules improve reuse but can increase coupling
- ownership boundaries affect blast radius
- secrets and policy need deliberate handling
- provider/API behavior affects execution
- destroy needs safeguards
- reverting definitions does not guarantee rollback
- IaC can integrate with CI/CD and GitOps
- infrastructure changes should be observable
- IaC improves repeatability but does not guarantee correctness

---

# 53. Practical Package — Next Layer

The practical package should include safe exercises such as:

- model desired vs actual state
- compare declarative vs imperative approaches
- simulate drift
- build a dependency graph
- classify create/update/replace/delete actions
- design state and ownership boundaries
- review a hypothetical plan for security, blast radius, and cost

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 54. Assessment Package — Pending

The assessment should test why IaC exists, desired vs actual state, declarative vs imperative, idempotence, drift, plan/apply, lifecycle, replacement risk, dependencies, state, locking, modules, environment separation, policy, secrets, provider/API behavior, import, destroy, rollback limits, CI/CD/GitOps relationships, and Senior/SRE/Architect reasoning.

---

# 55. Visual Package — Pending

The visual package should include:

1. Manual Infrastructure vs Infrastructure as Code
2. Desired State vs Actual State
3. Declarative vs Imperative
4. Plan → Apply → Infrastructure Lifecycle
5. IaC State / Dependency / Locking Model
6. IaC Change Risk: Review → Blast Radius → Recovery

---

# 56. What Comes Next

After D00-T008 is completed, continue to:

## 00.09 — CI/CD Mental Model

That topic will connect IaC and DevOps delivery principles to pipeline stages, artifacts, promotion, environments, deployment strategies, approvals, rollback, release safety, and feedback.

---

# 57. Sources & Evidence

Planned authoritative source families:

- HashiCorp Terraform documentation
- AWS CloudFormation documentation
- Microsoft Bicep / ARM documentation
- Ansible documentation
- OpenGitOps principles
- provider guidance on state, lifecycle, and automation
- security guidance for secrets and CI/CD integration

Current evidence status:

- conceptual draft: RESEARCHED
- source verification: pending
- practical package: pending
- assessment package: pending
- visual package: pending

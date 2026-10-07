# D00-T008 Source Verification — Infrastructure as Code Mental Model

## Verification Goal

Verify the core claims in **00.08 — Infrastructure as Code Mental Model** against official Terraform, AWS CloudFormation, Microsoft Bicep/ARM, Ansible, and OpenGitOps documentation.

## Verification Status

**Result:** Core claims verified with several important tool-specific nuances.

**Evidence level:** E2 — supported by official product documentation and vendor-neutral OpenGitOps principles.

This topic remains provider-neutral. Deep Terraform, Ansible, Bicep, CloudFormation, GitOps, policy-as-code, and provider-specific implementation belong to later domains.

---

## Verified Claim Map

| Topic claim | Verification | Primary source |
|---|---|---|
| IaC can express desired infrastructure declaratively and deploy it repeatedly | Verified | Microsoft Bicep |
| Plan/preview mechanisms reduce uncertainty before deployment | Verified | Terraform, AWS CloudFormation, Azure What-If |
| A preview does not guarantee successful deployment | Verified | AWS CloudFormation; Azure What-If limitations |
| Drift is the difference between expected/template state and actual resource state | Verified | AWS CloudFormation drift-aware change sets |
| Terraform state maps configuration resources to real-world objects | Verified | HashiCorp Terraform state docs |
| Terraform remote state is recommended for team collaboration | Verified | HashiCorp Terraform state docs |
| Terraform state locking prevents concurrent writers when the selected backend supports it | Verified | HashiCorp Terraform state locking docs |
| Import/adoption can bring existing resources under Terraform management | Verified | HashiCorp Terraform import docs |
| Terraform import requires plan review because unexpected replacement/destruction can occur | Verified | HashiCorp Terraform import docs |
| Bicep is declarative and does not require a user-managed state file | Verified | Microsoft Bicep |
| Ansible commonly expresses desired state and many modules are idempotent, but not all playbooks/modules are | Verified | Ansible documentation |
| GitOps requires declarative, versioned/immutable desired state, automatic pull, and continuous reconciliation | Verified | OpenGitOps |

---

# Primary / Authoritative Sources

## 1. HashiCorp Terraform — State

- https://developer.hashicorp.com/terraform/language/state
- https://developer.hashicorp.com/terraform/language/state/purpose
- https://developer.hashicorp.com/terraform/language/state/backends
- https://developer.hashicorp.com/terraform/language/state/locking

Supports:

- state as the mapping between configuration and remote objects
- state metadata/dependency tracking
- remote state for team collaboration
- locking when supported by the backend
- risks of unmanaged/manual state mutation
- state as operationally important, not disposable bookkeeping

### Important nuance

> State files are not universal to all IaC systems.

Terraform requires state, while Bicep/ARM relies on Azure Resource Manager and does not require a user-managed state file.

Therefore D00-T008 must teach **state tracking as tool-specific**, not as a universal IaC requirement.

---

## 2. HashiCorp Terraform — Plan / Apply / Import

- https://developer.hashicorp.com/terraform/tutorials/cli/apply
- https://developer.hashicorp.com/terraform/language/import
- https://developer.hashicorp.com/terraform/language/import/single-resource
- https://developer.hashicorp.com/terraform/tutorials/state/state-import

Supports:

- plan as a preview of intended changes
- apply as execution of planned changes
- create/update/delete/replace behavior
- importing existing resources
- plan review before import/apply
- potential replacement/destruction when imported configuration does not match the real resource

### Important nuance

> Import does not discover the original intent of a resource.

Terraform import works from current provider-reported infrastructure state and still requires operator understanding and careful plan review.

---

## 3. AWS CloudFormation — Change Sets and Drift

- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-changesets.html
- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/drift-aware-change-sets.html

Supports:

- previewing proposed infrastructure changes before execution
- create/update/delete/replacement visibility
- drift as divergence between expected/template configuration and actual resources
- three-way reasoning across actual state, previous deployment state, and desired state
- explicit statement that change sets do not guarantee successful stack updates

### Important nuance

A preview/change set is evidence for safer review, not proof that runtime execution will succeed.

Provider quotas, dependencies, API behavior, permissions, capacity, and runtime conditions can still cause failure.

---

## 4. Microsoft Bicep / Azure Resource Manager

- https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview
- https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deploy-what-if

Supports:

- declarative infrastructure definitions
- repeated deployment of the desired infrastructure
- dependency orchestration
- modules and reuse
- previewing changes with What-If
- no user-managed state/state file requirement

### Important nuance

Bicep proves why the curriculum should not imply:

> "All IaC tools need a state file."

The broader concept is that an IaC system needs some way to reason about intended/current resources, but the implementation differs by platform.

---

## 5. Ansible — Desired State and Idempotence

- https://docs.ansible.com/projects/ansible/latest/getting_started/introduction.html
- https://docs.ansible.com/projects/ansible-core/devel/playbook_guide/playbooks_intro.html

Supports:

- desired-state automation
- idempotence for many modules
- repeated execution producing no further change once desired state is reached

### Important nuance

Ansible explicitly notes that not every module/playbook is idempotent.

Therefore:

> "IaC is idempotent"

is too broad.

A better mental model is:

> Idempotence is a desirable property for repeatable infrastructure automation, but it depends on the tool, module, and implementation.

---

## 6. OpenGitOps — GitOps Relationship

- https://opengitops.dev/

Supports the four OpenGitOps principles:

1. Declarative
2. Versioned and immutable
3. Pulled automatically
4. Continuously reconciled

### Important nuance

GitOps and IaC overlap but are not identical.

IaC can be executed manually or through push-based CI/CD. GitOps specifically requires an automated pull/reconciliation model around versioned desired state.

---

# Verified Nuances / Corrections

## 1. State Is Tool-Specific

Terraform requires explicit state.

Bicep does not require the user to manage a state file.

Therefore D00-T008 should teach:

~~~text
Some IaC systems keep explicit state.
Others query/manage platform state through the control plane.
~~~

The universal concept is **resource identity/current-state reasoning**, not a universal state-file mechanism.

## 2. Locking Is Not Universal

Terraform locking depends on backend support.

Therefore:

> "Remote state provides locking"

is too broad.

Better:

> A remote backend may provide locking; verify backend capabilities.

## 3. IaC Does Not Always Continuously Reconcile

Terraform normally plans/applies when invoked.

GitOps agents continuously observe and reconcile.

Therefore:

> Declarative IaC != continuous reconciliation by default.

## 4. Declarative Does Not Mean Safe

Bicep, CloudFormation, Terraform, and GitOps can all express wrong desired state.

Declarative syntax improves intent clarity and repeatability, not correctness guarantees.

## 5. Plan / What-If / Change Set Is a Preview, Not a Promise

Terraform plan, Azure What-If, and CloudFormation change sets reduce uncertainty.

They cannot guarantee successful runtime deployment.

## 6. Drift Is a First-Class Operational Risk

CloudFormation explicitly defines drift around changes made outside managed template workflows.

Drift may be introduced by:

- console/manual changes
- CLI/SDK changes
- emergency incident changes
- external automation

Emergency changes should later be reconciled into the managed definition.

## 7. Import Requires Intent Reconstruction

Importing existing infrastructure maps a real resource into IaC management.

It does not reconstruct historical design intent automatically.

Careful plan review is required.

## 8. Idempotence Must Be Qualified

Many Ansible modules are idempotent.

Some are not.

Idempotence should be taught as an important automation property, not an unconditional guarantee.

## 9. GitOps Is More Specific Than IaC

GitOps adds:

~~~text
Declarative desired state
+ Versioned / immutable history
+ Automatic pull
+ Continuous reconciliation
~~~

IaC alone does not require all four.

## 10. Reverting Code Does Not Guarantee Infrastructure Rollback

Official plan/import/change-set behavior supports the broader operational point that infrastructure changes can involve replacement, state mutation, and provider-side effects.

Therefore infrastructure recovery must be designed rather than assumed from source-control history alone.

---

# Evidence Decision

The following D00-T008 areas are now eligible for **DOC-VERIFIED** status:

- declarative desired-state model
- plan/preview/apply mental model
- drift
- Terraform state purpose
- remote state/team collaboration
- backend-dependent locking
- resource import/adoption
- replacement/destruction risk
- Bicep declarative/no-user-managed-state nuance
- Ansible desired-state/idempotence nuance
- GitOps relationship and continuous reconciliation distinction

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured exercises:

- desired vs actual-state comparison
- declarative vs imperative classification
- drift simulation
- create/update/replace/delete classification
- dependency-graph reasoning
- state/ownership boundary design
- concurrent-change reasoning
- destructive-change review
- plan review for security, cost, and blast radius
- rollback vs roll-forward decision reasoning

These become the D00-T008 practical package.

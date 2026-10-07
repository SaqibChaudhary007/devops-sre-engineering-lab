# D00-T016 Source Verification — Automation Mental Models

## Verification Goal

Verify the core claims in **00.16 — Automation Mental Models** against authoritative reliability, control-loop, infrastructure-as-code, and cloud operational guidance.

Primary source families used:

- Google SRE automation and toil guidance
- Kubernetes controller / control-loop documentation
- HashiCorp Terraform workflow and state documentation
- Microsoft Azure Well-Architected transient-fault guidance

## Verification Status

**Result:** Core D00-T016 claims are supported, with important nuances around automation value, idempotency, desired/current state, reconciliation, planning and approval, retries, backoff, jitter, timeouts, partial failure, automation blast radius, toil reduction, and human judgment.

**Evidence level:** E2 — supported by first-party operational documentation and authoritative SRE guidance.

This topic remains at the D00 mental-model level. Detailed workflow-engine implementation, controller-runtime internals, distributed locking algorithms, message-broker semantics, cloud-specific automation APIs, GitOps engines, policy engines, autonomous remediation, and AI-agent execution belong to later domains.

---

# Primary / Authoritative Sources

## 1. Google SRE — The Evolution of Automation at Google

- https://sre.google/sre-book/automation-at-google/

Supports:

- automation is a force multiplier, not a panacea
- automation can improve consistency and scale
- thoughtless automation can create new problems
- idempotent fixes are safer for repeated execution
- rate limiting and blast-radius thinking matter
- automation should be applied judiciously rather than universally

### Verified nuance

Do not teach:

~~~text
Automation
→ Always Better
~~~

A stronger model is:

~~~text
Well-Understood Task
+ Safe Preconditions
+ Idempotent / Bounded Action
+ Validation
+ Guardrails
→ Useful Automation
~~~

Automation multiplies both good and bad decisions.

---

## 2. Google SRE — Eliminating Toil

- https://sre.google/sre-book/eliminating-toil/
- https://sre.google/workbook/eliminating-toil/

Supports:

- repetitive, manual, automatable operational work can consume engineering capacity
- automation is useful when it removes toil
- not all operational work is toil
- novel diagnosis and engineering work are not automatically toil
- automation should improve long-term operating leverage rather than simply script every task

### Verified nuance

A sensible maturity path is:

~~~text
Understand Work
→ Document / Standardize
→ Identify Repetition
→ Automate Safely
~~~

Do not automate a broken process merely because it is repetitive.

---

## 3. Kubernetes — Controllers and Control Loops

- https://kubernetes.io/docs/concepts/architecture/controller/

Supports:

- a controller is a control loop
- desired state and current state are distinct
- controllers observe current state and act to move it toward desired state
- reconciliation is iterative rather than one-time
- controllers may act directly or request changes through APIs

### Verified nuance

The D00 reconciliation model is valid:

~~~text
Observe
→ Compare Current vs Desired
→ Act
→ Observe Again
~~~

This is a durable control-system pattern, not a Kubernetes-only concept.

---

## 4. Kubernetes — Kubelet Sync Loop

- https://kubernetes.io/docs/reference/node/kubelet-sync-loop/

Supports:

- reconciliation can be continuous or periodic
- work may be queued from multiple sources
- observed state can lag real state slightly
- repeated loops try to drive actual state toward desired state

### Verified nuance

Reconciliation does not imply the system instantly becomes correct.

There can be delay, stale observations, transient failures, and repeated correction attempts.

---

## 5. Terraform — Plan / Apply / Desired State

- https://developer.hashicorp.com/terraform/cli/run
- https://developer.hashicorp.com/terraform/cli/commands/plan
- https://developer.hashicorp.com/terraform/cli/commands/apply

Supports:

- Terraform compares configuration/desired state with current state
- plan previews proposed changes before apply
- approval can be part of the workflow
- speculative plans are not guaranteed to remain valid if real-world state changes later
- apply may fail partway through
- Terraform does not automatically roll back every partially completed apply
- automation therefore needs state awareness and explicit failure/recovery reasoning

### Verified nuance

This supports several D00 concepts:

~~~text
Intent
→ Plan
→ Review / Approval
→ Apply
→ Validate
~~~

and:

~~~text
Partial Failure
→ Inspect Current State
→ Reconcile / Correct
~~~

Do not assume that all infrastructure automation is transactional.

---

## 6. Terraform — Idempotent Import Example

- https://developer.hashicorp.com/terraform/language/import/single-resource

Supports:

- an idempotent operation can be repeated without creating an additional effect after the intended state is already reached
- repeated execution can safely converge when the resource is already represented in state

### Verified nuance

At D00, idempotency means:

> Repeating the same intended operation should not create additional unintended side effects.

Idempotency does **not** mean:

- every operation succeeds
- every operation is reversible
- every retry is safe

---

## 7. Azure Well-Architected — Transient Fault Handling

- https://learn.microsoft.com/en-us/azure/well-architected/design-guides/handle-transient-faults

Supports:

- retries should be used for transient faults
- idempotency matters for retry safety
- exponential or increasing backoff can reduce pressure on recovering dependencies
- jitter helps prevent synchronized retries
- timeouts must be part of retry design
- throttling/rate limiting protects systems from overload
- retry policy needs explicit bounds and conditions

### Verified nuance

Do not teach:

~~~text
Failure
→ Retry Immediately Forever
~~~

A stronger model is:

~~~text
Classify Failure
→ Check Retry Safety
→ Bound Attempts
→ Backoff
→ Add Jitter Where Appropriate
→ Respect Timeout / Rate Limit
→ Stop / Escalate
~~~

---

# Verified Claim Map

| Topic claim | Verification | Primary source family |
|---|---|---|
| Automation is a force multiplier, not a panacea | Verified | Google SRE |
| Automation can reduce toil and improve consistency | Verified | Google SRE |
| Idempotency improves repeated-execution safety | Verified | Google SRE / Terraform |
| Current state and desired state are distinct | Verified | Kubernetes / Terraform |
| Reconciliation moves actual state toward desired state | Verified | Kubernetes |
| Control loops repeatedly observe and correct | Verified | Kubernetes |
| Planning/review before action is useful | Verified | Terraform |
| Approval can be an intentional automation boundary | Verified | Terraform |
| Partial apply can leave intermediate state | Verified | Terraform |
| Retries are appropriate mainly for transient faults | Verified | Azure |
| Retry safety depends on idempotency/side effects | Verified | Azure |
| Backoff reduces pressure on recovering dependencies | Verified | Azure |
| Jitter helps prevent synchronized retry storms | Verified | Azure |
| Timeouts are part of retry policy | Verified | Azure |
| Rate limiting / throttling bounds amplification | Verified | Google SRE / Azure |
| Automation should be observable and bounded | Verified at operational mental-model level | Google SRE |
| Automation can increase blast radius | Verified at operational mental-model level | Google SRE |
| Not all manual/operational work should be automated | Verified | Google SRE toil guidance |

---

# Verified Nuances / Corrections

## 1. Automation Is Not Synonymous with Scripting

Scripts are one implementation mechanism.

Automation also includes:

- controllers
- workflows
- reconciler loops
- schedulers
- pipelines
- policies
- event-driven systems

## 2. Automation Multiplies Intent

A useful mental model is:

~~~text
Good Intent + Safe Design
→ Faster Consistent Good Outcomes

Wrong Assumption + Broad Access
→ Faster Larger Failure
~~~

Automation increases leverage in both directions.

## 3. Reconciliation Is Iterative

Desired/current-state reconciliation is not a one-time action.

The system may require many observe/compare/act cycles and may never be perfectly static.

## 4. Idempotency Is About Repeated Effect

Idempotency does not guarantee success.

It means repeated application should not keep creating new unintended side effects after the intended state is reached.

## 5. Retry Is a Policy, Not a Reaction

Retry design should include:

- which failures qualify
- attempt limit
- delay/backoff
- jitter where useful
- timeout budget
- idempotency/side-effect analysis
- stop/escalation behavior

## 6. Partial Failure Must Be Expected

Infrastructure/workflow automation may complete some steps and fail later.

Therefore automation should expose current state and provide a path to reconcile, roll forward, roll back where safe, or compensate.

## 7. Rollback Is Not Universal

Rollback may be unsafe or impossible after:

- irreversible external side effects
- incompatible data migration
- downstream state changes

Roll-forward or compensation may be safer.

## 8. Approval Is Not Anti-Automation

A human approval boundary can be part of a well-designed automated workflow, especially for:

- high-impact action
- unusual state
- irreversible action
- weak confidence
- security-sensitive change

## 9. Success Output Is Not Outcome Validation

A process can exit successfully while the desired system state is not achieved.

Postconditions and user/system validation remain necessary.

## 10. Rate Limits and Guardrails Matter

Automation should have bounded:

- scope
- rate
- environment
- permissions
- batch size
- retry count

This reduces accidental amplification.

## 11. Automation Needs Identity

Automation acts on systems and therefore needs:

- explicit identity
- scoped permissions
- auditable actions
- controlled secret/credential use

Shared human credentials should not be the default automation identity.

## 12. Self-Healing Must Be Bounded

Repeated autonomous remediation without stop conditions can create loops or amplify an incident.

A stronger D00 model is:

~~~text
Detect
→ Validate Condition
→ Bounded Action
→ Recheck
→ Stop / Escalate
~~~

## 13. Human Judgment Still Matters

Automation is strongest for understood, measurable, bounded, repeated work.

Ambiguous or high-impact situations can still require human reasoning.

## 14. AI-Assisted Automation Requires Stronger Validation as Risk Rises

AI output can be probabilistic or uncertain.

At D00:

~~~text
Low Impact + Reversible
→ More Autonomy Possible

High Impact / Irreversible / Uncertain
→ Stronger Guardrails + Validation + Approval
~~~

Detailed AI-agent design belongs later.

---

# Evidence Decision

The following D00-T016 areas are now eligible for **DOC-VERIFIED** status:

- automation purpose and value
- automation vs manual work
- intent / trigger / state
- current vs desired state
- reconciliation
- control loops
- imperative/declarative distinction at foundation level
- preconditions / postconditions / validation
- repeatability
- idempotency
- duplicate-execution risk
- retries
- retry safety
- backoff
- jitter
- timeouts
- rate limiting / throttling
- partial failure
- rollback / roll-forward / compensation at foundation level
- human approval boundaries
- automation blast radius
- guardrails
- automation identity / least privilege
- automation observability / auditability
- toil reduction
- self-healing / auto-remediation preview
- automation economics
- reliability/security trade-offs
- AI-assisted automation safety boundary at foundation level

The following remain intentionally preview-level pending later domains:

- distributed-lock algorithms
- exactly-once processing semantics
- workflow-engine internals
- saga implementation patterns
- message-broker delivery semantics
- controller-runtime internals
- GitOps implementation
- autonomous remediation engines
- distributed scheduler design
- queue platform implementation
- policy-engine implementation
- AI-agent orchestration
- multi-agent execution
- production approval-system implementation

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured, safe exercises:

- classify tasks by automation suitability
- design triggers/preconditions/actions/validation
- compare imperative vs declarative models
- classify idempotent/non-idempotent actions
- review retry safety
- design timeout/backoff/jitter reasoning
- model partial failure and compensation
- review concurrency and duplicate execution
- define human approval boundaries
- design blast-radius guardrails
- design automation observability/audit evidence
- perform automation production-readiness review

These become the D00-T016 practical package.

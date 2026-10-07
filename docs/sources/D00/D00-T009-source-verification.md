# D00-T009 Source Verification — CI/CD Mental Model

## Verification Goal

Verify the core claims in **00.09 — CI/CD Mental Model** against current AWS Prescriptive Guidance, GitHub Actions documentation, Microsoft Azure delivery guidance, OpenGitOps principles, and SLSA supply-chain guidance.

## Verification Status

**Result:** Core claims verified with several important implementation and terminology nuances.

**Evidence level:** E2 — supported by current official platform documentation, vendor engineering guidance, and the SLSA/OpenGitOps specifications.

This topic remains provider-neutral. Deep implementation in GitHub Actions, GitLab CI/CD, Jenkins, Azure DevOps, Tekton, OpenShift Pipelines, Argo CD, deployment strategies, and supply-chain controls belongs to later domains.

---

## Verified Claim Map

| Topic claim | Verification | Primary source |
|---|---|---|
| CI/CD automates much of the software release lifecycle | Verified | AWS Prescriptive Guidance |
| CI integrates changes frequently and returns rapid validation feedback | Verified | AWS Prescriptive Guidance |
| Continuous delivery and continuous deployment differ at production promotion | Verified with terminology nuance | AWS Prescriptive Guidance |
| Pipelines commonly include source/build/test/staging/production activities | Verified | AWS Prescriptive Guidance |
| Build once / promote the same artifact reduces environment-to-environment artifact uncertainty | Verified | AWS DevOps Guidance; Microsoft Learn |
| Pipeline artifacts persist build/test outputs across jobs or stages | Verified | GitHub Actions |
| Pipeline concurrency needs explicit control when jobs target shared resources/environments | Verified | GitHub Actions |
| Hosted and self-hosted runners execute workflow jobs with different control/operational trade-offs | Verified | GitHub Actions |
| Environments can enforce approvals, deployment restrictions, protection rules, and scoped secrets | Verified | GitHub Actions |
| Pipeline credentials should be permission-scoped; short-lived identity federation can reduce long-lived secrets | Verified | GitHub Actions OIDC/security docs |
| Post-deployment behavior should feed back into the delivery process | Verified | AWS Prescriptive Guidance |
| Artifact provenance helps trace what produced a software artifact | Verified | SLSA v1.2 |
| GitOps adds declarative, versioned/immutable desired state, automatic pull, and continuous reconciliation | Verified | OpenGitOps |
| CI/CD and GitOps can complement each other but are not identical | Verified | OpenGitOps + AWS delivery guidance |

---

# Primary / Authoritative Sources

## 1. AWS Prescriptive Guidance — CI/CD Definitions

- https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-cicd-litmus/understanding-cicd.html
- https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-caf-platform-perspective/ci-cd.html
- https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-cicd-litmus/cicd-best-practices.html

Supports:

- CI/CD as automation across the software release lifecycle
- source/build/test/staging/production pipeline stages
- frequent integration and automated validation
- small/frequent changes
- continuous delivery vs continuous deployment distinction
- post-deployment behavior feeding back into delivery
- deployment strategies and recovery thinking
- versioned/signed build artifacts and provenance-related practices

### Important terminology nuance

AWS describes continuous delivery as retaining an explicit production approval and continuous deployment as an uninterrupted path to production.

The broader mental model should therefore remain:

~~~text
Continuous Delivery
→ software is kept releasable / production-ready through a repeatable process
→ production promotion may remain a deliberate decision

Continuous Deployment
→ validated change automatically proceeds to production
~~~

Do not reduce the distinction to a vendor-specific UI implementation.

---

# 2. AWS DevOps Guidance — Build Once / Deploy Many

- https://docs.aws.amazon.com/wellarchitected/latest/devops-guidance/anti-patterns-for-continuous-delivery.html

Supports:

- building more than once as a continuous-delivery anti-pattern
- risk of environment-specific rebuild differences
- using trusted artifact repositories
- promoting the same built artifact through environments

### Important nuance

"Build once, promote" is a strong delivery pattern, not a magical guarantee of identical runtime behavior.

Environment-specific configuration, infrastructure, data, dependencies, and runtime conditions can still differ.

---

# 3. Microsoft Learn — Build Once / Promote Same Artifact

- https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/publishing-workflows
- https://learn.microsoft.com/en-us/azure/devops/pipelines/process/stages

Supports:

- separation of build/publish from deployment
- build once / deploy the same image or artifact through multiple environments
- stage/job/task hierarchy
- approvals/checks around production stages
- controlled stage sequencing

### Important nuance

The portable concept is:

> Promote the same identified build output where practical.

Do not teach that every application type or deployment system can avoid every environment-specific transformation.

---

# 4. GitHub Actions — Artifacts

- https://docs.github.com/en/actions/concepts/workflows-and-actions/workflow-artifacts

Supports:

- artifacts as files produced during a workflow
- persistence of build/test outputs beyond a job
- sharing artifacts between jobs
- distinction between artifacts and dependency caches

### Important nuance

Artifact storage and cache storage serve different purposes.

Do not teach cache as a trusted substitute for a versioned release artifact.

---

# 5. GitHub Actions — Runners and Concurrency

- https://docs.github.com/en/actions/concepts/runners
- https://docs.github.com/en/actions/how-tos/manage-runners
- https://docs.github.com/en/actions/concepts/workflows-and-actions/concurrency

Supports:

- GitHub-hosted vs self-hosted execution workers
- workflow/job concurrency
- preventing multiple deployments from targeting the same environment simultaneously
- cancellation/queue behavior for stale or competing runs

### Important nuance

Concurrency controls coordination.

They do not prove the deployment itself is safe.

---

# 6. GitHub Actions — Environments, Protection, and Secrets

- https://docs.github.com/en/actions/concepts/workflows-and-actions/deployment-environments
- https://docs.github.com/en/actions/reference/workflows-and-actions/deployments-and-environments
- https://docs.github.com/en/actions/concepts/security/secrets
- https://docs.github.com/en/actions/reference/security/oidc

Supports:

- deployment environments
- required reviewers
- deployment branch/tag restrictions
- custom deployment protection rules
- environment-scoped secrets
- permission-limited credentials
- OIDC-based short-lived cloud identity patterns

### Important nuance

An approval gate is useful only if it represents a real risk/decision boundary.

A manual gate that adds no evidence or judgment can become pure queueing.

---

# 7. AWS — Post-Deployment Feedback

- https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-caf-platform-perspective/ci-cd.html

Supports:

- capturing post-deployment production behavior
- using monitoring/logging to understand pipeline/application outcomes
- feeding post-deployment results into corrective action
- deployment frequency/lead-time/pipeline-time metrics

### Important nuance

A successful deployment command proves that the deployment action completed.

It does **not** by itself prove that the service is healthy for users.

---

# 8. SLSA v1.2 — Artifact Provenance

- https://slsa.dev/spec/v1.2/provenance
- https://slsa.dev/spec/v1.2/verifying-artifacts

Supports:

- provenance as verifiable information about where/how an artifact was produced
- tracing build output back to source/build process
- artifact verification against trusted expectations

### Important nuance

Provenance strengthens traceability and integrity evidence.

It does not prove that application logic is correct or that deployment will be reliable.

---

# 9. OpenGitOps — GitOps Relationship

- https://opengitops.dev/

Supports the OpenGitOps principles:

1. Declarative
2. Versioned and immutable
3. Pulled automatically
4. Continuously reconciled

### Important nuance

CI/CD and GitOps can work together.

A common model is:

~~~text
CI
→ build / test / produce artifact

Delivery workflow
→ update desired state

GitOps reconciler
→ pull and apply desired state
~~~

GitOps does not eliminate the need for CI.

---

# Verified Nuances / Corrections

## 1. Continuous Delivery Is Broader Than "Manual Approval"

AWS uses a manual-production-approval distinction in its prescriptive definition.

For a provider-neutral curriculum, retain the broader concept:

> Continuous delivery keeps software releasable through a repeatable process; production release may remain a deliberate decision.

Continuous deployment specifically automates successful change through production promotion.

## 2. Build Once / Promote Is a Risk-Reduction Pattern

Rebuilding independently per environment can produce different artifacts.

Promoting the same identified artifact reduces that uncertainty.

It does not remove differences in:

- runtime configuration
- infrastructure
- data
- external dependencies
- traffic

## 3. Artifact and Cache Are Different

Artifacts represent build/test outputs that can be persisted and transferred.

Caches optimize repeated work.

A cache should not be treated as the canonical release artifact.

## 4. A Green Pipeline Is Evidence, Not Certainty

Passing automated checks means the checks passed.

It does not prove:

- all failure modes were tested
- production dependencies are healthy
- capacity is sufficient
- data migration is reversible
- user-facing behavior is correct

## 5. Approval Gates Must Represent Real Risk Decisions

GitHub/Azure environment controls prove that approvals and protection rules are valid delivery mechanisms.

They should still be judged by whether they reduce meaningful risk instead of adding ritual waiting.

## 6. Concurrency Is a Delivery-Safety Concern

Two otherwise-correct pipeline runs can conflict when they mutate:

- the same environment
- the same deployment target
- shared infrastructure/state
- shared mutable data

Concurrency policy is part of delivery architecture.

## 7. Runner Trust Boundary Matters

Hosted and self-hosted runners have different operational/security models.

Self-hosted execution can reach private systems but increases responsibility for runner hardening, isolation, lifecycle, and trust.

## 8. Long-Lived Secrets Are Not the Only Credential Model

OIDC/federated identity can allow workflow jobs to obtain short-lived credentials from supported cloud providers.

The curriculum should therefore teach:

> Prefer scoped, short-lived identity where available; otherwise protect stored secrets carefully.

## 9. Successful Deployment Does Not Equal Successful Release

Deployment changes runtime software.

Release makes behavior available to users.

Feature flags and traffic-control mechanisms can separate these events.

The exact mechanism is product/platform-specific.

## 10. Rollback Is Conditional

Rollback can be unsafe or impossible when:

- database/schema compatibility changed
- external state changed
- irreversible side effects occurred
- previous versions cannot work with the new state

Roll-forward, failover, restore, or feature disablement may be safer depending on the failure.

## 11. CI/CD and GitOps Are Different Control Models

Push-style delivery:

~~~text
Pipeline
→ target environment
~~~

GitOps-style delivery:

~~~text
Pipeline / Human
→ desired state in version control
→ reconciler pulls
→ environment converges
~~~

They can be combined.

## 12. Supply-Chain Traceability Goes Beyond Commit SHA

Useful traceability can include:

~~~text
Source Revision
→ Build Process
→ Artifact
→ Provenance / Attestation
→ Deployment
→ Runtime Outcome
~~~

This supports debugging and integrity verification.

---

# Evidence Decision

The following D00-T009 areas are now eligible for **DOC-VERIFIED** status:

- CI/CD definitions and delivery lifecycle
- CI vs continuous delivery vs continuous deployment
- pipeline stages
- build-once/promote pattern
- artifact concept
- stage/job/task mental model
- runner mental model
- concurrency
- environment protections and approvals
- secrets and short-lived identity
- deployment feedback/verification
- supply-chain provenance
- CI/CD vs GitOps relationship

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured exercises:

- trace commit → build → artifact → environment → production outcome
- classify pipeline stages and feedback points
- compare build-once/promote vs rebuild-per-environment
- distinguish artifact from cache
- diagnose a failing pipeline
- classify retryable vs deterministic failures
- reason about concurrency conflicts
- design artifact/version traceability
- evaluate environment protections and approval gates
- reason about rollback vs roll-forward
- connect deployment events to post-deployment telemetry

These become the D00-T009 practical package.

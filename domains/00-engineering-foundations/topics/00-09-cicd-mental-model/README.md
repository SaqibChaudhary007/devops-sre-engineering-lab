---
id: D00-T009
domain: D00
title: CI/CD Mental Model
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
    - D00-T008
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - How It Really Works
  - Why Does It Exist
  - Under the Hood
  - Five Levels
  - Production Room
  - Architecture With Saqib
---

# 00.09 — CI/CD Mental Model

## Start Here

You now understand DevOps as an end-to-end delivery system and Infrastructure as Code as a way to manage infrastructure change through reviewable, repeatable workflows.

The next question is:

> How does a software change move safely and repeatedly from source code to a running production system?

That is the problem space of **Continuous Integration and Continuous Delivery / Deployment**.

CI/CD is not:

- a Jenkins server
- a YAML file
- a single pipeline
- automatically safe because tests pass
- the same as "deploy to production on every commit"

The core mental model is:

~~~text
Change
→ Integrate
→ Build
→ Validate
→ Package
→ Promote
→ Deploy
→ Verify
→ Observe
→ Learn
~~~

This topic stays at the mental-model level. Deep implementation in GitHub Actions, GitLab CI, Jenkins, Azure DevOps, Argo CD, Tekton, OpenShift Pipelines, artifact systems, deployment strategies, and release engineering comes later.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- why CI exists
- why CD exists
- continuous integration
- continuous delivery
- continuous deployment
- pipeline stages
- pipeline vs workflow vs job vs step
- source trigger
- build
- unit/integration/security validation
- artifacts
- artifact immutability
- artifact repositories
- environment promotion
- promotion vs rebuild
- deployment
- release
- feature flags
- deployment strategy
- approval gates
- policy gates
- pipeline feedback
- failure handling
- retries
- rollback vs roll-forward
- secrets and credentials in pipelines
- runners/agents/executors
- hosted vs self-hosted execution
- caching
- concurrency
- environment protection
- branch protection
- quality gates
- deployment verification
- observability
- change correlation
- supply-chain integrity at a high level
- CI/CD with IaC
- CI/CD vs GitOps
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
- [00.08 — Infrastructure as Code Mental Model](../00-08-infrastructure-as-code-mental-model/README.md)

You should already understand source control, application artifacts, infrastructure, environments, delivery flow, feedback loops, change risk, desired state, and production ownership.

---

# 3. Why CI Exists

Without continuous integration, teams may work for long periods on separate changes and discover conflicts late.

A weak model:

~~~text
Developer A works for 10 days
Developer B works for 10 days
Developer C works for 10 days
→ merge everything together
→ discover conflicts and failures
~~~

CI shortens that feedback loop.

---

# 4. Continuous Integration

Continuous Integration means integrating changes frequently and validating them automatically.

~~~text
Code Change
→ Version Control
→ Build
→ Automated Validation
→ Feedback
~~~

The goal is not to "have a CI server."

The goal is to make integration problems visible quickly.

---

# 5. Why Frequent Integration Matters

Frequent integration reduces the amount of unknown change accumulated between validations.

Smaller integration batches are usually easier to:

- review
- test
- debug
- revert
- understand

CI is a feedback practice.

---

# 6. Why CD Exists

Even when code builds successfully, organizations still need a safe way to move software through environments toward users.

Continuous delivery addresses:

~~~text
How do we keep software in a releasable state?
~~~

Continuous deployment addresses:

~~~text
How can validated change reach production automatically?
~~~

---

# 7. Continuous Delivery

Continuous delivery means software is kept deployable through a repeatable delivery process.

A provider-neutral definition should focus on **releasability and repeatability**. Some delivery systems retain an explicit production approval or release decision; continuous deployment removes that explicit production promotion step when all required automated conditions are satisfied.

~~~text
Code
→ Build
→ Test
→ Package
→ Validate
→ Ready for Production
~~~

Production release may still require a deliberate decision.

---

# 8. Continuous Deployment

Continuous deployment means a change that passes required validations can proceed automatically to production.

~~~text
Change
→ Required Validation
→ Production
~~~

This is not appropriate for every environment or business.

Regulation, risk, architecture, data changes, and operational maturity all matter.

---

# 9. CI vs Continuous Delivery vs Continuous Deployment

A useful distinction:

~~~text
CI
→ integrate and validate frequently

Continuous Delivery
→ keep software releasable

Continuous Deployment
→ automatically release validated change to production
~~~

These concepts are related but not identical.

---

# 10. Pipeline Mental Model

A pipeline is a structured sequence of automated delivery activities.

~~~text
Source
→ Build
→ Test
→ Package
→ Deploy
→ Verify
~~~

A pipeline is a mechanism.

Delivery quality depends on what the pipeline proves and how safely it handles change.

---

# 11. Workflow / Pipeline / Job / Step

Terminology differs across tools, but a useful hierarchy is:

~~~text
Workflow / Pipeline
└── Job / Stage
    └── Step / Task
~~~

Do not memorize vendor vocabulary before understanding the model.

---

# 12. Trigger

A pipeline may start because of:

- commit
- pull request
- merge
- tag
- release
- schedule
- manual request
- external event

The trigger should match the engineering intent.

---

# 13. Source Checkout

The pipeline needs a known source revision.

Important questions:

- which commit?
- which branch?
- which tag?
- was the source reviewed?
- can the build be reproduced from that revision?

Traceability begins here.

---

# 14. Build

The build converts source into a runnable or distributable form.

Examples:

- binary
- package
- container image
- archive
- static site bundle

A successful build proves only that build requirements succeeded.

It does not prove production safety.

---

# 15. Validation Layers

Validation may include:

- formatting
- linting
- unit tests
- integration tests
- API tests
- dependency checks
- security scans
- policy checks
- infrastructure validation

Different checks answer different questions.

---

# 16. Fast Feedback vs Deep Validation

Not every check needs to run at the same point.

A useful model:

~~~text
Fast checks early
→ deeper checks later
→ expensive checks only when justified
~~~

Slow feedback increases queueing and encourages bypass behavior.

---

# 17. Quality Gate

A quality gate determines whether a change may continue.

Examples:

~~~text
Tests pass?
Security threshold met?
Policy satisfied?
Review approved?
~~~

A gate should protect a meaningful risk, not simply add process.

---

# 18. Artifact

An artifact is the output produced by a build.

Examples:

- container image
- JAR
- ZIP
- package
- binary

A good delivery system can answer:

> Which artifact is running in production?

---

# 19. Build Once, Promote

A strong mental model is:

~~~text
Build once
→ validate artifact
→ promote same identified artifact
→ deploy to later environments
~~~

Why?

Because rebuilding per environment can produce different outputs.

This reduces **artifact uncertainty**, but does not eliminate environment-specific differences in configuration, infrastructure, data, dependencies, or traffic.

---

# 20. Artifact Immutability

An immutable artifact should not change after creation.

Conceptually:

~~~text
Artifact v1
= same bits in test
= same bits in staging
= same bits in production
~~~

Configuration may differ by environment, but the promoted artifact should remain identifiable.

---

# 21. Artifact Repository

Artifact repositories store build outputs.

They support:

- versioning
- retention
- provenance
- promotion
- controlled access

The repository becomes part of the software delivery supply chain.

---

# 22. Environment Promotion

A change may move through:

~~~text
Development
→ Test
→ Staging
→ Production
~~~

Promotion means the same approved artifact advances through increasingly critical environments.

---

# 23. Promotion vs Rebuild

Promotion:

~~~text
same artifact
→ next environment
~~~

Rebuild:

~~~text
same source
→ new artifact
→ next environment
~~~

Promotion reduces uncertainty about what was tested.

---

# 24. Environment-Specific Configuration

The artifact may be the same while configuration differs.

Examples:

- endpoints
- credentials
- feature flags
- scaling values
- resource limits

Configuration should remain controlled and traceable.

---

# 25. Deployment

Deployment places a software version into an environment.

A deployment may occur without users immediately receiving the new behavior.

That distinction matters.

---

# 26. Release

Release means making functionality available to users.

Deployment and release can be separated through mechanisms such as feature flags.

~~~text
Deploy code
≠
Enable feature
~~~

---

# 27. Feature Flags — Preview

Feature flags allow behavior to be enabled or disabled independently from deployment.

Benefits may include:

- gradual rollout
- controlled exposure
- faster disablement

Risks include:

- stale flags
- hidden complexity
- inconsistent behavior

Deep implementation comes later.

---

# 28. Deployment Strategy — Preview

Common strategies include:

- rolling
- blue/green
- canary
- recreate

At D00 level, retain:

> Deployment strategy controls exposure and blast radius.

Deep implementation belongs to later domains.

---

# 29. Approval Gates

Some environments require human approval.

An approval can be valuable when it represents a real risk decision.

It becomes harmful when it is only ritual waiting.

---

# 30. Automated Policy Gates

Some decisions can be automated.

Examples:

- approved dependency policy
- infrastructure policy
- required tests
- vulnerability threshold
- environment rule

Automation should encode known rules.

Human judgment should remain where context matters.

---

# 31. Pipeline Feedback

A pipeline is also a feedback system.

Useful feedback includes:

- what failed
- where it failed
- why it failed
- which revision failed
- which artifact was produced
- which environment changed
- who approved it
- what happened after deployment

---

# 32. Failure Handling

Pipeline failure should be understandable.

A useful response model:

~~~text
Failure
→ classify
→ preserve evidence
→ stop unsafe continuation
→ recover or retry safely
~~~

Blind reruns can hide real defects.

---

# 33. Retry

Retries can help with transient failures.

But retries can also hide:

- flaky tests
- unreliable infrastructure
- rate limits
- race conditions
- dependency problems

A retry policy should distinguish transient failure from deterministic failure.

---

# 34. Flaky Tests

A flaky test sometimes passes and sometimes fails without meaningful code change.

Effects include:

- lost trust
- rerun culture
- slower delivery
- hidden defects

CI becomes weak when engineers stop believing its signals.

---

# 35. Pipeline Concurrency

Multiple pipeline runs may happen at the same time.

Questions:

- can two deployments target the same environment?
- should old runs be cancelled?
- can two releases mutate shared state?
- are locks needed?
- can jobs safely run in parallel?

Concurrency design affects delivery safety.

---

# 36. Runner / Agent / Executor

The pipeline needs compute to execute jobs.

Different systems call this:

- runner
- agent
- executor
- worker

The mental model is:

~~~text
Pipeline Definition
→ Execution Worker
→ Commands / Build / Tests
~~~

---

# 37. Hosted vs Self-Hosted Execution

Hosted workers reduce operational burden.

Self-hosted workers provide more network/control flexibility.

Trade-offs include:

- security
- isolation
- maintenance
- performance
- network access
- cost

---

# 38. Caching

Caching can accelerate builds.

Examples:

- dependencies
- compiled layers
- container layers

But stale or poisoned caches can create confusing behavior.

A cache is an optimization mechanism, **not the canonical release artifact**.

A faster pipeline is not valuable if it becomes nondeterministic.

---

# 39. Secrets in CI/CD

Pipelines often require credentials.

Secrets should not be:

- hardcoded in source
- printed in logs
- embedded in artifacts

Better models include short-lived credentials, secret stores, protected variables, and identity-based access where supported.

Where a platform supports workload identity federation/OIDC, a pipeline can obtain scoped short-lived credentials instead of storing a long-lived cloud credential.

---

# 40. Least Privilege

A deployment job should have only the permissions needed for its task.

A pipeline with broad administrator access has a large blast radius.

CI/CD security is partly identity architecture.

---

# 41. Environment Protection

Production may require stronger controls such as:

- restricted deploy permissions
- protected environments
- approvals
- branch/tag rules
- deployment windows
- policy checks

Controls should be proportional to risk.

---

# 42. Branch Protection

Branch protection can require:

- review
- passing checks
- signed or trusted changes
- restricted merge paths

The goal is to reduce unreviewed source changes reaching critical delivery paths.

---

# 43. Deployment Verification

A successful deployment command does not prove the service is healthy.

Post-deployment validation can include:

- health checks
- smoke tests
- metrics
- logs
- error rate
- latency
- SLO signals

---

# 44. Observability and CI/CD

Delivery events should be visible in production telemetry.

~~~text
Deployment
→ Change Marker
→ Metrics / Logs / Traces
→ Compare Before vs After
~~~

This improves diagnosis and incident correlation.

---

# 45. Rollback

Rollback returns to a previous known-good version or configuration.

Rollback is easier when:

- artifacts are immutable
- versions are known
- data compatibility is preserved
- deployment is reversible

Rollback is not always safe.

---

# 46. Roll Forward

Roll-forward corrects the problem with a new change.

It may be safer when:

- database/schema changes are not reversible
- state changed irreversibly
- the previous version is incompatible

Recovery strategy must match the failure mode.

---

# 47. Database Changes

Application delivery becomes harder when schema/data changes are involved.

Risks include:

- backward incompatibility
- long migrations
- locks
- partial completion
- rollback difficulty

At D00 level, retain:

> Application and data change must be designed together.

---

# 48. CI/CD and IaC

Application and infrastructure delivery often intersect.

~~~text
Application Pipeline
→ artifact

IaC Pipeline
→ environment / platform change
~~~

The two should coordinate where dependencies exist.

---

# 49. CI/CD vs GitOps

Push-based CI/CD often looks like:

~~~text
Pipeline
→ directly changes target environment
~~~

GitOps commonly looks like:

~~~text
Pipeline
→ updates desired state in Git
→ reconciler pulls and applies
~~~

They can work together.

They are not the same delivery model.

---

# 50. Supply Chain — Mental Model

Software delivery depends on more than source code.

~~~text
Source
→ Dependencies
→ Build System
→ Artifact
→ Repository
→ Deployment System
→ Runtime
~~~

Compromise at any stage can affect production.

Deep software supply-chain security comes later.

---

# 51. Traceability

A mature delivery system should help answer:

- which commit?
- which build?
- which artifact?
- which tests?
- which approval?
- which deployment?
- which environment?
- which production outcome?

Traceability supports debugging, audit, and recovery.

---

# 52. Senior Engineer Perspective

A senior engineer asks:

- where does the pipeline wait?
- what feedback is slow?
- which test is unreliable?
- which artifact is promoted?
- can the build be reproduced?
- what is the deployment blast radius?
- can we recover?
- what evidence proves success?

The focus is system flow, not YAML syntax.

---

# 53. SRE Perspective

An SRE asks:

- what change reached production?
- did SLOs degrade?
- how quickly was failure detected?
- was rollback/failover safe?
- are alerts correlated with deployments?
- is the pipeline itself reliable?
- how much delivery toil exists?

CI/CD is part of production reliability.

---

# 54. Architect Perspective

An architect asks:

- what delivery model fits the system?
- how are artifacts managed?
- which environments exist?
- what promotion model is used?
- where are approvals justified?
- what deployment strategy limits blast radius?
- how are credentials isolated?
- how are application and IaC changes coordinated?
- where does GitOps fit?
- what level of automation is safe?

Delivery architecture is part of system architecture.

---

# 55. Common Beginner Mistakes

## Mistake 1

"CI/CD means Jenkins."

No. Jenkins is one implementation tool.

## Mistake 2

"Passing tests means the change is production-safe."

Tests provide evidence, not certainty.

## Mistake 3

"We rebuild separately for every environment."

This increases artifact uncertainty.

## Mistake 4

"Deployment and release are the same."

They can be separated.

## Mistake 5

"Retry until green."

Blind retries can hide flaky or real failures.

## Mistake 6

"Production approval makes delivery safe."

An approval without evidence may only add waiting.

## Mistake 7

"Rollback always works."

Data and compatibility changes may make rollback unsafe.

## Mistake 8

"GitOps replaces CI."

CI and GitOps solve overlapping but different parts of delivery.

---

# 56. Five-Level Explanation

## L1 — Foundation

CI/CD automates how software changes are integrated, validated, packaged, and moved toward production.

## L2 — Engineer

CI/CD combines source triggers, builds, tests, artifacts, environment promotion, deployment, and feedback.

## L3 — Senior Engineer

A strong delivery system optimizes fast feedback, reproducibility, artifact integrity, safe promotion, recovery, and traceability.

## L4 — SRE

CI/CD must be evaluated against reliability, SLO impact, change failure, recovery speed, deployment observability, and operational toil.

## L5 — Architect

CI/CD architecture aligns source control, artifact strategy, environment model, deployment risk, credentials, policy, recovery, IaC, GitOps, and organizational ownership.

---

# 57. What You Must Retain

Before moving on, retain:

- CI is frequent integration plus fast validation
- continuous delivery and continuous deployment are different
- a pipeline is a mechanism, not the goal
- build success is not production safety
- fast feedback matters
- different validation layers answer different questions
- build once/promote reduces artifact uncertainty
- artifacts should remain identifiable and preferably immutable
- deployment and release can be separated
- feature flags can reduce release coupling
- gates should protect meaningful risk
- retries can hide failures
- flaky tests destroy trust
- pipeline concurrency needs design
- runners execute pipeline jobs and have security implications
- caching trades speed against determinism risk
- secrets and permissions require least privilege
- successful deployment does not prove service health
- deployment events should be observable
- rollback is not always safe
- roll-forward may be required
- application and data changes must be designed together
- CI/CD and IaC can coordinate
- CI/CD and GitOps are not identical
- delivery traceability is critical

---

# 58. Practical Package — Next Layer

The practical package should include safe, provider-neutral exercises such as:

- trace one change from commit to production
- classify pipeline stages and feedback points
- compare build-once/promote vs rebuild-per-environment
- review a hypothetical failing pipeline and identify root causes
- classify retryable vs non-retryable failures
- design artifact/version traceability
- evaluate approval gates and environment protections
- design a rollback/roll-forward decision tree

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 59. Assessment Package — Pending

The assessment should test:

- CI/CD definitions
- triggers
- build and validation
- artifacts
- promotion
- deployment vs release
- feature flags
- gates
- failure handling
- retries/flaky tests
- runners
- concurrency
- caching
- secrets/permissions
- environment protection
- deployment verification
- observability
- rollback/roll-forward
- database change risk
- CI/CD with IaC
- CI/CD vs GitOps
- Senior/SRE/Architect reasoning

---

# 60. Visual Package — Pending

The visual package should include:

1. CI vs Continuous Delivery vs Continuous Deployment
2. Source → Build → Validate → Artifact → Promote → Deploy
3. Build Once / Promote Same Artifact
4. Pipeline Feedback & Failure Loop
5. Deployment vs Release
6. CI/CD + IaC + GitOps Relationship

---

# 61. What Comes Next

After D00-T009 is completed, continue to:

## 00.10 — Containers & Orchestration Mental Model

That topic will connect software delivery and infrastructure automation to containers, images, runtime isolation, orchestration, scheduling, and platform behavior.

---

# 62. Sources & Evidence

Planned authoritative source families:

- AWS CI/CD and deployment guidance
- Microsoft DevOps / Azure Pipelines guidance
- GitHub Actions documentation
- GitLab CI/CD documentation
- Jenkins documentation where useful
- Google Cloud delivery guidance
- OpenGitOps principles
- SLSA / software supply-chain guidance
- official platform guidance for artifacts, environments, and deployment verification

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification: complete
- practical package: pending
- assessment package: pending
- visual package: pending

Detailed verification record:

- [D00-T009 Source Verification](../../../../docs/sources/D00/D00-T009-source-verification.md)

Verified nuances:

- continuous delivery is best taught provider-neutrally as maintaining a releasable state; production may still require a deliberate decision
- continuous deployment automatically promotes validated change through production
- build-once/promote reduces artifact uncertainty but does not make environments identical
- artifacts and caches serve different purposes
- passing checks provides evidence rather than a guarantee of production safety
- approval gates are valuable only when they represent meaningful risk decisions
- concurrency policy is part of delivery safety
- runner trust/ownership changes the security model
- short-lived OIDC/federated credentials can reduce reliance on stored long-lived secrets
- deployment success does not by itself prove service health
- GitOps and CI/CD are complementary but distinct control models
- SLSA provenance strengthens artifact traceability and integrity evidence

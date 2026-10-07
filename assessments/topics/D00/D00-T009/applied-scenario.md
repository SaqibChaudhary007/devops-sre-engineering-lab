# D00-T009 — Applied Delivery Scenario

## Scenario

A customer-facing payments service uses the following delivery path:

~~~text
Commit
→ Pull Request
→ Build
→ Unit Tests
→ Integration Tests
→ Security Scan
→ Package
→ Staging
→ Production Approval
→ Production Deploy
→ Health Verification
~~~

Current problems:

~~~text
- builds take 28 minutes
- unit tests are fast, but integration tests are flaky
- engineers frequently rerun failed tests until they pass
- the service is rebuilt independently for staging and production
- the staging artifact and production artifact can have different dependency patch versions
- two production deployments can run at the same time
- the production runner has broad administrator credentials
- production approval is usually a quick click with little evidence
- the pipeline marks deployment success when the deployment command exits 0
- p95 latency increased after two recent releases, but deployment events were not visible in monitoring
- rollback failed once because a database migration was not backward compatible
- teams say GitOps will replace CI next quarter
~~~

## Task 1 — Map the Delivery System

Map:

~~~text
Source
→ Validation
→ Artifact
→ Promotion
→ Deployment
→ Verification
→ Runtime Feedback
~~~

Identify where evidence is missing.

## Task 2 — CI Reasoning

Explain which behaviors weaken continuous integration:

- long feedback time
- flaky integration tests
- rerun-until-green
- accumulated uncertainty

Propose the highest-value improvements first.

## Task 3 — Artifact Strategy

Compare:

~~~text
Rebuild for Staging
→ Artifact A

Rebuild for Production
→ Artifact B
~~~

with:

~~~text
Build Once
→ Artifact X
→ Staging
→ Production
~~~

Explain why the second model reduces artifact uncertainty.

## Task 4 — Artifact vs Cache

Define which of these belong to trusted release flow:

- dependency cache
- container image digest
- test report
- package-manager cache
- build provenance
- release ZIP

Explain why caches must not become release identity.

## Task 5 — Concurrency

Two production runs start five minutes apart.

Design a production concurrency policy.

Include:

- one active deployment per production target
- stale-run handling
- queue/cancel behavior
- shared-state awareness

Explain what concurrency policy still cannot guarantee.

## Task 6 — Retry / Flaky Test

An integration test fails once and passes on rerun.

Decide whether to:

- retry automatically
- retry after review
- block
- quarantine test
- investigate dependency

Explain the evidence you need before choosing.

## Task 7 — Approval Gate

Replace the current "click approve" behavior with a meaningful approval checklist.

Include:

- artifact identity
- required validations
- active deployment status
- blast radius
- rollback/roll-forward path
- production health signals

## Task 8 — Runner / Credential Security

The production runner has broad administrator credentials.

Explain:

- blast-radius risk
- runner compromise risk
- why self-hosted execution changes the trust model
- how least privilege and short-lived credentials improve safety

## Task 9 — Deployment Verification

The deployment command exits successfully.

Define a better post-deployment verification gate using:

- version consistency
- health
- errors
- latency
- dependency health
- SLO indicators

## Task 10 — Observability / Change Correlation

Design change markers containing:

~~~text
Commit SHA
Build ID
Artifact ID
Pipeline Run
Environment
Deploy Start/End
Result
~~~

Explain how these improve incident diagnosis.

## Task 11 — Rollback / Roll Forward

A release includes an incompatible database migration.

Explain why:

> "Deploy the previous version"

may fail.

Choose the likely recovery approach from:

~~~text
Rollback
Roll Forward
Failover
Restore
Feature Disablement
Manual Investigation
~~~

Defend the choice.

## Task 12 — GitOps Relationship

Evaluate:

> "Once we adopt GitOps, we no longer need CI."

Explain what CI still does and what GitOps adds.

## Task 13 — Senior Engineer Response

Use:

~~~text
Impact
→ Delivery Timeline
→ Source Revision
→ Artifact Identity
→ Test Evidence
→ Active Runs
→ Environment State
→ Runtime Signals
→ Recovery
→ Prevention
~~~

## Task 14 — SRE View

Connect delivery design to:

- change fail rate
- failed deployment recovery time
- SLOs
- alerting
- deployment markers
- operational toil

## Task 15 — Architect View

Design a safer target model covering:

- trigger strategy
- fast vs deep validation
- artifact repository
- build-once/promote
- concurrency
- environment protections
- runner trust
- credentials
- deployment strategy
- post-deploy verification
- rollback/roll-forward
- CI + IaC + GitOps relationship

## Success Standard

A strong answer treats CI/CD as a traceable, evidence-driven delivery system.

It should identify:

- slow/flaky feedback
- artifact uncertainty
- concurrency conflicts
- weak approvals
- excessive credential blast radius
- missing deployment verification
- missing change correlation
- rollback limitations
- incorrect CI/GitOps assumptions

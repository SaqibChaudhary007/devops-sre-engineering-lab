---
id: EXP-D00-014
domain: D00
topics:
  - D00-T009
level: L2-L3
type: experiment
status: draft
estimated_time: 55-75m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-014 — Diagnose Pipeline Failure, Retry, Concurrency, and Recovery

## Objective

Practice diagnosing a hypothetical CI/CD pipeline using evidence rather than blindly rerunning jobs.

## Safety

This is a local reasoning exercise only.

Do not execute production deployments or use privileged credentials.

## Scenario

A production delivery pipeline contains:

~~~text
Trigger
→ Build
→ Unit Tests
→ Integration Tests
→ Security Check
→ Package
→ Staging Deploy
→ Smoke Test
→ Production Approval
→ Production Deploy
→ Health Verification
~~~

Observed events:

~~~text
Run 101:
- build passed
- unit tests passed
- integration tests failed once, passed on rerun
- staging deploy passed

Run 102:
- started 2 minutes later
- used the same production target
- production approval granted first
- production deployment began while Run 101 was still active

Run 101:
- production deploy failed halfway
- automatic retry started

Run 102:
- production deploy also started
- health verification reported mixed versions
- latency increased
~~~

## 1. Build a Timeline

Create a chronological timeline for Run 101 and Run 102.

Mark:

- deterministic events
- transient-looking events
- concurrency events
- retry events
- production impact

## 2. Classify Failures

Classify each failure as one of:

~~~text
Likely Deterministic
Likely Transient
Flaky / Untrusted Signal
Concurrency Conflict
Unknown / Need More Evidence
~~~

Include:

- integration test failure
- partial production deployment
- mixed-version health result
- latency increase

## 3. Retry Decision

For each failure, decide:

~~~text
Retry Automatically
Retry Manually After Review
Do Not Retry
Cancel Competing Run
Investigate First
~~~

Explain why blind retry can make diagnosis worse.

## 4. Flaky Test Reasoning

The integration test failed once and passed on rerun.

Ask:

- is the test flaky?
- is the dependency unstable?
- did rerun mask a real problem?
- what evidence is needed?

Explain why "rerun until green" reduces trust.

## 5. Concurrency Control

Design a concurrency rule for production.

Consider:

- one active deployment per production environment
- canceling stale runs
- queueing newer runs
- protecting shared mutable state

Explain what concurrency control can and cannot guarantee.

## 6. Approval Gate Review

Run 102 received approval while Run 101 was still active.

Explain why approval should consider current environment state.

A good approval decision should include:

- active deployments
- artifact identity
- known incidents
- rollback/recovery readiness
- deployment target status

## 7. Deployment Verification

The deployment command partially succeeded.

Explain why "job succeeded" and "service healthy" are different outcomes.

Define post-deployment checks using:

- health
- error rate
- latency
- version consistency
- dependency health

## 8. Rollback vs Roll Forward

Assume the environment now contains mixed versions.

Choose among:

~~~text
Rollback
Roll Forward
Pause Traffic
Failover
Manual Investigation
~~~

Explain what evidence determines the safest response.

## 9. Change Correlation

Design change markers:

~~~text
Run ID
Artifact ID
Environment
Start Time
End Time
Result
Commit SHA
~~~

Explain how they help incident diagnosis.

## 10. Runner / Credential Risk

Assume a self-hosted production runner has broad administrator credentials.

Identify risks:

- credential exposure
- lateral movement
- persistent compromise
- oversized blast radius

Propose safer principles:

- least privilege
- ephemeral/isolated runners where practical
- short-lived credentials
- protected environments

## 11. Senior Engineer Connection

Use this troubleshooting sequence:

~~~text
Impact
→ Timeline
→ Active Runs
→ Artifact Identity
→ Failure Evidence
→ Concurrency
→ Retry History
→ Environment State
→ Recovery
→ Prevention
~~~

## 12. SRE Connection

Connect the delivery incident to:

- SLO impact
- alerting
- deployment markers
- failed deployment recovery time
- change fail rate
- operational toil

## 13. Architect Connection

Design guardrails for:

- concurrency
- retries
- protected production environments
- runner trust
- credentials
- post-deploy verification
- automatic rollback conditions

## Validation Checklist

- [ ] Built the timeline
- [ ] Classified failures
- [ ] Designed retry decisions
- [ ] Explained flaky-test risk
- [ ] Designed concurrency controls
- [ ] Reviewed approval quality
- [ ] Defined deployment verification
- [ ] Chose a recovery strategy
- [ ] Designed change markers
- [ ] Addressed runner and credential risk

## Teach-Back

Explain:

> "A failed pipeline should produce evidence, not a reflexive rerun."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

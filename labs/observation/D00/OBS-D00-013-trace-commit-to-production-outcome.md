---
id: OBS-D00-013
domain: D00
topics:
  - D00-T009
level: L1-L2
type: observation
status: draft
estimated_time: 40-55m
environment:
  - Local workstation
  - Text editor or notebook
evidence_status:
  - DRAFT
---

# OBS-D00-013 — Trace a Change from Commit to Production Outcome

## Objective

Map one software change through a complete CI/CD delivery path and identify where evidence, artifacts, approvals, environments, and feedback are produced.

## Why This Matters

A pipeline is not just a sequence of tasks.

A mature delivery system should let you answer:

~~~text
Which commit?
Which build?
Which artifact?
Which tests?
Which approval?
Which environment?
Which deployment?
Which production outcome?
~~~

## Safety

This is a documentation and reasoning exercise.

No production credentials, deployment access, or cloud account is required.

## Scenario

Use this hypothetical change:

> Add a new API field named preferred_language to a customer profile response.

Assume the organization uses:

- Git-based source control
- pull-request review
- automated CI
- an artifact repository
- development
- staging
- production
- a production approval
- application monitoring

## 1. Draw the Delivery Path

Create:

~~~text
Commit
→ Pull Request
→ Review
→ Build
→ Unit Tests
→ Integration Tests
→ Package
→ Artifact Repository
→ Staging
→ Approval
→ Production
→ Verification
→ Observe
→ Learn
~~~

## 2. Identify Evidence at Each Stage

Complete:

| Stage | Input | Output | Evidence Produced | Failure Signal | Owner |
|---|---|---|---|---|---|
| Commit | | | | | |
| Review | | | | | |
| Build | | | | | |
| Unit Test | | | | | |
| Integration Test | | | | | |
| Package | | | | | |
| Artifact Store | | | | | |
| Staging Deploy | | | | | |
| Production Approval | | | | | |
| Production Deploy | | | | | |
| Verification | | | | | |
| Observe | | | | | |

## 3. Traceability Chain

Create one traceability chain:

~~~text
Commit SHA
→ Build ID
→ Artifact Version / Digest
→ Staging Deployment
→ Production Deployment
→ Change Marker
→ Runtime Metrics
~~~

Explain what breaks if one link is missing.

## 4. Feedback Classification

Classify each signal as:

~~~text
Fast
Medium
Slow
~~~

Signals:

- lint failure
- unit test failure
- integration test failure
- staging smoke test failure
- production health-check failure
- latency regression
- user complaint

## 5. Deployment vs Release

Assume the code is deployed with a feature flag disabled.

Explain:

~~~text
Deployment
≠
Release
~~~

Then describe what event actually releases the feature to users.

## 6. Approval Quality

Evaluate this approval question:

> "Can I click approve?"

Replace it with better questions:

- what changed?
- what evidence exists?
- what is the blast radius?
- what is the rollback/roll-forward path?
- what production signal will confirm health?

## 7. Production Feedback

Assume the deployment succeeds, but p95 latency increases by 35%.

Explain:

- why the deployment command can still be "successful"
- what post-deployment verification should catch
- what signal should link back to the change
- who should own the learning loop

## 8. Senior Engineer Connection

A senior engineer should be able to trace:

~~~text
Source
→ Artifact
→ Environment
→ Runtime Outcome
~~~

without guessing.

## 9. SRE Connection

Connect the deployment to:

- SLOs
- latency
- errors
- change markers
- rollback/failover
- incident correlation

## 10. Architect Connection

Ask:

- which evidence must be retained?
- which environments need stronger protections?
- where should approvals exist?
- what should be automated?
- what must remain observable after deploy?

## Validation Checklist

- [ ] Mapped the complete delivery path
- [ ] Identified evidence at each stage
- [ ] Built a traceability chain
- [ ] Classified feedback speed
- [ ] Explained deployment vs release
- [ ] Improved approval questions
- [ ] Connected production telemetry to the deployment

## Teach-Back

Explain:

> "A CI/CD pipeline is a traceable feedback system, not just automation."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completing and reviewing the exercise.

---
id: EXP-D00-013
domain: D00
topics:
  - D00-T009
level: L2-L3
type: experiment
status: draft
estimated_time: 50-70m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-013 — Build Once, Promote, Cache, and Artifact Integrity

## Objective

Compare two delivery models and reason about artifact identity, rebuild risk, caching, provenance, and environment promotion.

## Safety

This is a local reasoning exercise only.

No real build system, artifact repository, or deployment target is required.

## Scenario

A team delivers one service to development, staging, and production.

Compare two models.

### Model A — Rebuild per Environment

~~~text
Commit A
→ Build for Dev
→ Artifact A1

Commit A
→ Build for Staging
→ Artifact A2

Commit A
→ Build for Production
→ Artifact A3
~~~

### Model B — Build Once and Promote

~~~text
Commit A
→ Build Once
→ Artifact B1
→ Dev
→ Staging
→ Production
~~~

Assume dependency resolution can produce different patch versions if not pinned.

## 1. Artifact Identity

For each model, answer:

- how many artifacts exist?
- which artifact was actually tested?
- which artifact reached production?
- how easy is it to prove that production runs what staging validated?

## 2. Rebuild Risk

List reasons two builds from the same source revision might differ:

- dependency resolution
- build-tool version
- base image change
- environment variables
- timestamps/metadata
- external package repository changes

Explain why identical source does not automatically mean identical artifact.

## 3. Build Once / Promote

Explain why promoting the same identified artifact reduces uncertainty.

Also explain what it does **not** guarantee.

Discuss:

- environment configuration
- infrastructure differences
- runtime dependencies
- traffic
- data

## 4. Artifact vs Cache

Classify each item as:

~~~text
Release Artifact
Cache
Build Input
Build Metadata
~~~

Items:

1. container image tagged with immutable digest
2. dependency download cache
3. compiled binary
4. test report
5. package-manager cache
6. source commit
7. build provenance record
8. ZIP release package

Explain why a cache should not be treated as the canonical production artifact.

## 5. Immutability

Assume:

~~~text
artifact:v1
~~~

is overwritten after staging validation.

Explain:

- why the tag is now ambiguous
- why production traceability breaks
- why immutable identity/digest/version matters

## 6. Provenance

Build a minimal provenance chain:

~~~text
Source Revision
→ Build Process
→ Artifact Identifier
→ Provenance Record
→ Deployment
~~~

Explain what provenance can prove and what it cannot prove.

## 7. Environment Promotion

Create a promotion checklist:

- artifact identity known
- required tests passed
- security/policy checks passed
- environment-specific configuration reviewed
- deployment permissions valid
- recovery strategy understood

## 8. Cost / Speed Trade-Off

Model A performs three builds.

Model B performs one build and three deployments.

Discuss:

- build cost
- queue time
- reproducibility
- artifact certainty
- storage

Do not assume build-once is always operationally simpler for every software type.

## 9. Senior Engineer Connection

Explain why:

> "Same commit"

is weaker evidence than:

> "Same verified artifact."

## 10. SRE Connection

Explain how immutable artifact identity helps incident response.

## 11. Architect Connection

Decide:

- where artifacts are stored
- retention policy
- who can overwrite/delete
- whether signatures/provenance are required
- how environments consume artifacts

## Validation Checklist

- [ ] Compared rebuild-per-environment vs promote-same-artifact
- [ ] Identified rebuild variability
- [ ] Distinguished artifact from cache
- [ ] Explained artifact immutability
- [ ] Built a provenance chain
- [ ] Designed a promotion checklist
- [ ] Connected artifact identity to incident response

## Teach-Back

Explain:

> "Build once and promote the same identified artifact reduces uncertainty, but runtime environments can still differ."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

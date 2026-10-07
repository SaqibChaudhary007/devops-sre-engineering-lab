---
id: OBS-D00-019
domain: D00
topics:
  - D00-T015
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# OBS-D00-019 — Map Assets, Threats, Trust Boundaries, and Controls

## Objective

Build a safe, provider-neutral security map for a sample service without performing any offensive testing.

## Why This Matters

Security decisions are stronger when they start from assets, trust boundaries, identities, and realistic failure modes instead of adding controls at random.

## Safety

This is a reasoning exercise only.

Do not probe public systems, bypass controls, test real credentials, exploit vulnerabilities, or modify production infrastructure.

## Scenario

Use this simple application:

~~~text
Customer
→ Public Web/API
→ Application Service
→ Database
→ Queue
→ Worker

Developer
→ Source Repository
→ CI/CD Pipeline
→ Artifact Registry
→ Production
~~~

## 1. Identify Assets

Classify assets such as:

- customer data
- account identities
- application source
- deployment credentials
- build artifacts
- production configuration
- service availability
- audit evidence

Explain why security starts with what matters.

## 2. Identify Trust Boundaries

Mark where trust changes, for example:

~~~text
Internet
→ Public Edge

Developer
→ Source Repository

CI/CD
→ Artifact Registry

Deployment Pipeline
→ Production

Application
→ Database
~~~

Explain why each crossing requires an explicit decision.

## 3. Identify Threat Categories

Use safe conceptual categories only:

- stolen credential
- accidental misconfiguration
- excessive permission
- leaked secret
- untrusted artifact
- compromised dependency
- unauthorized change
- third-party outage or compromise

Do not describe exploitation procedures.

## 4. Identify Vulnerabilities / Weaknesses

For each threat, identify possible weaknesses such as:

- broad permissions
- hard-coded secret
- no audit trail
- insecure default
- no review gate
- unclear ownership
- unverified artifact
- unnecessary public exposure

## 5. Connect Risk

Use:

~~~text
Asset
+ Threat
+ Weakness
+ Exposure
+ Impact
→ Risk
~~~

Rank each risk qualitatively:

~~~text
Low
Medium
High
Needs More Context
~~~

Explain your reasoning rather than relying only on labels.

## 6. Map Preventive Controls

Possible controls:

- authentication
- authorization
- least privilege
- private-by-default configuration
- scoped identities
- encryption
- secret separation
- review/approval
- network segmentation
- signed or verified artifacts

## 7. Map Detective Controls

Possible evidence:

- login events
- authorization failures
- privilege changes
- secret access
- deployment approvals
- artifact-promotion events
- configuration changes

Explain why prevention without detection is incomplete.

## 8. Human vs Workload Identity

Classify:

- developer
- administrator
- CI/CD job
- application service
- background worker

Decide which should use human identity and which should use workload identity.

## 9. Authentication vs Authorization

For each actor, answer:

~~~text
How is identity established?
What is the actor allowed to do?
~~~

Explain why strong authentication does not justify broad permissions.

## 10. Least-Privilege Review

Use:

~~~text
Identity
→ Resource
→ Required Action
→ Required Scope
→ Required Duration
~~~

Review:

- developer
- CI/CD
- application
- worker
- database access

## 11. Blast-Radius Review

Ask:

- if one credential is compromised, what can it reach?
- can it change production?
- can it read customer data?
- can it publish artifacts?
- can it delete backups?
- can it affect multiple environments?

Suggest safe architectural ways to reduce blast radius.

## 12. Senior Engineer Connection

Use:

~~~text
Asset
→ Threat
→ Trust Boundary
→ Identity
→ Permission
→ Control
→ Evidence
→ Risk Reduction
~~~

## 13. SRE Connection

Connect security to:

- incident detection
- access audit
- recovery trust
- blast radius
- operational ownership

## 14. Architect Connection

Ask:

- which trust boundaries need stronger controls?
- where should identities be separated?
- what permissions should be time-bounded?
- which controls must be preventive vs detective?
- what must be required before production launch?

## Validation Checklist

- [ ] Identified assets
- [ ] Mapped trust boundaries
- [ ] Identified safe threat categories
- [ ] Identified weaknesses
- [ ] Ranked risks qualitatively
- [ ] Mapped preventive and detective controls
- [ ] Distinguished human/workload identity
- [ ] Distinguished authentication/authorization
- [ ] Performed a least-privilege review
- [ ] Reviewed blast radius

## Teach-Back

Explain:

> "Security engineering begins by understanding what matters, where trust changes, who or what is acting, what can go wrong, and which controls reduce meaningful risk."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

---
id: EXP-D00-025
domain: D00
topics:
  - D00-T015
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

# EXP-D00-025 — Identity, Least Privilege, Secrets, and Audit Review

## Objective

Practice security reasoning around human/workload identities, authentication vs authorization, least privilege, secrets lifecycle, time-bounded access, and auditability.

## Safety

This is a local reasoning exercise.

Do not test real credentials, bypass access controls, attempt privilege escalation, expose secrets, or modify production permissions.

## Scenario

A team currently operates like this:

~~~text
- all developers share one administrator account
- CI/CD uses a long-lived static credential
- application and worker use the same database credential
- database password is stored in a repository configuration file
- emergency access never expires
- secret rotation is manual and undocumented
- privilege changes are not audited
~~~

## 1. Separate Identities

Design distinct identities for:

- developer
- administrator
- CI/CD pipeline
- application service
- worker

Explain why shared identities weaken accountability and blast-radius control.

## 2. Authentication vs Authorization

For each identity, write:

~~~text
Authentication
→ how identity is established

Authorization
→ what actions/resources are permitted
~~~

Explain why these are separate decisions.

## 3. Least-Privilege Matrix

Build a table with:

~~~text
Identity
Resource
Required Action
Scope
Duration
Approval
Audit Evidence
~~~

Review whether any permission is broader than needed.

## 4. Time-Bounded Access

Redesign emergency access:

~~~text
Need
→ Approval
→ Temporary Grant
→ Audit
→ Expiry / Revocation
~~~

Explain why permanent emergency access creates unnecessary risk.

## 5. Secrets Classification

Classify:

- database password
- API token
- private key
- signing key
- certificate
- non-sensitive application setting

Use:

~~~text
Secret / Credential
Sensitive Operational Data
Ordinary Configuration
~~~

## 6. Secret Placement Review

Classify these storage locations:

- source repository
- container image
- pipeline variable store
- dedicated secrets system
- local plaintext notes
- version-controlled config file

Use:

~~~text
Unsafe
Needs Strong Controls
Appropriate Pattern
Depends on Context
~~~

Keep the reasoning conceptual and provider-neutral.

## 7. Secret Lifecycle

Design:

~~~text
Create
→ Store
→ Distribute
→ Use
→ Rotate
→ Revoke
→ Audit
~~~

For the database credential.

Explain which lifecycle stages are missing in the current scenario.

## 8. Short-Lived Credential Reasoning

Compare:

~~~text
Long-Lived Static Credential
vs
Short-Lived Scoped Credential
~~~

Discuss:

- exposure window
- scope
- issuance
- revocation
- monitoring
- operational complexity

Explain why short-lived does not automatically mean safe.

## 9. Separation of Duties

Design a safe release flow such as:

~~~text
Developer Proposes
→ Reviewer Approves
→ Pipeline Builds
→ Controlled Identity Deploys
→ Audit Records Change
~~~

Explain why concentrating every step in one identity can increase risk.

## 10. Audit Review

Define useful audit questions:

- who changed permission?
- who accessed the secret?
- which identity deployed?
- what resource changed?
- when did it happen?
- what was the result?

Explain why audit evidence supports both security and incident investigation.

## 11. Secure Defaults

Redesign new-service defaults around:

- private-by-default exposure
- minimal permissions
- no shared credentials
- audit enabled
- secret separation
- explicit ownership

Explain why secure defaults reduce dependence on perfect operator behavior.

## 12. Senior Engineer Connection

Use:

~~~text
Actor
→ Identity
→ Authentication
→ Authorization
→ Least Privilege
→ Secret Use
→ Audit
→ Review
~~~

## 13. SRE Connection

Connect identity/security controls to:

- emergency access
- incident response
- recovery
- on-call operations
- auditability
- blast radius

## 14. Architect Connection

Decide:

- how identities should be separated
- where temporary access is appropriate
- which permissions require approval
- which credentials should be rotated automatically
- what audit evidence is mandatory

## Validation Checklist

- [ ] Separated human/workload identities
- [ ] Distinguished authentication and authorization
- [ ] Built a least-privilege matrix
- [ ] Designed time-bounded emergency access
- [ ] Classified secrets
- [ ] Reviewed secret placement
- [ ] Designed a secret lifecycle
- [ ] Explained short-lived credential trade-offs
- [ ] Applied separation of duties
- [ ] Designed useful audit evidence
- [ ] Defined secure defaults

## Teach-Back

Explain:

> "Strong identity security connects authentication, authorization, least privilege, time-bounded access, secret lifecycle, and auditability."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

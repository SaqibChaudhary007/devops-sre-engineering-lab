---
id: D00-T015
domain: D00
title: Security Foundations
level:
  - L1
  - L2
  - L3
priority: P1
status: draft
estimated_time:
  theory: 6-8h
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
    - D00-T009
    - D00-T010
    - D00-T011
    - D00-T012
    - D00-T013
    - D00-T014
  recommended: []
evidence_status:
  - RESEARCHED
certifications: []
content_series:
  - How It Really Works
  - Why Does It Exist
  - Under the Hood
  - Five Levels
  - Production Room
  - Think Like SRE
  - Architecture With Saqib
---

# 00.15 — Security Foundations

## Start Here

You now understand how systems are built, distributed, operated, observed, and recovered.

The next question is:

> How do we reduce the chance that systems, identities, data, dependencies, or delivery paths are misused, compromised, exposed, or changed by the wrong actor?

That is the problem space of **security engineering**.

Security is not:

- one firewall
- one antivirus product
- a penetration test at the end
- only the security team's responsibility
- only authentication
- only encryption
- blocking every change
- eliminating all risk
- adding controls without understanding the asset or threat

The core mental model is:

~~~text
Asset
→ Threat
→ Trust Boundary
→ Control
→ Detection
→ Response
→ Recovery
→ Improvement
~~~

A second useful model is:

~~~text
Identity
→ Authentication
→ Authorization
→ Least Privilege
→ Audit
~~~

Security engineering reduces risk by understanding what must be protected, who or what can interact with it, where trust changes, what controls apply, how misuse is detected, and how the system recovers.

This D00 topic stays at the foundational mental-model level. Deep cryptography, network security, Kubernetes security, cloud IAM, application security, threat detection, vulnerability management, supply-chain security, secrets platforms, compliance engineering, and offensive security belong to later domains.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- security as risk management
- confidentiality
- integrity
- availability
- assets
- threats
- vulnerabilities
- exploits at a conceptual level
- likelihood
- impact
- risk
- threat actors
- attack surface
- trust boundaries
- authentication
- authorization
- identity
- machine identity
- human identity
- service identity
- least privilege
- separation of duties
- deny by default
- zero trust at a conceptual level
- secrets
- credentials
- keys
- certificates
- token concepts
- encryption at rest / in transit
- hashing at a conceptual level
- data classification
- data minimization
- logging and audit trails
- security monitoring
- vulnerability management preview
- patching
- secure configuration
- hardening
- dependency risk
- third-party risk
- software supply chain preview
- artifact integrity
- provenance preview
- CI/CD security preview
- infrastructure-as-code security preview
- container / Kubernetes security preview
- cloud shared responsibility connection
- network segmentation preview
- defense in depth
- secure defaults
- fail-safe defaults
- blast radius
- incident response connection
- backup / recovery security
- production readiness
- security ownership
- security trade-offs
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
- [00.09 — CI/CD Mental Model](../00-09-cicd-mental-model/README.md)
- [00.10 — Containers & Orchestration Mental Model](../00-10-containers-orchestration-mental-model/README.md)
- [00.11 — Distributed Systems Foundations](../00-11-distributed-systems-foundations/README.md)
- [00.12 — Reliability Engineering Foundations](../00-12-reliability-engineering-foundations/README.md)
- [00.13 — SRE Foundations](../00-13-sre-foundations/README.md)
- [00.14 — Observability Foundations](../00-14-observability-foundations/README.md)

You should already understand systems, dependencies, distributed trust, change pipelines, observability, incidents, blast radius, and recovery.

---

# 3. What Is Security Engineering?

Security engineering is the discipline of reducing the likelihood and impact of misuse, unauthorized access, data exposure, tampering, disruption, and compromise.

A practical model:

~~~text
What Matters?
→ What Can Go Wrong?
→ Who / What Can Cause It?
→ What Controls Reduce Risk?
→ How Will We Detect Failure?
→ How Will We Respond and Recover?
~~~

Security is fundamentally about managing risk, not eliminating all possible risk.

---

# 4. CIA Triad

A foundational model is:

~~~text
Confidentiality
Integrity
Availability
~~~

## Confidentiality

Information is accessible only to authorized identities.

## Integrity

Information and system state are accurate and changed only in authorized ways.

## Availability

Authorized users can access the system or data when needed.

These goals can conflict, so trade-offs matter.

---

# 5. Asset

An asset is something worth protecting.

Examples:

- customer data
- credentials
- production systems
- source code
- build artifacts
- signing keys
- business processes
- service availability
- reputation
- audit evidence

Security starts by identifying assets.

---

# 6. Threat

A threat is something capable of causing harm to an asset.

Examples conceptually:

- stolen credential
- malicious insider
- compromised dependency
- accidental misconfiguration
- destructive automation
- vulnerable service
- leaked secret
- unauthorized change

Threat does not automatically mean incident.

---

# 7. Vulnerability

A vulnerability is a weakness that can be used or triggered in a harmful way.

Examples:

- excessive permissions
- exposed secret
- insecure default
- unpatched component
- weak trust boundary
- missing validation

A vulnerability becomes important in context:

~~~text
Asset
+ Exposure
+ Threat
+ Impact
→ Risk
~~~

---

# 8. Risk

A simple mental model:

~~~text
Risk
≈ Likelihood × Impact
~~~

Real risk analysis can be more complex.

At D00 retain:

> Security decisions should prioritize meaningful risk rather than counting controls.

---

# 9. Threat Actor

A threat actor is a person, group, process, or compromised system that can cause harm.

Possible categories:

- external attacker
- malicious insider
- careless insider
- compromised account
- compromised dependency
- automated bot
- accidental operator action

Security must account for both malicious and accidental causes.

---

# 10. Attack Surface

Attack surface is the set of ways a system can be interacted with or reached.

Examples:

- public endpoints
- admin interfaces
- credentials
- APIs
- CI/CD systems
- dependencies
- management ports
- cloud consoles

More exposed capability usually means more security responsibility.

---

# 11. Reduce Attack Surface

Reducing attack surface can include:

- removing unused services
- disabling unnecessary access
- narrowing network exposure
- limiting permissions
- reducing secret distribution
- minimizing externally reachable interfaces

A simpler system is often easier to secure.

---

# 12. Trust Boundary

A trust boundary is where the level of trust changes.

Examples:

~~~text
Internet
→ Edge

User
→ Application

Application
→ Database

CI Runner
→ Production

Cloud Account A
→ Cloud Account B
~~~

Crossing a trust boundary should trigger explicit security decisions.

---

# 13. Identity

Identity answers:

> Who or what is acting?

Identities may represent:

- human users
- administrators
- services
- workloads
- CI/CD jobs
- devices
- machines

Security depends on trustworthy identity.

---

# 14. Authentication

Authentication answers:

> Can this identity prove who or what it claims to be?

Examples conceptually:

- password + second factor
- certificate
- workload identity
- short-lived token
- hardware-backed credential

Authentication does not decide what the identity is allowed to do.

---

# 15. Authorization

Authorization answers:

> What is this authenticated identity allowed to do?

Examples:

- read data
- deploy application
- restart service
- access secret
- create infrastructure
- approve release

Authentication and authorization are different.

---

# 16. Authentication vs Authorization

A simple model:

~~~text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
~~~

Both are required.

A strongly authenticated identity can still have dangerous authorization.

---

# 17. Least Privilege

Least privilege means granting only the permissions required for the task.

Avoid:

~~~text
Everyone
→ Admin
~~~

Prefer:

~~~text
Identity
→ Required Scope
→ Required Actions
→ Required Duration
~~~

Least privilege reduces blast radius.

---

# 18. Time-Bounded Access

Permissions that are needed temporarily should ideally not exist forever.

Conceptually:

~~~text
Need Access
→ Approve
→ Grant
→ Expire / Revoke
~~~

Long-lived unnecessary access creates risk.

---

# 19. Separation of Duties

Separation of duties avoids concentrating every critical action in one identity or process.

Examples:

- developer proposes change
- reviewer approves
- pipeline deploys
- audit trail records

This reduces accidental and malicious misuse.

---

# 20. Deny by Default

A secure default posture is:

~~~text
Not Explicitly Allowed
→ Denied
~~~

rather than:

~~~text
Allowed Unless Blocked
~~~

The exact implementation depends on the platform.

---

# 21. Zero Trust — Preview

Zero Trust is often summarized as:

> Never trust solely because of network location; verify identity, context, and policy.

At D00 retain:

- explicit identity
- least privilege
- continuous verification
- limited trust
- strong segmentation

Deep Zero Trust architecture comes later.

---

# 22. Human Identity vs Workload Identity

Humans and workloads should not share identity casually.

Humans may need:

- interactive login
- MFA
- approval
- role-based permissions

Workloads may need:

- machine identity
- short-lived credentials
- scoped permissions
- automated rotation

Identity type should match the actor.

---

# 23. Credential

A credential helps prove identity.

Examples:

- password
- API key
- token
- certificate
- private key

Credentials are sensitive assets.

---

# 24. Secret

A secret is sensitive information that grants access or protects another sensitive operation.

Examples:

- database password
- API token
- private key
- signing key
- encryption key

Secrets should not be treated as normal configuration.

---

# 25. Secret Lifecycle

A useful model:

~~~text
Create
→ Store
→ Distribute
→ Use
→ Rotate
→ Revoke
→ Audit
~~~

Security problems often occur in the lifecycle, not only in storage.

---

# 26. Hard-Coded Secrets

Hard-coding secrets into:

- source code
- container images
- scripts
- configuration committed to Git

creates long-lived exposure and difficult rotation.

At D00 retain:

> Separate secret material from code and version-controlled configuration.

---

# 27. Short-Lived Credentials

Short-lived credentials reduce the time window in which a stolen credential remains useful.

Conceptually:

~~~text
Long-Lived Static Secret
→ Larger Exposure Window

Short-Lived Credential
→ Smaller Exposure Window
~~~

Short-lived does not mean automatically safe; scope and issuance still matter.

---

# 28. Certificates — Preview

Certificates can bind identity information to cryptographic keys.

They may support:

- service identity
- TLS
- mutual authentication

At D00, understand the role without deep PKI mechanics.

---

# 29. Encryption in Transit

Encryption in transit protects data while it moves across networks.

A common example is TLS.

This reduces exposure to interception or tampering on the path.

---

# 30. Encryption at Rest

Encryption at rest protects stored data.

Examples:

- disk encryption
- database encryption
- object-storage encryption

Encryption does not replace access control.

---

# 31. Hashing — Preview

Hashing transforms input into a fixed-size value used for purposes such as:

- integrity checking
- content identity
- password-verification systems when combined with appropriate password-specific techniques

Hashing is not the same as reversible encryption.

---

# 32. Data Classification

Not all data needs the same controls.

Possible categories:

- public
- internal
- confidential
- highly sensitive

Classification helps drive:

- access
- logging
- encryption
- retention
- monitoring

---

# 33. Data Minimization

Collect only the data needed for the business or operational purpose.

Less sensitive data means:

- less exposure
- less retention risk
- simpler governance

This connects directly to observability telemetry design.

---

# 34. Security Logging and Audit Trail

Security-relevant activity should often leave trustworthy evidence.

Examples:

- login attempts
- privilege changes
- secret access
- deployment approvals
- policy changes
- administrative actions

Audit evidence should answer:

~~~text
Who / What
Did What
To Which Resource
When
From Where
With What Result
~~~

---

# 35. Security Monitoring

Security monitoring detects behavior that may indicate:

- unauthorized access
- unexpected privilege use
- abnormal configuration change
- suspicious credential use
- policy violation

Monitoring must still be actionable and contextual.

---

# 36. Detection Is Part of Security

Prevention alone is not enough.

A stronger model:

~~~text
Prevent
→ Detect
→ Contain
→ Recover
→ Learn
~~~

Security and reliability share this lifecycle.

---

# 37. Defense in Depth

Defense in depth uses multiple independent or complementary controls.

Example:

~~~text
Identity
+ Authorization
+ Network Boundary
+ Encryption
+ Audit
+ Monitoring
~~~

One control failing should not automatically expose everything.

---

# 38. Secure Defaults

Secure defaults reduce the chance that a new system begins in an unnecessarily exposed state.

Examples:

- minimal permissions
- private by default
- encryption enabled
- logging enabled
- unused features disabled

Defaults shape real-world risk.

---

# 39. Fail-Safe Defaults

When a security control cannot determine that an action is allowed, the safer default is usually denial.

Conceptually:

~~~text
Uncertain Permission
→ Deny
~~~

The exact implementation depends on business and availability requirements.

---

# 40. Secure Configuration

Configuration controls matter because many security failures come from insecure settings rather than broken cryptography.

Areas include:

- permissions
- public exposure
- debug mode
- anonymous access
- default credentials
- logging
- TLS requirements

Configuration should be reviewed and versioned where possible.

---

# 41. Hardening

Hardening reduces unnecessary capability and exposure.

Examples conceptually:

- remove unused services
- disable unused accounts
- limit open interfaces
- restrict privileges
- apply safe defaults

Hardening should be driven by the system's actual purpose.

---

# 42. Patching

Patching reduces exposure to known defects.

A useful model:

~~~text
Known Issue
→ Evaluate Risk
→ Test Fix
→ Deploy Safely
→ Validate
~~~

Security patching must balance urgency with operational safety.

---

# 43. Vulnerability Management — Preview

Vulnerability management includes:

- discovering weaknesses
- understanding exposure
- prioritizing risk
- remediating
- validating
- tracking exceptions

Do not prioritize only by severity score without asset and exposure context.

---

# 44. Dependency Risk

Modern systems rely on:

- libraries
- packages
- images
- base operating systems
- third-party APIs
- build tools

Every dependency extends the trust chain.

---

# 45. Third-Party Risk

An external dependency can affect:

- confidentiality
- integrity
- availability
- compliance
- supply chain

Ask:

- what access does it have?
- what data does it receive?
- what happens if it is compromised?
- what happens if it becomes unavailable?

---

# 46. Software Supply Chain — Preview

A simplified software supply-chain path is:

~~~text
Source
→ Dependency
→ Build
→ Artifact
→ Registry
→ Deployment
→ Runtime
~~~

Every stage can affect production trust.

Deep supply-chain security comes later.

---

# 47. Artifact Integrity

Artifact integrity asks:

> Is this the artifact we intended to build and deploy?

Useful concepts include:

- checksum/digest
- signature
- provenance
- controlled promotion

Deep implementation comes later.

---

# 48. Provenance — Preview

Provenance is evidence about where an artifact came from and how it was produced.

Conceptually:

~~~text
Source
+ Build Process
+ Identity
+ Artifact
→ Provenance Evidence
~~~

This supports trust in the delivery path.

---

# 49. CI/CD Security — Preview

CI/CD systems often hold powerful permissions.

Risks include:

- exposed secrets
- compromised runner
- overly broad deployment permissions
- unreviewed pipeline change
- untrusted dependency

Treat pipelines as production security boundaries.

---

# 50. Infrastructure as Code Security — Preview

IaC can improve security through:

- review
- repeatability
- policy
- drift visibility

But can also spread insecure configuration quickly.

Automation increases both consistency and blast radius.

---

# 51. Container / Kubernetes Security — Preview

Containerized systems introduce security boundaries around:

- image trust
- runtime privileges
- workload identity
- network access
- secrets
- admission/policy
- host/kernel sharing

Deep Kubernetes security comes later.

---

# 52. Cloud Shared Responsibility Connection

Cloud providers secure parts of the platform.

Customers still own important responsibilities depending on the service model.

Security questions include:

- identity
- configuration
- data
- workload
- network exposure
- secrets
- monitoring

Never assume "cloud" means "secure by default."

---

# 53. Network Segmentation — Preview

Segmentation limits which systems can communicate.

Conceptually:

~~~text
Need to Communicate
→ Allow

No Business Need
→ Block
~~~

Segmentation reduces lateral blast radius.

Deep network security comes later.

---

# 54. Blast Radius

Security architecture should ask:

> If one identity, service, credential, or component is compromised, how much can it affect?

Blast radius can be reduced through:

- scoped permissions
- segmentation
- separate accounts/projects
- isolated secrets
- independent trust boundaries

---

# 55. Security Incident Response Connection

Security incidents still require:

~~~text
Detect
→ Scope
→ Contain
→ Preserve Evidence
→ Recover
→ Validate
→ Learn
~~~

This overlaps with reliability incident response but includes additional concerns such as trust restoration and credential/identity review.

---

# 56. Backup and Recovery Security

Backups can contain sensitive data.

Security questions include:

- who can read them?
- who can delete them?
- who can restore them?
- are they encrypted?
- are restore actions audited?
- can compromised production credentials destroy backups?

Recovery architecture is also security architecture.

---

# 57. Security and Observability

Security needs evidence.

Useful telemetry may include:

- authentication events
- authorization failures
- privilege changes
- secret access
- configuration changes
- suspicious activity
- unusual service behavior

But security telemetry itself must protect sensitive information.

---

# 58. Security and Reliability

Security and reliability can reinforce or conflict.

Examples:

- strict controls can slow recovery if emergency access is poorly designed
- weak controls can make recovery untrustworthy
- aggressive blocking can affect availability
- excessive privilege can increase incident blast radius

Architecture must balance both.

---

# 59. Security and Developer Experience

Security controls that are extremely difficult to use may be bypassed.

Good security engineering aims for:

~~~text
Safe Path
→ Easy Path
~~~

Secure defaults and developer-friendly workflows improve adoption.

---

# 60. Security Ownership

Security is shared.

Possible owners include:

- application teams
- platform teams
- security teams
- SRE
- cloud/infrastructure teams

Clear responsibility matters for:

- patching
- secrets
- IAM
- vulnerabilities
- incidents
- exceptions

---

# 61. Production Readiness

Before launch, ask:

- assets identified?
- data classified?
- identities defined?
- least privilege applied?
- secrets managed?
- network exposure understood?
- dependencies reviewed?
- logging/audit ready?
- vulnerability/patch process understood?
- recovery protected?
- ownership clear?

Security is a production-readiness gate.

---

# 62. Common Beginner Mistakes

## Mistake 1

"Security means firewall."

A firewall is one control.

## Mistake 2

"Authentication solves security."

Authentication does not replace authorization, least privilege, monitoring, or secure design.

## Mistake 3

"Encryption means the data is secure."

Encryption does not replace identity, authorization, secrets management, or operational controls.

## Mistake 4

"Admin access is easier."

Broad privileges increase blast radius.

## Mistake 5

"Secrets are just config."

Secrets have a lifecycle and should be handled differently.

## Mistake 6

"Security belongs only to security teams."

Product and platform teams own many real security controls.

## Mistake 7

"More controls automatically means more security."

Controls that do not address real risk can add complexity without reducing meaningful exposure.

## Mistake 8

"If prevention is strong, detection is unnecessary."

Controls can fail. Detection and response remain necessary.

---

# 63. Five-Level Explanation

## L1 — Foundation

Security protects systems, identities, and data from unauthorized or harmful use.

## L2 — Engineer

Security engineers identify assets, threats, trust boundaries, identities, permissions, secrets, and controls that reduce risk.

## L3 — Senior Engineer

Security engineering connects identity, least privilege, secure configuration, dependencies, telemetry, supply-chain trust, blast radius, incident response, and production readiness.

## L4 — SRE / Security Operations

Operational security uses detection, audit evidence, secure access, patching, incident response, recovery, and continuous risk reduction.

## L5 — Architect

Security architecture balances business need, risk, identity boundaries, trust, segmentation, data protection, developer experience, cost, operational complexity, reliability, and recovery.

---

# 64. Senior Engineer Perspective

A senior engineer asks:

- what asset are we protecting?
- what is the threat?
- where is the trust boundary?
- what identity is acting?
- what permissions exist?
- what secret or credential is involved?
- what is the blast radius?
- what evidence exists?
- what safe control reduces the risk?

---

# 65. SRE Perspective

An SRE asks:

- can we detect misuse?
- is privileged access auditable?
- can recovery be trusted?
- are emergency paths controlled?
- can one credential cause wide impact?
- are secrets rotatable?
- do alerts indicate meaningful security conditions?
- what control failure would become a reliability incident?

---

# 66. Architect Perspective

An architect asks:

- what assets have the highest business impact?
- where are trust boundaries?
- how are human and workload identities separated?
- what controls are preventive vs detective?
- how is least privilege enforced at scale?
- how are secrets and keys governed?
- how is supply-chain trust established?
- what security controls affect availability?
- how will the organization recover trust after compromise?

---

# 67. What You Must Retain

Before moving on, retain:

- security is risk management
- confidentiality, integrity, and availability are distinct goals
- assets come before controls
- threats and vulnerabilities are different
- risk depends on context, likelihood, and impact
- attack surface should be minimized
- trust boundaries require explicit decisions
- identity comes before access
- authentication and authorization are different
- least privilege reduces blast radius
- temporary access should not become permanent by default
- separation of duties reduces concentrated risk
- deny-by-default is a strong mental model
- Zero Trust is about explicit verification and limited trust
- human and workload identities should be designed differently
- credentials and secrets are sensitive assets
- secret lifecycle includes rotation and revocation
- hard-coded secrets create long-lived exposure
- encryption in transit and at rest solve different problems
- encryption does not replace access control
- hashing and encryption are different
- data classification drives controls
- data minimization reduces exposure
- audit trails support accountability and investigation
- prevention must be combined with detection and response
- defense in depth reduces single-control dependency
- secure defaults matter
- insecure configuration is a major risk source
- patching is risk-driven change
- vulnerability management includes context and prioritization
- dependencies extend the trust chain
- supply-chain trust spans source to runtime
- CI/CD is a security boundary
- IaC can scale secure or insecure configuration
- cloud security uses shared responsibility
- segmentation reduces lateral blast radius
- backups require security controls
- security and observability reinforce each other
- security and reliability must be balanced
- usable security improves adoption
- ownership must be explicit
- security is a production-readiness gate

---

# 68. Practical Package — Next Layer

The practical package should include safe, provider-neutral exercises such as:

- identify assets, threats, vulnerabilities, and risks for a sample service
- map trust boundaries
- distinguish authentication vs authorization
- review permissions for least privilege
- classify human vs workload identities
- review a secret lifecycle
- identify unsafe secret placement
- classify data and logging sensitivity
- map defense-in-depth controls
- review a CI/CD trust path
- map supply-chain trust at a conceptual level
- perform a production-readiness security review

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 69. Assessment Package — Pending

The assessment should test:

- security as risk management
- CIA triad
- assets / threats / vulnerabilities / risk
- attack surface
- trust boundaries
- identity
- authentication / authorization
- least privilege
- separation of duties
- deny by default
- Zero Trust preview
- human/workload identity
- credentials / secrets
- secret lifecycle
- encryption / hashing concepts
- data classification / minimization
- logging / audit
- detection / response
- defense in depth
- secure defaults
- hardening
- patching
- vulnerability management preview
- dependency / third-party risk
- software supply-chain preview
- CI/CD / IaC security previews
- cloud shared responsibility
- segmentation
- blast radius
- backup/recovery security
- production readiness
- Senior/SRE/Architect reasoning

---

# 70. Visual Package — Pending

The visual package should include:

1. Asset → Threat → Vulnerability → Risk → Control
2. Identity → Authentication → Authorization → Least Privilege → Audit
3. Trust Boundary → Control → Detection → Response
4. Secret Lifecycle: Create → Store → Distribute → Use → Rotate → Revoke
5. Source → Build → Artifact → Registry → Deployment → Runtime Trust Chain
6. Defense in Depth → Blast Radius Reduction

---

# 71. What Comes Next

After D00-T015 is completed, continue to:

## 00.16 — Automation Mental Models

That topic will deepen idempotency, orchestration, event-driven automation, safe retries, state, control loops, human approval boundaries, and automation failure modes.

---

# 72. Sources & Evidence

Planned authoritative source families:

- NIST cybersecurity guidance
- NIST Zero Trust Architecture
- OWASP guidance
- CISA secure-by-design / security guidance
- major cloud-provider security architecture guidance
- supply-chain guidance such as SLSA where useful
- vendor-neutral identity and secrets-management references

Current evidence status:

- conceptual draft: RESEARCHED
- source verification: pending
- practical package: pending
- assessment package: pending
- visual package: pending

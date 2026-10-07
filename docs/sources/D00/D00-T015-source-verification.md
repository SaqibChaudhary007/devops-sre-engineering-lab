# D00-T015 Source Verification — Security Foundations

## Verification Goal

Verify the core claims in **00.15 — Security Foundations** against authoritative cybersecurity, identity, secure-by-design, cloud-security, secrets-management, and software-supply-chain guidance.

Primary source families used:

- NIST Cybersecurity Framework (CSF) 2.0
- NIST SP 800-207 Zero Trust Architecture
- NIST SP 800-207A cloud-native Zero Trust guidance
- OWASP Authorization, Secrets Management, Cryptographic Storage, Password Storage, and CI/CD Security guidance
- CISA Secure by Design / Secure by Default guidance
- SLSA v1.2 provenance guidance
- AWS and Microsoft Azure shared-responsibility guidance

## Verification Status

**Result:** Core D00-T015 claims are supported, with important nuances around cybersecurity risk, Zero Trust, authentication vs authorization, least privilege, secrets lifecycle, secure defaults, cryptography, software-supply-chain provenance, cloud shared responsibility, and security/reliability trade-offs.

**Evidence level:** E2 — supported by first-party standards, government guidance, established security-project documentation, and major cloud-provider guidance.

This topic remains at the D00 mental-model level. Deep cryptography, IAM policy language, Kubernetes security controls, offensive security, detailed vulnerability scoring, key-management implementation, compliance frameworks, supply-chain attestations, and platform-specific security engineering belong to later domains.

---

# Primary / Authoritative Sources

## 1. NIST Cybersecurity Framework 2.0

- https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20
- https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=957258

Supports:

- cybersecurity should be managed as organizational risk
- risk should be understood, assessed, prioritized, and communicated
- cybersecurity outcomes span governance, identification, protection, detection, response, and recovery
- prevention alone is not a complete security program
- response and recovery readiness are part of cybersecurity

### Verified nuance

CSF 2.0 uses six functions:

~~~text
Govern
Identify
Protect
Detect
Respond
Recover
~~~

Therefore the D00 security lifecycle should not imply that security ends at preventive controls.

---

## 2. NIST SP 800-207 — Zero Trust Architecture

- https://www.nist.gov/publications/zero-trust-architecture
- https://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.SP.800-207.pdf

Supports:

- Zero Trust does not grant implicit trust solely because of network location or ownership
- resource protection is more important than assuming a trusted internal network
- authentication and authorization are distinct functions
- access should be limited to what is needed
- identity, credentials, access management, endpoints, workloads, and infrastructure all matter

### Verified nuance

Do not reduce Zero Trust to:

~~~text
Never trust anyone.
~~~

A better D00 model is:

~~~text
No implicit trust from location alone
→ verify identity/context
→ authorize explicitly
→ grant minimum necessary access
→ continually evaluate trust
~~~

---

## 3. NIST SP 800-207A — Cloud-Native Zero Trust

- https://csrc.nist.gov/pubs/sp/800/207/A/final

Supports:

- cloud-native systems require identity-aware access controls
- service/workload identity matters in addition to user identity
- network identity alone is insufficient for many modern distributed applications
- application and service identities are important security subjects

### Verified nuance

Human identity and workload identity should be taught as related but operationally different classes of identity.

---

## 4. OWASP Authorization Cheat Sheet

- https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html

Supports:

- authentication and authorization are distinct
- an authenticated user is not automatically authorized for every action
- least privilege means granting only the minimum privileges needed
- authorization failures can affect confidentiality, integrity, and availability

### Verified nuance

The canonical model is correct:

~~~text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
~~~

Strong authentication does not compensate for excessive authorization.

---

## 5. OWASP Secrets Management Cheat Sheet

- https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html

Supports:

- secrets include API keys, database credentials, IAM credentials, SSH keys, certificates, and related sensitive material
- hard-coded/plaintext secrets are a serious operational risk
- secrets require storage, provisioning, auditing, rotation, and lifecycle management
- least privilege should apply to secrets
- reducing unnecessary human exposure to secrets improves security
- automated secret creation/rotation can reduce manual error when designed safely

### Verified nuance

Secrets management is a lifecycle problem, not just a storage problem:

~~~text
Create
→ Store
→ Distribute
→ Use
→ Rotate
→ Revoke
→ Audit
~~~

Short-lived credentials reduce exposure windows but still require correct scope, issuance, revocation, and identity controls.

---

## 6. OWASP Cryptographic Storage and Password Storage Guidance

- https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html
- https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html

Supports:

- encryption at rest protects stored data
- cryptographic protection should follow threat modeling and architecture decisions
- encryption does not replace access control
- password storage should use appropriate password-hashing techniques rather than reversible encryption
- hashing and encryption solve different problems

### Verified nuance

At D00:

~~~text
Encryption
→ reversible protection with a key

Hashing
→ one-way transformation used for integrity/content identity and, with password-specific algorithms, password verification
~~~

Do not teach generic fast hashes as appropriate password-storage mechanisms.

---

## 7. CISA Secure by Design / Secure by Default

- https://www.cisa.gov/sites/default/files/2023-10/Shifting-the-Balance-of-Cybersecurity-Risk-Principles-and-Approaches-for-Secure-by-Design-Software.pdf
- https://www.cisa.gov/sites/default/files/2023-12/SbD-Alert-How-Software-Manufacturers-Can-Protect-Customers-by-Eliminating-Default-Passwords-508c_0.pdf

Supports:

- security should be built into product design and development
- secure defaults reduce customer/operator burden
- default passwords are dangerous
- privileged accounts should receive stronger authentication protections
- high-quality audit logging is important
- the easiest operational path should ideally be the secure path

### Verified nuance

The D00 principle:

~~~text
Safe Path
→ Easy Path
~~~

is aligned with Secure by Design / Secure by Default thinking.

Security should not depend entirely on every operator remembering to harden unsafe defaults manually.

---

## 8. OWASP CI/CD Security

- https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html

Supports:

- CI/CD systems can hold powerful credentials and permissions
- least privilege applies to pipeline identities and secrets
- temporary credentials can reduce the impact of credential theft
- pipeline permissions should be intentionally scoped
- CI/CD environments are security-sensitive trust boundaries

### Verified nuance

Treating the delivery system as a production security boundary is correct.

Automation does not remove risk; it can distribute insecure permissions or configuration quickly.

---

## 9. SLSA v1.2 Provenance

- https://slsa.dev/spec/v1.2/
- https://slsa.dev/spec/v1.2/provenance
- https://slsa.dev/spec/v1.2/verifying-artifacts

Supports:

- provenance is verifiable information describing where, when, and how an artifact was produced
- build provenance can connect an artifact back to build inputs and process
- provenance enables artifact verification against expectations
- provenance is part of software-supply-chain trust

### Verified nuance

At D00:

~~~text
Source
→ Build
→ Artifact
→ Deployment
→ Runtime
~~~

is a valid introductory trust-chain model.

However, provenance alone does not automatically make an artifact trustworthy; it must be generated by a trustworthy process and verified against expectations.

---

## 10. AWS Shared Responsibility

- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/shared-responsibility.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/security.html

Supports:

- cloud security is shared between provider and customer
- provider responsibility includes underlying cloud infrastructure
- customer responsibility varies with service type
- customers remain responsible for areas such as data, access, application/configuration, and service-specific controls

### Verified nuance

Do not teach:

~~~text
Cloud Provider
→ Owns Security
~~~

A stronger model is:

~~~text
Provider Responsibilities
+
Customer Responsibilities
→ Cloud Security Outcome
~~~

The exact boundary changes by service model.

---

## 11. Microsoft Azure Shared Responsibility

- https://learn.microsoft.com/en-us/azure/security/fundamentals/shared-responsibility

Supports:

- responsibility changes across IaaS, PaaS, and SaaS
- customers retain responsibility for data and identities
- customers retain important configuration and access-management responsibilities
- moving to managed services shifts some responsibilities but does not remove customer security ownership

### Verified nuance

"Shared responsibility" is not one fixed matrix for every cloud service.

The service model changes which layer the provider operates and which controls remain with the customer.

---

# Verified Claim Map

| Topic claim | Verification | Primary source family |
|---|---|---|
| Security is risk management | Verified | NIST CSF 2.0 |
| Security includes prevent/detect/respond/recover | Verified | NIST CSF 2.0 |
| Authentication and authorization are distinct | Verified | OWASP / NIST ZTA |
| Least privilege reduces unnecessary access | Verified | OWASP / NIST ZTA |
| Zero Trust removes implicit trust based on location alone | Verified | NIST SP 800-207 |
| Workload/service identity matters | Verified | NIST SP 800-207A |
| Secrets require lifecycle management | Verified | OWASP Secrets |
| Hard-coded/plaintext secrets are risky | Verified | OWASP Secrets |
| Short-lived credentials reduce exposure duration | Verified with scope caveat | OWASP CI/CD / Secrets |
| Encryption does not replace access control | Verified | OWASP Cryptographic Storage |
| Hashing and encryption are different | Verified | OWASP Password Storage |
| Secure defaults reduce operator/customer burden | Verified | CISA Secure by Design |
| High-quality audit logs support investigation | Verified | CISA |
| CI/CD is a security-sensitive trust boundary | Verified | OWASP CI/CD |
| Automation can amplify insecure configuration/permissions | Verified at mental-model level | OWASP CI/CD / secure-by-design reasoning |
| Supply-chain trust spans source/build/artifact | Verified | SLSA |
| Provenance records where/how an artifact was produced | Verified | SLSA |
| Provenance should be verified against expectations | Verified | SLSA |
| Cloud security uses shared responsibility | Verified | AWS / Azure |
| Responsibility varies by cloud service model | Verified | AWS / Azure |
| Data/identity/configuration remain important customer responsibilities | Verified | Azure / AWS |
| Security ownership belongs across product/platform/security teams | Verified at organizational mental-model level | NIST CSF / CISA |

---

# Verified Nuances / Corrections

## 1. Risk Is Not a Universal Equation

The topic uses:

~~~text
Risk ≈ Likelihood × Impact
~~~

as a beginner mental model.

Keep the approximation symbol.

Real risk assessment is contextual and may include exposure, threat capability, control strength, uncertainty, business impact, and other factors.

## 2. CIA Is a Foundation, Not a Complete Security Architecture

Confidentiality, integrity, and availability are valuable security objectives.

But architecture also needs:

- identity
- trust
- auditability
- resilience
- governance
- response/recovery
- supply-chain considerations

## 3. Zero Trust Is Not "Trust Nobody"

Zero Trust removes implicit trust assumptions.

It requires explicit policy decisions about subjects, devices/workloads, resources, and context.

## 4. Authentication Does Not Grant Unlimited Authorization

A correctly authenticated administrator, service, or pipeline can still be dangerously overprivileged.

Identity proof and permission scope must be evaluated separately.

## 5. Least Privilege Includes Scope and Duration

Least privilege is stronger when asking:

~~~text
Who / What?
Which Resource?
Which Action?
For How Long?
Under Which Conditions?
~~~

## 6. Secrets Are Lifecycle Assets

The biggest secret-management problem may occur during:

- creation
- delivery
- human handling
- CI/CD use
- rotation
- revocation

not only storage.

## 7. Short-Lived Does Not Mean Safe by Itself

A short-lived credential with administrator-level access can still have a large blast radius.

Scope, identity, issuance, and monitoring still matter.

## 8. Encryption Is One Control

Encryption protects data under particular threat models.

It does not replace:

- authorization
- key management
- identity
- data minimization
- secure configuration
- monitoring

## 9. Password Hashing Needs Password-Specific Techniques

Do not imply:

~~~text
SHA-256(password)
→ secure password storage
~~~

D00 should only teach the conceptual distinction; implementation-specific algorithms belong later.

## 10. Secure Defaults Matter More Than Security Documentation Alone

If the normal/default path is unsafe, real deployments are likely to inherit that risk.

The secure path should be easy and defaults should reduce exposure.

## 11. Defense in Depth Does Not Mean "Add Random Controls"

Multiple controls should address meaningful failure modes and avoid a single control becoming the only barrier.

More controls without threat/risk reasoning can create complexity without meaningful protection.

## 12. CI/CD Has Production-Grade Trust

Pipeline systems often hold:

- source access
- artifact publishing access
- secrets
- cloud credentials
- deployment authority

Therefore pipeline identities and permissions deserve least-privilege and audit thinking.

## 13. Provenance Is Evidence, Not Automatic Trust

Provenance can describe an artifact's origin and build path.

Trust also depends on:

- builder trust
- source trust
- policy
- verification
- signing/attestation integrity

## 14. Shared Responsibility Changes with Service Model

IaaS, PaaS, SaaS, and individual managed services shift operational responsibility differently.

Customers should not assume managed service means no customer security responsibility.

## 15. Security and Reliability Can Conflict

A control can improve one property while making another operational path harder.

Examples include:

- emergency access vs least privilege
- availability vs aggressive blocking
- rapid patching vs change risk
- strict segmentation vs recovery access

Architectural decisions should evaluate both security and reliability consequences.

---

# Evidence Decision

The following D00-T015 areas are now eligible for **DOC-VERIFIED** status:

- security as risk management
- prevent/detect/respond/recover lifecycle
- identity at foundation level
- authentication vs authorization
- least privilege
- time/scoped access as a security principle
- separation-of-duties mental model
- deny-by-default / secure-default mental models
- Zero Trust preview
- human vs workload identity
- credentials and secrets
- secret lifecycle
- hard-coded-secret risk
- short-lived-credential concept
- certificates at foundation level
- encryption at rest / in transit
- hashing vs encryption at foundation level
- data classification/minimization mental models
- audit/security logging
- detection as part of security
- defense in depth
- secure defaults
- secure configuration / hardening at foundation level
- patching / vulnerability-management preview
- dependency / third-party risk
- software-supply-chain preview
- artifact integrity / provenance preview
- CI/CD security preview
- IaC automation-blast-radius connection
- cloud shared-responsibility model
- blast-radius thinking
- security incident-response connection
- security/reliability trade-offs
- security ownership and production readiness

The following remain intentionally preview-level pending later domains:

- detailed threat modeling methodologies
- exploit mechanics
- offensive-security techniques
- cryptographic algorithms and key-management internals
- PKI implementation
- IAM policy syntax
- MFA protocol internals
- secrets-platform implementation
- vulnerability scanners and scoring systems
- SBOM generation/verification
- SLSA attestation implementation
- artifact-signing implementation
- Kubernetes admission/security-policy implementation
- network-security implementation
- cloud-provider IAM implementation
- compliance/control-framework engineering
- forensic procedures

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured, safe exercises:

- identify assets, threats, vulnerabilities, and risk for a sample service
- map trust boundaries
- distinguish authentication from authorization
- review permissions for least privilege
- classify human vs workload identity
- review a secret lifecycle
- identify unsafe secret placement
- classify data/logging sensitivity
- map defense-in-depth controls
- review CI/CD trust and permissions
- map software-supply-chain trust conceptually
- perform a production-readiness security review

These become the D00-T015 practical package.

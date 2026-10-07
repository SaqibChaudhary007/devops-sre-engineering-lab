---
id: EXP-D00-026
domain: D00
topics:
  - D00-T015
level: L2-L3
type: experiment
status: draft
estimated_time: 60-80m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# EXP-D00-026 — Supply-Chain Trust, Defense in Depth, and Security Readiness

## Objective

Practice safe security-architecture reasoning across CI/CD trust, artifact integrity, provenance, defense in depth, blast-radius reduction, backup security, and production readiness.

## Safety

This is a design and review exercise only.

Do not tamper with repositories, artifacts, pipelines, credentials, registries, or production systems. Do not attempt to bypass controls or reproduce real attack techniques.

## Scenario

A software-delivery path looks like this:

~~~text
Developer
→ Source Repository
→ CI/CD Runner
→ Build
→ Artifact Registry
→ Deployment Pipeline
→ Production Runtime
~~~

Current weaknesses:

~~~text
- pipeline has broad production permissions
- build artifacts are promoted without verification
- source and pipeline changes use weak review rules
- dependency ownership is unclear
- one credential can access multiple environments
- production and backup access use the same identity
- security logging is incomplete
- service launch checklist has no security section
~~~

## 1. Map the Trust Chain

For each stage, identify:

- asset
- acting identity
- trust boundary
- allowed action
- evidence generated
- failure consequence

Use:

~~~text
Source
→ Build
→ Artifact
→ Registry
→ Deployment
→ Runtime
~~~

## 2. CI/CD Trust Review

Review:

- pipeline identity
- deployment permissions
- secret exposure
- environment separation
- approval gates
- audit evidence

Explain why CI/CD should be treated as a production security boundary.

## 3. Artifact Integrity

For an artifact moving from build to deployment, explain the purpose of:

- digest/checksum
- controlled promotion
- signature concept
- provenance concept
- verification before deployment

Keep this at conceptual level.

## 4. Provenance Reasoning

Use:

~~~text
Source
+ Build Process
+ Builder Identity
+ Artifact
→ Provenance Evidence
~~~

Then explain why provenance is not automatic trust.

Ask:

- do we trust the builder?
- do we trust the source?
- was the evidence altered?
- does policy allow this artifact?
- was verification actually performed?

## 5. Dependency / Third-Party Risk

For a third-party dependency, ask:

- what data can it access?
- what privileges does it inherit?
- what happens if unavailable?
- what happens if compromised?
- who owns updates?
- how is risk reviewed?

Do not perform dependency exploitation.

## 6. Defense in Depth

Design multiple complementary controls around production deployment:

~~~text
Identity
+ Least Privilege
+ Review
+ Artifact Verification
+ Environment Separation
+ Audit
+ Monitoring
~~~

Explain why adding random controls without threat/risk reasoning is not meaningful defense in depth.

## 7. Blast-Radius Review

Assume one deployment credential is compromised conceptually.

Do not attempt any real access.

Ask:

- can it reach dev/test/prod?
- can it read secrets?
- can it modify backups?
- can it publish artifacts?
- can it change IAM?
- can it disable audit evidence?

Redesign the architecture to limit possible impact.

## 8. Backup Security

Review backups for:

- read access
- delete access
- restore access
- encryption
- separate identity
- audit trail
- environment separation

Explain why recovery architecture is also security architecture.

## 9. Security Monitoring

Define safe, useful events to capture:

- authentication
- failed authorization
- privilege change
- secret access
- artifact promotion
- deployment approval
- configuration change
- backup deletion/restore attempt

Explain why detection complements prevention.

## 10. Security + Reliability Trade-Off

Review these tensions:

- emergency access vs least privilege
- aggressive blocking vs availability
- urgent patch vs change risk
- segmentation vs recovery access

For each, propose a balanced operating principle rather than an absolute rule.

## 11. Production-Readiness Security Review

Score each:

~~~text
Ready
Partially Ready
Not Ready
~~~

for:

- assets identified
- data classified
- trust boundaries mapped
- human/workload identities separated
- least privilege reviewed
- secrets lifecycle defined
- audit/security logging ready
- CI/CD permissions scoped
- artifacts verified
- dependency ownership defined
- backup access protected
- response/recovery ownership clear

## 12. Security Ownership

Assign conceptual ownership among:

- application team
- platform team
- security team
- SRE
- infrastructure/cloud team

Explain why shared responsibility still requires explicit accountability.

## 13. Senior Engineer Connection

Use:

~~~text
Trust Chain
→ Identity
→ Permission
→ Artifact
→ Evidence
→ Control
→ Blast Radius
→ Recovery
~~~

## 14. SRE Connection

Connect security to:

- production readiness
- auditability
- emergency access
- incident response
- backup/recovery
- service reliability

## 15. Architect Connection

Decide:

- where trust boundaries should be strengthened
- how environment permissions should be separated
- what artifact evidence is mandatory
- what controls reduce blast radius
- what security checks belong in launch readiness

## Validation Checklist

- [ ] Mapped the software-delivery trust chain
- [ ] Reviewed CI/CD as a security boundary
- [ ] Explained artifact integrity and provenance
- [ ] Reviewed dependency/third-party risk
- [ ] Designed meaningful defense in depth
- [ ] Reviewed blast radius
- [ ] Reviewed backup security
- [ ] Defined security monitoring evidence
- [ ] Balanced security/reliability trade-offs
- [ ] Performed production-readiness review
- [ ] Assigned ownership

## Teach-Back

Explain:

> "Security of software delivery depends on trustworthy identities, scoped permissions, verifiable artifacts, meaningful controls, audit evidence, limited blast radius, and recoverable systems."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

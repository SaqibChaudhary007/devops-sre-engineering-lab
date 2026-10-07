# D00-T015 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- security is risk management, not simply control accumulation
- CIA is foundational but incomplete
- assets, threats, vulnerabilities, and risks are distinct
- attack surface and trust boundaries drive security design
- Zero Trust removes implicit trust based on location/ownership
- human and workload identity are different operational classes
- authentication and authorization are separate
- least privilege includes scope and duration
- separation of duties reduces concentrated risk
- deny-by-default and secure defaults reduce exposure
- secrets have a lifecycle
- hard-coded secrets create long-lived exposure
- short-lived credentials reduce time exposure but still require correct scope/issuance/revocation
- encryption does not replace authorization or key management
- hashing is not reversible encryption
- password storage needs password-specific hashing techniques
- auditability and detection complement prevention
- defense in depth addresses meaningful failure modes
- patching and vulnerability management are risk-prioritization activities
- dependencies extend the trust chain
- CI/CD is a production security boundary
- provenance is evidence, not automatic trust
- shared cloud responsibility varies by service model
- segmentation and identity scoping reduce blast radius
- backup/recovery systems need independent security controls
- security and reliability may reinforce or conflict
- production readiness includes security ownership and recovery trust

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T015

Critical misconception override: no competency if the learner believes authentication = authorization, Zero Trust = trust nobody, admin-for-everyone = acceptable, secrets = ordinary config, short-lived = automatically safe, encryption = complete security, generic fast hashes = adequate password storage, provenance = automatic trust, or managed cloud = provider owns all security.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Assets / threats / weaknesses / risk | 10 |
| Trust boundaries / identity model | 10 |
| Authentication / authorization / least privilege | 15 |
| Emergency access / time-bounded permissions | 10 |
| Secrets lifecycle / credential design | 10 |
| Audit / detection / response | 10 |
| CI/CD / artifact / provenance / dependency trust | 15 |
| Shared responsibility / environment separation / backups | 10 |
| Security vs reliability / production readiness | 5 |
| Senior / SRE / Architect target design | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- begin with assets and trust boundaries
- separate human and workload identity
- separate authentication from authorization
- scope privileges by action/resource/duration
- replace permanent emergency access with temporary audited access
- treat secrets as lifecycle assets
- reduce static credential exposure
- design meaningful audit evidence
- treat CI/CD as production-grade trust
- require artifact verification before deployment
- use provenance as evidence subject to verification
- separate production and backup authority
- explain shared responsibility by service model
- combine prevention with detection/response
- balance security controls with recovery and availability

## Follow-Up Evaluation

- L1: defines security concepts
- L2: connects identity, access, secrets, and controls
- L3: reasons through operational security risks
- L4: designs SRE/security operating practices
- L5: designs architecture/governance/reliability trade-offs

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. adaptable, production-aware, and trade-off aware

Target: 4/5 average.

## Remediation Map

If weak on:

- risk / CIA / assets / threats / vulnerabilities → revisit sections 3–9 and OBS-D00-019
- attack surface / trust boundaries → revisit sections 10–12 and OBS-D00-019
- identity / authentication / authorization → revisit sections 13–16 and EXP-D00-025
- least privilege / time-bounded access / separation of duties → revisit sections 17–20 and EXP-D00-025
- Zero Trust / human-workload identity → revisit sections 21–22
- credentials / secrets / lifecycle → revisit sections 23–27 and EXP-D00-025
- encryption / hashing / data protection → revisit sections 28–33
- audit / detection / defense in depth → revisit sections 34–39 and EXP-D00-026
- secure configuration / hardening / patching → revisit sections 40–43
- dependency / third-party / supply chain → revisit sections 44–48 and EXP-D00-026
- CI/CD / IaC / container-cloud previews → revisit sections 49–53 and EXP-D00-026
- blast radius / incident / backup security → revisit sections 54–57 and EXP-D00-026
- security-reliability / ownership / readiness → revisit sections 58–61 and EXP-D00-026
- Senior/SRE/Architect reasoning → revisit sections 64–66

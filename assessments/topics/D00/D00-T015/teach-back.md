# D00-T015 — Teach-Back Assessment

## Goal

Demonstrate that you can explain security as risk management rather than as a collection of tools.

## Task A — Beginner

Explain:

- asset
- threat
- vulnerability
- risk
- control

## Task B — CIA

Explain:

- confidentiality
- integrity
- availability

Then explain why CIA alone is not a complete security architecture.

## Task C — Identity

Teach:

~~~text
Identity
→ Authentication
→ Authorization
→ Least Privilege
→ Audit
~~~

Use one human and one workload example.

## Task D — Zero Trust

Explain Zero Trust without saying "trust nobody."

Include:

- no implicit trust from location alone
- explicit identity/context
- authorization
- least privilege
- continual evaluation

## Task E — Secrets

Explain:

~~~text
Create
→ Store
→ Distribute
→ Use
→ Rotate
→ Revoke
→ Audit
~~~

Then explain why secrets should not be committed to source.

## Task F — Cryptography Boundaries

Explain:

- encryption in transit
- encryption at rest
- hashing

Then explain why encryption does not replace access control and why generic fast hashes are not the right password-storage model.

## Task G — CI/CD and Supply Chain

Explain:

~~~text
Source
→ Build
→ Artifact
→ Registry
→ Deployment
→ Runtime
~~~

Then explain why provenance is evidence but not automatic trust.

## Task H — Defense in Depth

Explain how multiple complementary controls reduce single-control dependency.

Avoid describing defense in depth as "just add more controls."

## Task I — Shared Responsibility

Explain why moving from IaaS to PaaS/SaaS changes responsibilities but does not remove customer responsibility for identity, data, and important configuration.

## Task J — Architect

Explain how you would balance:

- security
- reliability
- developer experience
- cost
- operational complexity
- recovery

## Scoring

Score 1–5 for:

- correctness
- clarity
- risk reasoning
- identity/access reasoning
- secrets/cryptography reasoning
- supply-chain reasoning
- security/reliability reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

# D00-T015 Visual / Diagram Package — Security Foundations

This package provides reusable diagrams for **00.15 — Security Foundations**.

## Diagram Set

1. [DIA-D00-083 — Asset → Threat → Vulnerability → Risk → Control](DIA-D00-083-asset-threat-vulnerability-risk-control.md)
2. [DIA-D00-084 — Identity → Authentication → Authorization → Least Privilege → Audit](DIA-D00-084-identity-authn-authz-least-privilege-audit.md)
3. [DIA-D00-085 — Trust Boundary → Control → Detection → Response](DIA-D00-085-trust-boundary-control-detection-response.md)
4. [DIA-D00-086 — Secret Lifecycle: Create → Store → Distribute → Use → Rotate → Revoke](DIA-D00-086-secret-lifecycle.md)
5. [DIA-D00-087 — Source → Build → Artifact → Registry → Deployment → Runtime Trust Chain](DIA-D00-087-software-supply-chain-trust.md)
6. [DIA-D00-088 — Defense in Depth → Blast Radius Reduction](DIA-D00-088-defense-in-depth-blast-radius.md)

## Learning Progression

~~~text
Asset
→ Threat
→ Trust Boundary
→ Identity
→ Control
→ Detection
→ Response
→ Recovery
→ Improvement
~~~

## Design Rules

- stay defensive and provider-neutral
- begin with assets and meaningful risk before controls
- distinguish authentication from authorization
- show least privilege as scope + action + duration
- show Zero Trust as removal of implicit trust, not "trust nobody"
- treat secrets as lifecycle assets
- treat CI/CD and software delivery as security trust boundaries
- show provenance as evidence, not automatic trust
- combine preventive and detective controls
- show security and reliability as interacting architecture concerns
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Deep IAM policy design, cryptography, Kubernetes security, network security, vulnerability exploitation, secrets-platform implementation, compliance engineering, and supply-chain attestation tooling belong to later domains.

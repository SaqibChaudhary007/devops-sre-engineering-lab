# D00-T009 Visual / Diagram Package — CI/CD Mental Model

This package provides reusable diagrams for **00.09 — CI/CD Mental Model**.

## Diagram Set

1. [DIA-D00-047 — CI vs Continuous Delivery vs Continuous Deployment](DIA-D00-047-ci-vs-continuous-delivery-vs-deployment.md)
2. [DIA-D00-048 — Source → Build → Validate → Artifact → Promote → Deploy](DIA-D00-048-source-build-validate-artifact-promote-deploy.md)
3. [DIA-D00-049 — Build Once / Promote Same Artifact](DIA-D00-049-build-once-promote-same-artifact.md)
4. [DIA-D00-050 — Pipeline Feedback & Failure Loop](DIA-D00-050-pipeline-feedback-failure-loop.md)
5. [DIA-D00-051 — Deployment vs Release](DIA-D00-051-deployment-vs-release.md)
6. [DIA-D00-052 — CI/CD + IaC + GitOps Relationship](DIA-D00-052-cicd-iac-gitops-relationship.md)

## Learning Progression

~~~text
Integrate
→ Build
→ Validate
→ Package
→ Promote
→ Deploy
→ Verify
→ Observe
→ Learn
~~~

## Design Rules

- stay provider-neutral
- distinguish CI from continuous delivery and continuous deployment
- show artifacts as identified outputs, not caches
- reinforce build-once/promote where practical
- separate deployment from release
- make failure, feedback, retry, and recovery visible
- distinguish push-style CI/CD from GitOps pull/reconciliation
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Deep vendor-specific pipeline syntax, deployment strategies, artifact systems, GitOps tooling, and supply-chain implementation belong to later domains.

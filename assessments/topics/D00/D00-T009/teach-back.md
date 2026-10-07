# D00-T009 — Teach-Back Assessment

## Goal

Demonstrate that you can explain CI/CD as a delivery system rather than as a specific tool.

## Task A — Beginner

Explain:

- what CI is
- what CD is
- why teams use them

Use one simple analogy.

## Task B — Engineer

Explain:

~~~text
Change
→ Integrate
→ Build
→ Validate
→ Package
→ Promote
→ Deploy
→ Verify
→ Observe
~~~

Explain what evidence should exist at each major step.

## Task C — Continuous Delivery vs Continuous Deployment

Explain the difference without tying the answer to a specific vendor UI.

## Task D — Artifact Challenge

Explain:

- build-once/promote
- artifact immutability
- artifact vs cache
- why same commit is weaker evidence than same verified artifact

## Task E — Senior Engineer

Explain why this statement is unsafe:

> "The pipeline is green, so production is safe."

Include:

- test coverage
- runtime dependencies
- concurrency
- deployment verification
- data compatibility
- rollback

## Task F — SRE

Explain how CI/CD should connect to:

- SLOs
- deployment markers
- alerts
- change failure
- recovery time
- operational toil

## Task G — Architect

Explain how you would design:

- artifact flow
- environment protections
- concurrency
- runner trust
- credentials
- approval/policy gates
- deployment verification
- recovery

## GitOps Challenge

Explain why:

~~~text
CI/CD
≠
GitOps
~~~

Then describe how they can work together.

## Recovery Challenge

Explain why:

> "Rollback to the previous application version"

may be unsafe after an incompatible data/schema change.

## Scoring

Score 1–5 for:

- correctness
- clarity
- CI/CD definition accuracy
- artifact/promotion reasoning
- delivery-risk reasoning
- reliability awareness
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

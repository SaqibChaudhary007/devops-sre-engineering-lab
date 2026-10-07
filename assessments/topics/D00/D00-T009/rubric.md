# D00-T009 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- CI is frequent integration plus fast automated validation
- continuous delivery and continuous deployment are different
- pipelines are mechanisms, not delivery maturity by themselves
- exact source revision and artifact identity matter
- build-once/promote reduces artifact uncertainty
- artifacts and caches are different
- deployment and release can be separated
- approval gates should represent meaningful risk decisions
- retries can hide flaky or deterministic failures
- concurrency needs deliberate control
- hosted/self-hosted runners have different trust models
- pipeline credentials should be least privilege
- short-lived identity is preferable where available
- deployment success does not prove service health
- deployment events should be observable
- rollback can be unsafe
- CI/CD and GitOps are distinct but complementary
- provenance strengthens traceability but not correctness guarantees

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T009

Critical misconception override: no competency if the learner believes CI/CD equals a tool, green tests guarantee production safety, continuous delivery equals continuous deployment, caches are release artifacts, deployment equals release, blind retries are safe, rollback always works, or GitOps replaces CI.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Delivery-system mapping / evidence | 10 |
| CI feedback / flaky-test reasoning | 10 |
| Artifact / promotion strategy | 15 |
| Concurrency / retry reasoning | 10 |
| Approval / environment protection | 10 |
| Runner / credential security | 10 |
| Deployment verification / observability | 10 |
| Recovery / database compatibility | 10 |
| CI/CD vs GitOps reasoning | 5 |
| Senior / SRE / Architect design | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- identify feedback delays and flaky-test trust problems
- promote the same identified artifact rather than rebuild independently
- distinguish artifact from cache
- prevent competing production deployments
- make approval evidence-driven
- reduce runner/credential blast radius
- verify runtime health after deployment
- correlate deployments with production telemetry
- recognize rollback limits after data/schema changes
- preserve CI while integrating GitOps

## Follow-Up Evaluation

- L1: defines CI/CD concepts
- L2: connects stages, artifacts, environments, and feedback
- L3: diagnoses delivery-system failures
- L4: connects delivery design to reliability/recovery
- L5: designs artifact, environment, policy, runner, credential, and GitOps boundaries

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

- CI/CD definitions → revisit sections 3–10
- pipeline stages / validation → revisit sections 11–17
- artifacts / promotion → revisit sections 18–24 and EXP-D00-013
- deployment / release → revisit sections 25–30
- failure / retry / concurrency → revisit sections 31–38 and EXP-D00-014
- secrets / permissions / protections → revisit sections 39–42
- verification / observability → revisit sections 43–44 and OBS-D00-013
- rollback / data compatibility → revisit sections 45–47
- CI/CD + IaC / GitOps / supply chain → revisit sections 48–51
- Senior/SRE/Architect reasoning → revisit sections 52–56

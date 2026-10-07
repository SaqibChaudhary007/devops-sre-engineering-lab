# D00-T008 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- IaC is an operating model, not one tool
- desired state and actual state can differ
- declarative and imperative approaches are distinct
- idempotence is desirable but implementation-dependent
- drift is a production risk
- version control improves reviewability and traceability
- plan/preview reduces uncertainty but does not guarantee success
- replacement/delete actions require stronger review
- dependency graphs affect ordering
- explicit state files are tool-specific
- remote state and locking are not equivalent
- locking is backend/tool-dependent
- modules improve reuse but can create coupling
- ownership boundaries affect blast radius
- secrets/policy require deliberate design
- import/adoption requires careful review
- GitOps is more specific than IaC
- reverting source code does not guarantee infrastructure rollback

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T008

Critical misconception override: no competency if the learner believes IaC equals Terraform, all IaC requires a state file, remote state guarantees locking, declarative equals safe, preview guarantees success, Git revert guarantees rollback, or GitOps equals IaC.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Desired vs actual / drift reasoning | 10 |
| Plan classification | 10 |
| Replacement / delete risk | 15 |
| State / locking reasoning | 10 |
| Scaling / dependency reasoning | 10 |
| Security review | 10 |
| Backup / recovery reasoning | 10 |
| Preview-limit reasoning | 5 |
| Rollback / roll-forward reasoning | 10 |
| Senior / SRE / Architect design | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- identify drift and unmanaged resources
- distinguish desired state from runtime reality
- treat replacement differently from update
- demand evidence before deleting stateful resources
- understand that remote state may not provide locking
- identify scaling dependencies and cost impact
- block or challenge broad public SSH exposure
- treat backup retention as a recovery requirement
- explain why plan is not proof of successful apply
- explain why Git revert is not a complete rollback strategy
- propose ownership/state/policy controls

## Follow-Up Evaluation

- L1: defines IaC concepts
- L2: connects plan, state, drift, modules, and dependencies
- L3: diagnoses unsafe infrastructure change
- L4: connects infrastructure change to reliability/recovery
- L5: designs state, ownership, policy, and organizational boundaries

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

- why IaC exists → revisit sections 3–4
- desired/actual/drift → revisit sections 5–10 and OBS-D00-012
- plan/apply/lifecycle → revisit sections 11–18 and EXP-D00-012
- state/locking → revisit sections 19–23 and EXP-D00-011
- modules/environments → revisit sections 24–29
- blast radius/review/policy/secrets → revisit sections 30–34
- provider/API/import/destroy → revisit sections 35–38
- rollback/GitOps/observability → revisit sections 39–44
- Senior/SRE/Architect reasoning → revisit sections 47–51

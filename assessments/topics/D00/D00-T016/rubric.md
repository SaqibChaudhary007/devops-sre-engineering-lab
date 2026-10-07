# D00-T016 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- automation is a force multiplier, not a universal improvement
- task understanding comes before automation
- trigger and intent are different
- current and desired state are different
- reconciliation is iterative
- imperative and declarative automation solve different problems
- preconditions protect before action
- postconditions and validation prove outcome
- repeatability is not idempotency
- idempotency reduces repeated-effect risk but does not guarantee success
- duplicate execution should be expected
- retry is a bounded policy for appropriate failures
- backoff/jitter/timeouts/rate limits reduce amplification
- partial failure must be modeled explicitly
- rollback is not always possible
- roll-forward or compensation may be safer
- workflows create coordination state
- queues decouple work but add state and delay
- concurrency introduces race conditions
- locking can coordinate but adds failure modes
- blast radius should be bounded
- human approval can be part of good automation
- automation needs dedicated identity and least privilege
- automation must be observable and auditable
- self-healing must be bounded with stop/escalation conditions
- automation has engineering/maintenance cost
- AI-assisted automation needs stronger controls as risk rises

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T016

Critical misconception override: no competency if the learner believes automation = scripting everything, retries are always safe, idempotency = guaranteed success, rollback is always possible, exit code = outcome validation, admin access is acceptable by default, self-healing = retry forever, or human approval = failed automation design.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Automation suitability / intent / trigger | 10 |
| State / reconciliation / imperative-declarative reasoning | 10 |
| Preconditions / postconditions / validation | 10 |
| Idempotency / duplicate execution | 15 |
| Retry / backoff / jitter / timeout reasoning | 15 |
| Partial failure / rollback / roll-forward / compensation | 15 |
| Guardrails / blast radius / approval boundaries | 10 |
| Identity / secrets / observability / auditability | 10 |
| Economics / AI-assisted autonomy | 5 |
| Senior / SRE / Architect target design | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- automate only understood, bounded, valuable work
- distinguish trigger from permission to act
- model current vs desired state
- choose imperative/declarative appropriately
- define preconditions and postconditions
- validate intended outcome rather than process completion
- identify duplicate-execution risk
- classify idempotency correctly
- bound retries and use backoff/jitter/timeout budgets
- model partial failure
- avoid assuming universal rollback
- define guardrails for scope/rate/concurrency/permissions
- place human approval at high-impact boundaries
- use dedicated automation identity
- emit operational and audit evidence
- bound self-healing
- reduce AI autonomy as uncertainty and impact rise

## Follow-Up Evaluation

- L1: defines automation concepts
- L2: connects state, validation, retries, and guardrails
- L3: reasons through production automation failures
- L4: designs SRE/platform automation practices
- L5: designs architecture/governance/autonomy trade-offs

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

- automation purpose / suitability → revisit sections 3–7 and OBS-D00-020
- triggers / state / reconciliation → revisit sections 8–15 and OBS-D00-020
- imperative / declarative → revisit sections 16–18 and EXP-D00-028
- preconditions / postconditions / validation → revisit sections 19–21 and OBS-D00-020
- repeatability / idempotency / duplicates → revisit sections 22–25 and EXP-D00-027
- retries / backoff / jitter / timeout → revisit sections 26–31 and EXP-D00-027
- partial failure / rollback / compensation → revisit sections 32–35 and EXP-D00-027
- workflows / queues / concurrency / locking → revisit sections 36–44 and EXP-D00-028
- blast radius / guardrails / human approval → revisit sections 45–49 and EXP-D00-028
- automation identity / least privilege / secrets → revisit sections 50–52 and EXP-D00-028
- observability / auditability / outcome validation → revisit sections 53–55 and EXP-D00-028
- self-healing / remediation / runbooks → revisit sections 56–59 and EXP-D00-028
- drift / push-pull / economics / reliability-security → revisit sections 60–65
- AI-assisted automation → revisit section 66 and EXP-D00-028
- Senior/SRE/Architect reasoning → revisit sections 69–71

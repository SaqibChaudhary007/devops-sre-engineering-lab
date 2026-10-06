# D00-T003 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- source is developer-authored input
- artifact is a produced delivery/build output
- runtime/interpreter/compiler are distinct but may be combined in real execution models
- dependencies can exist at build time and runtime
- transitive dependencies matter
- lockfiles improve dependency repeatability but do not ensure full reproducibility
- build reproducibility depends on controlled inputs/toolchain/environment
- configuration can change behavior without source modification
- environment differences can create runtime failure
- build, startup and runtime failures are different stages
- exit status communicates process success/failure
- release identity is critical for troubleshooting and rollback

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T003

Critical misconception override: no competency if the learner believes source equals artifact, successful CI guarantees healthy production, or configuration/runtime dependencies do not affect deployment behavior.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Failure-stage classification | 10 |
| Source/artifact mental model | 15 |
| Hypothesis quality | 15 |
| Artifact identity evidence | 15 |
| Configuration reasoning | 15 |
| Safe troubleshooting sequence | 10 |
| SRE/reliability reasoning | 10 |
| Architecture/prevention reasoning | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- classify the failure as startup/configuration related
- avoid blaming source code without evidence
- verify the exact artifact deployed
- compare production configuration with known-good environments
- inspect secret/config injection paths
- use logs and exit status as evidence
- distinguish mitigation from permanent prevention
- propose release/configuration controls

## Follow-Up Evaluation

- L1: defines software lifecycle concepts
- L2: connects source, build, artifact and runtime
- L3: diagnoses build/startup/runtime failures
- L4: connects release quality to SLO and recovery
- L5: evaluates artifact/runtime/supply-chain trade-offs

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. adaptable, production-aware and trade-off aware

Target: 4/5 average.

## Remediation Map

If weak on:

- source/runtime/process → revisit sections 3–10 and OBS-D00-005
- dependencies/packages/versioning → revisit sections 11–16
- build/artifact → revisit sections 18–22 and OBS-D00-006
- configuration/environment → revisit sections 23–27 and EXP-D00-003
- reproducibility/locking → revisit sections 27–28 and source-verification notes
- failure stages → revisit sections 31–34 and EXP-D00-003
- release identity → revisit section 35
- SRE reasoning → revisit sections 38–40
- architecture trade-offs → revisit section 41

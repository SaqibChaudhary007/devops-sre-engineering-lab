
# D00-T001 — Rubric & Self-Review Guide

Use this only after attempting the assessment.

## Knowledge Check — Expected Concepts

1. CPU, memory, storage and network/I/O.
2. CPU executes instructions/work.
3. RAM is active volatile working memory; storage is persistent.
4. A core is a physical execution unit within a processor.
5. A logical CPU/hardware thread is an execution context exposed to the OS and is not always a physical core.
6. Cache reduces the latency gap between CPU execution and slower memory.
7. I/O is data movement to/from devices such as storage and network.
8. Storage latency is time taken for an operation.
9. Throughput is amount of work/data completed per unit time.
10. IOPS is I/O operations per second.

For questions 11–25, award strongest marks when the learner:

- explains relationships rather than reciting definitions
- avoids absolute conclusions
- distinguishes evidence from proof
- identifies waiting/dependency behavior
- recognizes queueing and saturation
- connects metrics to workload context

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T001

Critical misconception override: a learner cannot be marked competent if they still believe one metric alone proves health/root cause.

## Applied Scenario Rubric — 100 Points

| Dimension | Points |
|---|---:|
| Impact & scope | 15 |
| Architecture understanding | 10 |
| Evidence interpretation | 15 |
| Hypothesis quality | 15 |
| Avoiding premature conclusions | 10 |
| Next-evidence selection | 10 |
| Senior troubleshooting structure | 10 |
| SRE reasoning | 10 |
| Architecture/trade-offs | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should treat storage latency as a leading hypothesis, not a proven root cause.

It should request evidence such as:

- storage wait/queue behavior
- database wait states
- per-request timing
- whether all requests are affected
- dependency timing
- historical baseline

It should avoid random restarts before evidence collection unless mitigation urgency justifies it.

## Follow-Up Evaluation

- L1: defines the component
- L2: connects components
- L3: reasons about failure and waiting
- L4: connects to SLO/user impact
- L5: discusses constraints and trade-offs

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. clear, accurate, adaptable and production-aware

Target: 4/5 average.

## Remediation Map

If weak on:

- CPU/core/cache → revisit CPU section
- memory/storage distinction → revisit memory hierarchy
- I/O/waiting → revisit I/O and bottlenecks
- utilization/saturation → revisit performance section
- scenario reasoning → repeat OBS-D00-001 and EXP-D00-001
- process model → repeat OBS-D00-002
- SRE reasoning → revisit user-impact vs resource-metric section
- architecture reasoning → revisit bottleneck, scale and trade-off sections

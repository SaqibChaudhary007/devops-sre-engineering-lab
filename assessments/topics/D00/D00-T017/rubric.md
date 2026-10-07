# D00-T017 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- systems are defined by interactions and outcomes, not just parts
- boundaries are chosen for the question being analyzed
- environment and interfaces matter
- state/stock accumulates over time
- flows change stocks
- constraints shape throughput
- bottlenecks can migrate
- local optimization can harm the global outcome
- queues create buffering and delay
- saturation increases instability
- reinforcing loops amplify behavior
- balancing loops counteract deviation
- delays can create over-correction and oscillation
- hidden coupling creates surprising correlated failure
- retries are system feedback
- backpressure must propagate upstream
- autoscaling is a delayed control loop
- humans and organizational incentives belong in the system model
- emergent behavior comes from interactions
- cascading failure can involve multiple contributing conditions
- redundancy is only valuable when relevant failure modes are sufficiently independent
- second-order effects matter
- architecture decisions are interventions
- SLOs represent system outcomes

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T017

Critical misconception override: no competency if the learner believes component health proves system health, local optimization always helps globally, more capacity is always the answer, retries cannot amplify overload, autoscaling is instantaneous, redundancy automatically means independence, or every incident has exactly one isolated root cause.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| System boundary / context / flows | 10 |
| Stocks / constraints / bottleneck reasoning | 15 |
| Local vs global optimization / critical path | 10 |
| Feedback loops / delays / oscillation | 15 |
| Retry amplification / backpressure / autoscaling | 15 |
| Queue / saturation interpretation | 10 |
| Hidden coupling / common failure domains | 10 |
| Cascading failure / blast radius | 5 |
| Second-order effects / leverage points | 5 |
| Senior / SRE / Architect target design | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- choose a system boundary appropriate to checkout SLO analysis
- map multiple interacting flows
- distinguish state/stock from flow
- identify the active bottleneck using evidence
- predict bottleneck migration
- reject local optimization as automatically globally beneficial
- identify reinforcing and balancing loops
- include feedback delays
- show how retries amplify downstream pressure
- use backpressure as a chain-level behavior
- interpret queue age and throughput, not depth alone
- identify hidden/common-mode dependencies
- map cascading failure across technical and human systems
- distinguish redundancy from independence
- identify second-order effects
- rank interventions by leverage rather than size

## Follow-Up Evaluation

- L1: defines systems concepts
- L2: connects boundaries, flows, constraints, and feedback
- L3: reasons through system-level production behavior
- L4: applies SRE thinking to feedback, overload, and stability
- L5: designs architecture interventions and trade-offs

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

- system / boundary / environment → revisit sections 3–7 and OBS-D00-021
- inputs / outputs / flows / state → revisit sections 8–10 and OBS-D00-021
- constraints / bottlenecks / throughput / latency → revisit sections 11–17 and OBS-D00-021
- queues / stocks / flows / capacity → revisit sections 18–22 and OBS-D00-021
- feedback loops / delays / oscillation → revisit sections 23–29 and EXP-D00-029
- nonlinearity / thresholds / coupling → revisit sections 30–33
- dependency chains / critical path / contention / backpressure → revisit sections 34–38 and EXP-D00-029
- retries / autoscaling / alerting / automation feedback → revisit sections 39–42 and EXP-D00-029
- human / organizational feedback → revisit sections 43–45
- emergent behavior / cascading failure / blast radius → revisit sections 46–49 and EXP-D00-030
- second-order effects / trade-offs / leverage → revisit sections 50–53 and EXP-D00-030
- symptoms / patterns / structure → revisit sections 54–56 and EXP-D00-030
- observability / SLOs / architecture interventions → revisit sections 57–62 and EXP-D00-030
- Senior/SRE/Architect reasoning → revisit sections 65–67

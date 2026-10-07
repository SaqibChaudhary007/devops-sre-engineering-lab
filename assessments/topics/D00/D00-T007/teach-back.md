# D00-T007 — Teach-Back Assessment

## Goal

Demonstrate that you can explain DevOps without turning the explanation into a tool list.

## Task A — Beginner

Explain:

- what DevOps is
- why it exists
- why DevOps is not a single tool or team

Use one simple analogy.

## Task B — Engineer

Explain:

~~~text
Idea
→ Code
→ Build
→ Test
→ Deploy
→ Operate
→ Observe
→ Learn
~~~

Then identify:

- one queue
- one handoff
- one bottleneck
- one feedback loop

## Task C — Senior Engineer

Explain why this statement is incomplete:

> "Our developers are fast, so delivery is fast."

Include:

- WIP
- queues
- handoffs
- batch size
- bottlenecks
- waiting time

## Task D — DORA Metrics

Explain the current five metrics:

~~~text
Throughput
├── Change Lead Time
├── Deployment Frequency
└── Failed Deployment Recovery Time

Instability
├── Change Fail Rate
└── Deployment Rework Rate
~~~

Then explain why none should be optimized alone.

## Task E — SRE

Explain how deployment design affects:

- reliability
- SLOs
- recovery
- blast radius
- toil

## Task F — Architect

Compare:

~~~text
DevOps
vs
SRE
vs
Platform Engineering
~~~

Explain:

- overlap
- differences
- when each helps
- why none is simply a replacement for the others

## Toil Challenge

Classify and explain:

- repetitive manual deployment
- incident command decision
- automated environment reset
- architecture review
- repeated permission creation

## Blameless Learning Challenge

Explain why:

> "Blameless" does not mean "nobody is accountable."

## Scoring

Score 1–5 for:

- correctness
- clarity
- flow reasoning
- feedback reasoning
- DORA metric reasoning
- reliability awareness
- architecture / organizational trade-off awareness

Target: average 4/5 with no critical misconception.

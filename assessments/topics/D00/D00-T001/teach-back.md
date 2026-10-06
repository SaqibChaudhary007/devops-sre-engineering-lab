
# D00-T001 — Teach-Back Assessment

## Goal

Prove that you understand the system well enough to explain it at multiple levels.

## Task A — Beginner

Explain in plain language:

- CPU
- memory
- storage
- network

Constraint: avoid deep jargon.

## Task B — Engineer

Explain:

~~~text
Program
→ Process
→ Operating System
→ CPU / Memory / I/O
~~~

Include one real example.

## Task C — Senior Engineer

Explain why this statement is wrong:

> “CPU is low, therefore the server is healthy.”

Your explanation should include:

- waiting
- I/O
- dependencies
- bottlenecks
- evidence

## Task D — SRE

Explain why:

> “High CPU” and “user-facing outage”

are not the same thing.

Include:

- utilization
- saturation
- latency/errors
- service impact

## Task E — Architect

A system must handle 10× growth.

Explain what you would investigate before recommending:

- larger machines
- more machines
- caching
- faster storage
- architectural redesign

## Diagram Challenge

Draw from memory:

~~~text
Application
   ↓
Operating System
   ↓
CPU / Memory / I/O
            ↓
      Storage / Network
~~~

Then add:

- one possible bottleneck
- one dependency
- one user-facing symptom

## Rubric Dimensions

Score 1–5 for:

- correctness
- clarity
- structure
- appropriate depth
- examples
- system connection
- ability to answer follow-ups

Target: average 4/5 with no major technical misconception.

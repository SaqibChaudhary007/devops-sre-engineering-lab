# D00-T003 — Teach-Back Assessment

## Goal

Demonstrate that you can explain the software lifecycle at multiple levels of depth.

## Task A — Beginner

Explain:

- source code
- compiler/runtime
- artifact
- process

Use simple language and one analogy.

## Task B — Engineer

Explain this flow:

~~~text
Source
→ Dependencies
→ Build
→ Artifact
→ Configuration
→ Runtime
→ Process
~~~

Include one compiled example and one runtime-driven example.

## Task C — Senior Engineer

Explain why this statement is wrong:

> "CI passed, so production should work."

Include:

- artifact
- runtime dependency
- configuration
- environment
- startup failure
- external dependency

## Task D — SRE

Explain how poor release identity and dependency control can increase incident duration.

Include:

- exact version
- change correlation
- rollback
- reproducibility
- deployment events

## Task E — Architect

Explain the design trade-offs involved in choosing:

~~~text
native compiled artifact
vs
runtime-dependent artifact
vs
container image
~~~

Include:

- portability
- runtime dependencies
- performance
- image/artifact size
- security
- supportability
- operational complexity

## Diagram Challenge

Draw from memory:

~~~text
Source
  ↓
Build
  ↓
Artifact
  ↓
Configuration + Runtime
  ↓
Process
  ↓
User
~~~

Then add:

- one build-time dependency
- one runtime dependency
- one startup failure
- one runtime failure
- one version identifier

## Scoring

Score 1–5 for:

- correctness
- clarity
- structure
- appropriate depth
- examples
- production connection
- follow-up handling

Target: average 4/5 with no critical misconception.

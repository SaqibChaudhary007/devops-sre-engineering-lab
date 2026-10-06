
# D00-T002 — Teach-Back Assessment

## Goal

Demonstrate that you can explain operating-system concepts at increasing levels of depth.

## Task A — Beginner

Explain:

- operating system
- kernel
- process
- user space

Use simple language and one analogy.

## Task B — Engineer

Explain this flow:

~~~text
Application
→ System Call
→ Kernel
→ Resource / Device
~~~

Include one file example and one network example.

## Task C — Senior Engineer

Explain why this statement is wrong:

> "The process is running, so the service is healthy."

Include:

- process state
- sockets
- files
- permissions
- dependencies
- waiting

## Task D — SRE

Explain how an operating-system problem could cause an SLO violation without high CPU or memory usage.

Use at least two examples.

## Task E — Architect

Compare:

~~~text
Virtual Machine
vs
Container
~~~

from the operating-system perspective.

Include:

- kernel model
- isolation
- resource control
- failure domain
- operational trade-offs

## Diagram Challenge

Draw from memory:

~~~text
User Space
   ↓
System Calls
   ↓
Kernel
   ↓
CPU / Memory / Filesystem / Network / Devices
~~~

Then add:

- one security boundary
- one OS resource limit
- one production failure scenario

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

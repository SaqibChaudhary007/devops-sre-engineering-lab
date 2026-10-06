
# D00-T002 — Applied Scenario

## Scenario

Architecture:

~~~text
Users
  ↓
Reverse Proxy
  ↓
Application Process
  ↓
Local Files + Remote Database
~~~

Symptoms:

~~~text
Application process exists
CPU usage: low
Memory usage: normal
Service latency: high
Some requests fail
Recent deployment: none
Application logs:
  "Too many open files"
  "Connection failed"
Host load: moderate
Disk capacity: healthy
~~~

## Task 1 — Impact and Scope

Answer:

1. What is the user-visible impact?
2. What do you know about application-process health?
3. What important information is still missing?

## Task 2 — OS-Level Hypotheses

List your top four hypotheses.

Consider areas such as:

- file descriptors
- sockets
- process limits
- dependency connections
- process state
- kernel/network behavior

For each hypothesis, state:

- why it is plausible
- what evidence supports it
- what evidence you would collect next

## Task 3 — Weak Conclusions

Explain why each statement is weak:

- "The process is running, so the application is healthy."
- "CPU is low, so this cannot be an OS problem."
- "Restart the host."
- "The database must be down."

## Task 4 — Next Evidence

What would you inspect next?

Examples of categories:

- process limits
- open file count
- socket state
- process state
- application connection pools
- host-wide file-descriptor pressure
- dependency reachability
- kernel/system logs

Do not jump to a destructive change before establishing evidence.

## Task 5 — Senior Engineer Response

Write a troubleshooting path using:

~~~text
Impact
→ Scope
→ Process State
→ OS Resources
→ Evidence
→ Hypotheses
→ Safe Test
→ Mitigation
→ Root Cause
→ Prevention
~~~

## Task 6 — SRE View

Answer:

1. Which user-facing indicators matter most here?
2. Is "process exists" a good availability SLI?
3. How could an OS limit cause SLO impact without high CPU or memory?
4. What could be monitored proactively?

## Task 7 — Architect View

Suppose the issue is repeated file-descriptor and connection exhaustion during peak traffic.

What design questions would you ask before simply raising OS limits?

Consider:

- connection lifecycle
- pooling
- downstream capacity
- backpressure
- concurrency
- retry behavior
- workload scaling
- host limits
- container limits
- observability
- cost/complexity

## Success Standard

A strong answer recognizes that an alive process can still be unhealthy, treats OS resource limits as strong hypotheses, requests targeted evidence and avoids treating a restart or higher limits as an automatic permanent fix.

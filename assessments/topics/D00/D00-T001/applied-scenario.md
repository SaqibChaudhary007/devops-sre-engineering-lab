
# D00-T001 — Applied Scenario

## Scenario

Architecture:

~~~text
Users
  ↓
Web Application
  ↓
Database
  ↓
SSD Storage
~~~

Current observations:

~~~text
Web CPU:             28%
Web memory:          normal
Database CPU:        31%
Database memory:     normal
Request latency:     4–6 seconds
Error rate:          low
Storage utilization: moderate
Storage latency:     very high
Traffic:             unchanged
Recent deployment:   none
~~~

## Task 1 — Impact and Scope

Answer:

1. What do you know about user impact?
2. What do you still need to know?
3. Is this likely a total outage, partial degradation or unknown? Why?

## Task 2 — Hypotheses

List your top three hypotheses in order.

For each one, state:

- why it is plausible
- what evidence supports it
- what evidence is still missing

## Task 3 — Avoid Premature Conclusions

Explain why these answers are weak:

- “CPU is fine, so the server is healthy.”
- “Storage latency is high, so storage is definitely the root cause.”
- “Restart the database.”

## Task 4 — Next Evidence

What would you want to inspect next?

Think about:

- database wait behavior
- disk I/O latency/queues
- request timing
- dependency timing
- recent system changes
- whether all requests are affected

## Task 5 — Senior Engineer Response

Write a short investigation plan using:

~~~text
Impact
→ Scope
→ Evidence
→ Hypotheses
→ Test
→ Mitigation
→ Root Cause
→ Prevention
~~~

## Task 6 — SRE View

Answer:

1. Which user-facing signal matters most here?
2. Would CPU utilization alone be a good paging signal?
3. What would determine whether this condition is consuming reliability/error budget?

## Task 7 — Architect View

Suppose this problem is caused by storage latency under peak load and is expected to worsen as traffic grows 10×.

What design questions would you ask before choosing a solution?

Consider:

- workload type
- state
- latency target
- throughput
- scaling model
- cost
- failure domains
- operational complexity

## Success Standard

A strong answer identifies storage as a strong hypothesis without pretending the root cause is proven, requests relevant evidence, connects technical behavior to user impact and avoids jumping straight to a tool or restart.

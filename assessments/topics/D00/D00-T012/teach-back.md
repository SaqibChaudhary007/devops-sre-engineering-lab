# D00-T012 — Teach-Back Assessment

## Goal

Demonstrate that you can explain reliability engineering from the user journey through detection, containment, recovery, and improvement.

## Task A — Beginner

Explain:

- reliability
- availability
- durability
- resilience
- recoverability

Keep the differences clear.

## Task B — User Journey

Explain why:

~~~text
"All servers are healthy"
~~~

does not prove:

~~~text
"The user can successfully check out"
~~~

## Task C — Redundancy

Explain why:

~~~text
3 replicas in one failure domain
~~~

may be less resilient than:

~~~text
2 replicas in independent failure domains
~~~

## Task D — SLI / SLO / SLA

Explain each term using one checkout example.

Then explain an error budget.

## Task E — Recovery

Explain:

- detection time
- response time
- recovery time
- MTTR
- why these should not be collapsed into one vague "incident duration"

## Task F — Backup / RTO / RPO

Explain why:

~~~text
Backup Exists
≠
Recovery Proven
~~~

Then distinguish RTO from RPO.

## Task G — Senior Engineer

Explain how to investigate:

~~~text
Node failure
→ capacity loss
→ latency
→ retries
→ saturation
→ checkout errors
~~~

without starting from random infrastructure commands.

## Task H — SRE

Explain how a critical user journey maps to:

~~~text
SLI
→ SLO
→ Error Budget
→ Operational Decision
~~~

## Task I — Architect

Explain how you would balance:

- reliability target
- failure-domain independence
- headroom
- redundancy
- graceful degradation
- recovery objectives
- cost
- operational complexity

## Task J — Production Readiness

Explain which evidence you would require before calling a new service production-ready.

## Scoring

Score 1–5 for:

- correctness
- clarity
- user-centered reliability reasoning
- failure-domain/redundancy reasoning
- SLI/SLO/error-budget reasoning
- recovery reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

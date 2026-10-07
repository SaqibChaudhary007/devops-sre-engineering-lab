# D00-T013 — Teach-Back Assessment

## Goal

Demonstrate that you can explain SRE as an engineering operating model, not just as monitoring or on-call.

## Task A — Beginner

Explain:

- what SRE is
- why SRE exists
- how SRE differs from purely manual operations

## Task B — SRE vs DevOps

Explain the overlap without claiming they are identical or completely separate.

## Task C — Service Objectives

Explain:

~~~text
User Journey
→ SLI
→ SLO
→ Error Budget
→ Engineering Decision
~~~

Use one checkout example.

## Task D — Paging

Explain:

- page
- ticket
- dashboard/context
- urgency
- actionability
- user impact

## Task E — Toil and Automation

Explain:

- what toil is
- what toil is not
- why automation should follow understanding
- how unsafe automation can increase blast radius

## Task F — Incident Response

Explain why:

~~~text
Reduce User Impact
→ Stabilize
→ Validate
→ Deep Root-Cause Work
~~~

can be stronger than waiting for perfect root cause before mitigation.

## Task G — Postmortem

Explain:

- what a postmortem is
- what blameless means
- why blameless is not accountability-free
- what makes an action item strong

## Task H — Safe Change

Explain:

~~~text
Small Change
→ Automated Checks
→ Limited Exposure
→ Observe
→ Continue / Stop / Recover
~~~

Then explain why a canary does not prove correctness.

## Task I — SRE

Explain how on-call pain, toil, SLOs, error budgets, release risk, and engineering work connect.

## Task J — Architect

Explain how you would design:

- SRE ownership
- SLO boundaries
- dependency reliability
- production-readiness gates
- progressive delivery
- on-call sustainability

## Scoring

Score 1–5 for:

- correctness
- clarity
- SRE operating-model reasoning
- SLI/SLO/error-budget reasoning
- paging/on-call reasoning
- toil/automation reasoning
- incident/postmortem reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.

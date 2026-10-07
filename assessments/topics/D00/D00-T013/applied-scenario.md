# D00-T013 — Applied SRE Scenario

## Scenario

A checkout service operates with:

~~~text
User Journey
→ Checkout API
→ Authentication
→ Order Service
→ Payment Provider
→ Database
→ Queue
~~~

Current operating model:

~~~text
- SLO: 99.9% successful checkout events over 30 days
- team pages on CPU > 80%
- no page on checkout success ratio
- noisy alerts wake on-call several times per week
- repeated manual restart is the common workaround
- payment provider occasionally slows down
- retries occur at multiple layers
- release process deploys 100% of traffic immediately
- one recent deployment caused a 12-minute outage
- postmortem action item was "be more careful"
- ownership of the checkout SLO is unclear
- production-readiness checklist does not exist
~~~

At 14:00:

~~~text
Payment latency rises
→ checkout success falls
→ retry traffic increases
→ queue age increases
→ CPU remains normal
→ page fires only at 14:09 after a secondary CPU spike
→ on-call begins at 14:13
→ repeated restart does not help
→ team reduces retries at 14:19
→ checkout recovers at 14:27
→ user journey validated at 14:31
~~~

## Task 1 — Define the User Journey and Service Boundary

Define:

- what service is being measured
- what counts as a good checkout event
- which dependencies affect the outcome
- which boundaries belong to the service vs external dependencies

## Task 2 — SLI / SLO / SLA

Propose:

- one success SLI
- one latency SLI
- one conceptual SLO
- one conceptual external SLA

Explain the differences.

## Task 3 — Error Budget

Explain:

- what the checkout error budget represents
- how this incident consumes it
- what decisions unhealthy consumption might influence
- why one universal freeze rule should not be assumed

## Task 4 — Alert Review

Evaluate:

~~~text
CPU > 80%
→ Page
~~~

Explain why it is weak by itself.

Design a stronger page using:

- checkout success impact
- payment dependency behavior
- retry pressure
- queue age
- current saturation context

## Task 5 — Page vs Ticket vs Dashboard

Classify:

- checkout success sharply below objective
- payment provider hard failure
- disk trend likely to become risky next week
- one noncritical worker restart
- repeated manual restart workaround
- low-priority warning with no impact

Explain each decision.

## Task 6 — Incident Timeline

From the timestamps, identify:

- time to detect
- time to respond
- time to mitigate
- time to recover
- time to validate

Explain what each interval says about the operating model.

## Task 7 — Mitigation vs Root-Cause Correction

Classify:

- reduce retry limit
- disable noncritical features
- switch to alternate dependency path
- redesign retry ownership
- add dependency SLO
- improve alert context
- remove repeated restart workaround

Use:

~~~text
Immediate Mitigation
Permanent Improvement
Can Be Either
~~~

## Task 8 — Toil Review

Classify:

- repeated manual restart
- recurring copy/paste health check
- one-time deep incident analysis
- building a durable automation system
- repeated certificate-renewal ticket
- architecture redesign

Explain why toil is multi-dimensional.

## Task 9 — Automation Candidate

Choose one toil item.

Design:

~~~text
Preconditions
→ Safe Boundary
→ Automation
→ Observability
→ Validation
→ Stop / Override
~~~

Explain how poor automation could increase blast radius.

## Task 10 — On-Call Sustainability

Evaluate:

- noisy pages
- repeated workaround
- unclear ownership
- missing runbook
- recurring payment dependency issue

Identify which should become engineering work.

## Task 11 — Safe Change / Progressive Delivery

Replace:

~~~text
Deploy 100% immediately
~~~

with:

~~~text
Small Change
→ Automated Checks
→ Limited Exposure
→ Observe
→ Continue / Stop / Recover
~~~

Define the signals that should determine rollout progression.

## Task 12 — Canary Limitations

Explain why a healthy canary does not guarantee the full rollout is correct.

Discuss:

- representative traffic
- observation time
- low-frequency failures
- dependency interaction
- stop/rollback capability

## Task 13 — Postmortem Review

Rewrite:

~~~text
"Be more careful next time"
~~~

into specific, owned, testable reliability actions.

## Task 14 — Blameless Learning

Explain how to investigate:

- why retries amplified the incident
- why detection took nine minutes
- why page context was weak
- why restarts were the default response
- why ownership was unclear

without reducing the incident to individual blame.

## Task 15 — Production Readiness

Score:

~~~text
Ready
Partially Ready
Not Ready
~~~

for:

- user journey defined
- SLI
- SLO
- actionable page
- dependency map
- runbook
- ownership
- capacity/headroom understanding
- safe release path
- rollback/roll-forward strategy
- recovery validation
- postmortem process

## Task 16 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Impact
→ User Journey
→ Service Boundary
→ SLI
→ Alert
→ Dependency Evidence
→ Mitigation
→ Recovery Validation
~~~

### SRE

Connect:

- SLO
- error budget
- page quality
- on-call load
- toil
- safe change
- postmortem
- action items

### Architect

Redesign:

- ownership model
- SLO boundaries
- dependency strategy
- progressive delivery
- capacity/headroom
- operational readiness gates

## Success Standard

A strong answer should explicitly reject:

- SRE = monitoring
- every alert should page
- CPU threshold = sufficient reliability signal
- error budget = permission to be careless
- toil = any operational work
- restart = root cause
- canary = proof of correctness
- postmortem = blame assignment

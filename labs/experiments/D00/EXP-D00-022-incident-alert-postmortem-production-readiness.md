---
id: EXP-D00-022
domain: D00
topics:
  - D00-T013
level: L2-L3
type: experiment
status: draft
estimated_time: 60-80m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-022 — Incident Response, Alert Actionability, Postmortem, and Production Readiness

## Objective

Practice SRE reasoning across incident detection, page quality, mitigation, recovery validation, postmortem learning, and production readiness.

## Safety

This is a local reasoning exercise.

No production changes, live incident manipulation, paging integration, or destructive testing is required.

## Scenario

A checkout service has:

~~~text
SLO = 99.9% successful checkout events over 30 days

At 14:00:
- payment latency rises
- checkout success begins falling
- CPU remains normal
- retry traffic increases
- queue age increases
- page fires at 14:09
- on-call starts investigation at 14:13
- recommendation service is disabled at 14:18
- retry limit is reduced at 14:21
- checkout recovers at 14:27
- service is validated at 14:31
~~~

Afterward, the team writes:

~~~text
Root cause: payment dependency slowdown
Action item: "Be more careful next time"
~~~

## 1. Build the Incident Timeline

Map:

~~~text
Impact Begins
→ Detection
→ Human Response
→ Mitigation
→ Recovery
→ Validation
~~~

Calculate conceptually:

- time to detect
- time to respond
- time to mitigate
- time to recover
- time to validate

Explain why these intervals reveal different reliability weaknesses.

## 2. Page Quality Review

The original page was:

~~~text
Payment latency high
~~~

Evaluate it against:

- urgency
- actionability
- user impact
- useful context

Design a stronger page that includes:

- checkout success impact
- payment dependency signal
- retry pressure
- current saturation/backlog context

## 3. Page vs Ticket vs Dashboard

Classify:

- checkout success below SLO threshold
- one noncritical worker restart
- queue growth trend that will become risky tomorrow
- payment provider hard failure blocking checkout
- one low-priority log warning
- repeated manual incident workaround

Use:

~~~text
Page
Ticket
Dashboard / Context
Depends on Policy
~~~

Explain each choice.

## 4. Mitigation vs Permanent Correction

Classify:

~~~text
Disable noncritical recommendations
Reduce retry limit
Fail over to a healthy payment path
Tune dependency timeout
Redesign retry ownership
Add dependency SLO
Create automated guardrail
~~~

as:

~~~text
Immediate Mitigation
Permanent / Preventive Improvement
Can Be Either
~~~

Explain why restoring service can come before complete root-cause correction.

## 5. Recovery Validation

Define what proves the service is actually recovered:

- checkout success ratio restored
- latency returned to acceptable range
- retry volume normalized
- queue age falling
- payment dependency stable
- no duplicate side effects
- user journey works end to end

Explain why infrastructure state alone is weak recovery evidence.

## 6. Postmortem Review

The action item:

~~~text
"Be more careful next time"
~~~

is weak.

Rewrite it into concrete system-improvement actions such as:

- define payment dependency SLO
- add retry-budget visibility
- improve page context
- add graceful degradation
- clarify ownership
- validate recovery runbook

Keep actions specific, owned, and testable.

## 7. Blameless Learning

Explain how to investigate:

- why retry pressure increased
- why detection took nine minutes
- why the page lacked user-impact context
- why recommendation failure affected recovery
- why the dependency slowdown had broad impact

without reducing the incident to individual blame.

Also explain why blameless does not mean ignoring responsibility or standards.

## 8. On-Call Load

Review:

- page frequency
- repeated workaround
- alert noise
- unclear ownership
- missing runbook
- recurring dependency issues

Identify which items should become engineering work.

## 9. Production Readiness Review

For a new service, score:

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
- dashboard
- runbook
- dependency map
- capacity/headroom understanding
- safe change path
- rollback/roll-forward plan
- ownership
- recovery validation
- post-incident review process

## 10. Release Safety Preview

A new version is planned.

Design a conceptual release flow:

~~~text
Small Change
→ Automated Checks
→ Limited Exposure
→ Observe User-Centered Signals
→ Continue / Stop / Recover
~~~

Explain what would cause rollout to stop.

## 11. Senior Engineer Connection

Use:

~~~text
Impact
→ Timeline
→ Page Quality
→ Dependency Evidence
→ Mitigation
→ Recovery Validation
→ Preventive Action
~~~

## 12. SRE Connection

Connect:

- SLO
- page quality
- error-budget impact
- on-call load
- mitigation
- postmortem
- toil reduction
- reliability action items

## 13. Architect Connection

Ask:

- which dependencies need stronger isolation?
- where should graceful degradation exist?
- what operational readiness gates should block launch?
- which SLOs belong at service vs dependency boundaries?
- what should be automated vs remain a human decision?

## Validation Checklist

- [ ] Built an incident timeline
- [ ] Evaluated page quality
- [ ] Classified page/ticket/dashboard signals
- [ ] Separated mitigation from permanent correction
- [ ] Defined recovery validation
- [ ] Improved postmortem action items
- [ ] Explained blameless systemic learning
- [ ] Identified on-call feedback as engineering input
- [ ] Performed a production-readiness review
- [ ] Designed a limited-exposure release flow

## Teach-Back

Explain:

> "SRE incident response reduces user impact first, validates recovery against the user journey, and converts recurring operational pain into concrete engineering improvements."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

# D00-T013 Source Verification — SRE Foundations

## Verification Goal

Verify the core claims in **00.13 — SRE Foundations** against authoritative SRE and operational-reliability guidance.

Primary sources used:

- Google Site Reliability Engineering book
- Google SRE Workbook
- AWS Well-Architected Operational Excellence guidance
- Microsoft Azure Well-Architected operational/reliability guidance

## Verification Status

**Result:** Core claims verified with important nuances around SRE identity, SLOs, error budgets, toil, paging, on-call, incident response, postmortems, release engineering, safe change, capacity, and production readiness.

**Evidence level:** E2 — supported by first-party SRE literature and current cloud-provider operational guidance.

This topic remains at the D00 mental-model level. Detailed SLO implementation, burn-rate alerting, error-budget automation, incident-command mechanics, quantitative toil programs, on-call program design, capacity models, and platform-specific SRE implementation belong to later domains.

---

# Primary / Authoritative Sources

## 1. Google SRE — Introduction

- https://sre.google/sre-book/introduction/

Supports:

- SRE applies software-engineering approaches to operational problems
- SRE is intentionally different from a purely manual operations model
- engineering should replace repetitive operational work where appropriate
- operational load must remain bounded enough to leave time for engineering improvements

### Verified nuance

The canonical topic should avoid claiming that SRE means "no operations."

The stronger mental model is:

~~~text
Operational Work
→ Measure
→ Understand
→ Engineer
→ Automate Where Appropriate
→ Reduce Repetition
→ Preserve Human Judgment Where Needed
~~~

---

## 2. Google SRE — Service Level Objectives

- https://sre.google/sre-book/service-level-objectives/

Supports:

- SLIs represent measurable service behavior
- SLOs define desired targets for those indicators
- SLAs are different from internal SLOs
- targets should be selected based on service/user needs
- 100% reliability is generally unrealistic and undesirable
- SLOs should drive operational and engineering decisions

### Verified nuance

A useful SRE sequence is:

~~~text
User Need
→ SLI
→ SLO
→ Decision
~~~

not:

~~~text
Available Metric
→ Alert
→ Call It Reliability
~~~

---

## 3. Google SRE — Embracing Risk / Error Budgets

- https://sre.google/sre-book/embracing-risk/
- https://sre.google/sre-book/service-best-practices/
- https://sre.google/workbook/error-budget-policy/

Supports:

- error budgets balance reliability with innovation/change velocity
- error budget is conceptually derived from the SLO
- error-budget status can influence release/risk decisions
- reliability and product-development teams benefit from a shared objective measure of acceptable unreliability

### Verified nuance

Error-budget policy is **not universal**.

Google's examples are examples of policy.

At D00, teach:

> Error-budget health should influence risk and engineering decisions through an explicit organizational policy.

Do not teach one vendor/company policy as a universal rule.

---

## 4. Google SRE — Eliminating Toil

- https://sre.google/sre-book/eliminating-toil/
- https://sre.google/workbook/eliminating-toil/

Supports:

- toil is not simply "work people dislike"
- toil tends to be manual, repetitive, automatable, tactical, lacking enduring value, and scaling with service growth
- excessive toil consumes engineering capacity
- SRE uses engineering to reduce recurring operational work

### Verified nuance

Not every operational task is toil.

Novel diagnosis, engineering work, and work that creates enduring improvement should not automatically be labeled toil.

Google's 50% operational-work target is an organizational practice, not a universal law.

---

## 5. Google SRE — Monitoring, Pages, Tickets, and Operational Load

- https://sre.google/sre-book/dealing-with-interrupts/
- https://sre.google/sre-book/table-of-contents/

Supports:

- pages and tickets have different urgency/response expectations
- not every operational signal should interrupt a human immediately
- excessive interrupts create unsustainable operational load
- monitoring and alerting are fundamental inputs to reliable operations

### Verified nuance

At D00:

~~~text
Page
→ urgent + actionable + immediate response required

Ticket
→ action required, but not immediate interruption

Dashboard
→ context / investigation / awareness
~~~

Exact operational policies differ by organization.

---

## 6. Google SRE Workbook — SLOs, Alerting, On-Call, Incident Response, Postmortems

- https://sre.google/workbook/index/
- https://sre.google/workbook/preface/

The workbook explicitly organizes SRE practice around:

- implementing SLOs
- monitoring
- alerting on SLOs
- eliminating toil
- on-call
- incident response
- postmortem culture
- managing load
- canarying releases

This validates the canonical D00-T013 topic boundaries.

---

## 7. Google SRE — Incident Learning / Postmortems

- https://sre.google/sre-book/introduction/
- https://sre.google/sre-book/operational-overload/

Supports:

- significant incidents should create learning
- postmortems should examine contributing factors and system conditions
- blame-focused incident culture can hide system weaknesses
- corrective actions should improve the system rather than only tell individuals to "be more careful"

### Verified nuance

"Blameless" does not mean:

- no accountability
- no standards
- ignoring unsafe decisions

It means investigating the system, information, tools, incentives, and context that shaped decisions so recurrence risk can be reduced.

---

## 8. Google SRE — Release Engineering / Canarying

- https://sre.google/sre-book/release-engineering/
- https://sre.google/workbook/canarying-releases/

Supports:

- reliable services need reliable release processes
- reproducibility and automation improve release safety
- canarying exposes a change to a limited portion of the service before wider rollout
- progressive exposure can reduce blast radius
- rollback and controlled rollout are part of safe delivery

### Verified nuance

Canarying reduces exposure risk.

It does not guarantee correctness.

A canary still requires:

- meaningful signals
- evaluation criteria
- stop/rollback decisions
- sufficient observation time

---

## 9. AWS Well-Architected — Operational Excellence

- https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/prepare.html

Supports:

- operational metrics should align with meaningful business/system outcomes
- observability should support proactive understanding
- safe delivery practices should provide fast feedback
- systems should recover rapidly from changes with undesired outcomes

### Verified nuance

SRE is connected to delivery engineering because change is a normal source of operational risk.

---

## 10. Microsoft Azure Well-Architected — Incident Response / Reliability Monitoring

- https://learn.microsoft.com/en-us/azure/well-architected/operational-excellence/incident-response
- https://learn.microsoft.com/en-us/azure/well-architected/reliability/monitoring

Supports:

- incident response needs explicit roles, procedures, detection, containment, diagnosis, recovery, testing, and learning
- monitoring should focus on meaningful workload/user outcomes
- actionable alerts should represent conditions worth responding to
- metrics, logs, traces, synthetic signals, and health models can be combined for operational understanding
- post-incident findings should become concrete system improvements

### Verified nuance

Incident response is both:

- technical
- procedural

Recovery quality depends on architecture, telemetry, access, roles, coordination, and practiced procedures.

---

# Verified Claim Map

| Topic claim | Verification | Primary source family |
|---|---|---|
| SRE applies software engineering to operations/reliability | Verified | Google SRE |
| SRE is not monitoring-only or on-call-only | Verified | Google SRE book/workbook structure |
| SRE and DevOps overlap but are not identical concepts | Verified at mental-model level | Google SRE Workbook |
| Reliability should begin with user/service behavior | Verified | Google SRE SLO guidance |
| SLI, SLO, and SLA are distinct | Verified | Google SRE |
| 100% reliability is usually the wrong default target | Verified | Google SRE |
| Error budgets balance reliability and change risk | Verified | Google SRE |
| Error-budget policy should influence decisions | Verified | Google SRE |
| Toil is not simply unpleasant work | Verified | Google SRE |
| Excessive toil consumes engineering capacity | Verified | Google SRE |
| Not every alert should page | Verified | Google SRE operational-load guidance |
| On-call requires sustainable operational load | Verified | Google SRE |
| Incident response prioritizes restoring service | Verified at mental-model level | Google/Azure |
| Mitigation and permanent correction are different | Verified at mental-model level | Incident-response practice |
| Postmortems should generate system improvements | Verified | Google/Azure |
| Blameless learning examines systemic contributors | Verified | Google SRE |
| Reliable release processes matter to reliability | Verified | Google SRE release engineering |
| Canary/progressive rollout can reduce exposure | Verified | Google SRE Workbook |
| Capacity/headroom and overload control affect reliability | Verified at mental-model level | Google/Azure |
| Production readiness includes operational readiness | Verified | Google/Azure |

---

# Verified Nuances / Corrections

## 1. SRE Is an Engineering Operating Model

The canonical wording is valid:

~~~text
Operations Problem
→ Measure
→ Understand
→ Engineer
→ Automate Where Useful
→ Reduce Toil
→ Improve Reliability
~~~

Avoid reducing SRE to a job title or toolset.

## 2. SRE vs DevOps Needs Nuance

Do not teach:

~~~text
DevOps = X
SRE = Y
with a hard boundary
~~~

A better D00 model is:

> DevOps is a broad culture and engineering movement; SRE is a concrete reliability-focused operating model that implements many overlapping principles through SLOs, error budgets, toil management, on-call, incident response, and engineering automation.

## 3. SLOs Must Follow User Need

Metrics should be selected because they represent service behavior users care about.

Do not define reliability from arbitrary infrastructure telemetry.

## 4. Error Budgets Are Decision Mechanisms

Conceptually:

~~~text
SLO
→ Allowed Unreliability
→ Error-Budget State
→ Risk / Change Decision
~~~

The exact consequence of budget exhaustion depends on organizational policy.

## 5. Google's Specific Policies Are Examples, Not Universal Rules

Examples such as:

- a 50% operational-work cap
- specific page volumes
- specific freeze rules

are Google practices.

Do not teach them as mandatory SRE standards.

## 6. Toil Is Multi-Dimensional

Toil commonly has characteristics such as:

- manual
- repetitive
- automatable
- tactical
- little enduring value
- scales with service growth

One characteristic alone does not always make work toil.

## 7. Automation Should Follow Understanding

Automation can reduce toil, but unsafe automation can increase blast radius.

A sound mental model is:

~~~text
Understand
→ Define Safe Conditions
→ Automate
→ Observe
→ Validate
→ Improve
~~~

## 8. Not Every Alert Should Interrupt a Human

Urgency and actionability matter.

Use page/ticket/dashboard as mental categories, while recognizing organizations may use different tooling and names.

## 9. On-Call Is an Engineering Feedback Loop

Recurring on-call pain should lead to:

- better alerts
- automation
- architectural improvements
- runbook improvements
- capacity fixes
- dependency fixes

On-call should not be treated as permanent manual firefighting.

## 10. Mitigation Comes Before Perfect Explanation

During an active incident:

~~~text
Reduce User Impact
→ Stabilize
→ Validate
→ Deep Root-Cause Work
~~~

The team still needs evidence and safe decision-making; this does not mean random action.

## 11. Blameless Is Not Accountability-Free

Blameless learning focuses on why actions made sense in context and what systemic conditions enabled the incident.

Standards, responsibility, and follow-through still matter.

## 12. Canarying Is Risk Reduction, Not Proof

Progressive rollout reduces the initial blast radius.

It still depends on:

- representative traffic
- good telemetry
- decision thresholds
- enough observation time
- rollback/stop capability

## 13. Capacity Is Part of SRE

Service reliability can fail through overload even when software is logically correct.

SRE therefore needs mental models for:

- headroom
- saturation
- queueing
- retry load
- load shedding
- backpressure
- dependency capacity

## 14. Production Readiness Is Operational Readiness

A service is not ready merely because it passes functional tests.

Operational readiness includes:

- service objectives
- ownership
- dashboards
- alerts
- runbooks
- capacity understanding
- recovery path
- change safety
- dependency understanding

---

# Evidence Decision

The following D00-T013 areas are now eligible for **DOC-VERIFIED** status:

- SRE definition and purpose
- SRE as engineering applied to operations
- SRE vs traditional operations mental model
- SRE vs DevOps relationship at foundation level
- user-centered reliability
- service-boundary thinking
- SLI/SLO/SLA distinction
- error-budget mental model
- reliability/change-velocity trade-off
- paging vs ticketing
- alert actionability
- sustainable on-call mental model
- toil definition and scaling risk
- automation as toil-reduction engineering
- mitigation vs permanent correction
- incident timeline
- postmortem learning
- blameless systemic learning
- release engineering
- canary/progressive delivery preview
- capacity/headroom/overload mental model
- production readiness
- ownership and continuous reliability review

The following remain intentionally preview-level pending later domains:

- multi-window/multi-burn-rate alerting
- formal SLI/SLO construction and statistical treatment
- detailed error-budget policies
- SRE staffing/engagement models
- quantitative toil programs
- on-call rotation design
- incident-command role mechanics
- capacity forecasting
- automated remediation systems
- production-readiness review governance
- platform-specific SRE implementation

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured exercises:

- map a user journey to an SLI and SLO
- distinguish SLI/SLO/SLA
- calculate conceptual error-budget consumption
- classify page vs ticket vs dashboard signals
- review alert actionability
- classify toil vs non-toil
- identify a safe automation candidate
- build an incident timeline
- separate mitigation from permanent correction
- review a postmortem action item
- evaluate a canary/progressive-delivery decision
- review production readiness

These become the D00-T013 practical package.

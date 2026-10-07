# D00-T012 Source Verification — Reliability Engineering Foundations

## Verification Goal

Verify the core claims in **00.12 — Reliability Engineering Foundations** against authoritative reliability and SRE guidance from Google SRE, AWS Well-Architected, and Microsoft Azure Well-Architected.

## Verification Status

**Result:** Core claims verified with important nuances around user-centered reliability, SLI/SLO/SLA boundaries, error budgets, recovery targets, redundancy, graceful degradation, change risk, observability, and recovery testing.

**Evidence level:** E2 — supported by authoritative engineering guidance and established SRE practice.

This topic remains at the D00 mental-model level. Detailed SLO engineering, error-budget policy, disaster-recovery implementation, chaos engineering, incident command, capacity engineering, and platform-specific reliability patterns belong to later topics.

---

# Primary / Authoritative Sources

## 1. Google SRE — Service Level Objectives

- https://sre.google/sre-book/service-level-objectives/

Supports:

- start from what users care about
- use SLIs to measure service behavior that matters
- define SLOs as targets for those indicators
- distinguish SLOs from SLAs
- avoid targeting 100% reliability by default
- use SLOs as a control signal for engineering decisions

### Verified nuance

A good SLO should be tied to **user-relevant behavior**, not merely to whatever metric is easiest to collect.

---

## 2. Google SRE — Error Budgets and Embracing Risk

- https://sre.google/sre-book/embracing-risk/
- https://sre.google/sre-book/service-best-practices/

Supports:

- 100% reliability is generally not the correct target for software services
- error budget = allowed unreliability derived from the SLO
- error budgets help balance reliability work and change velocity
- service reliability is a business/engineering trade-off, not only a technical maximization problem

### Verified nuance

Error budgets are useful only when they influence decisions. They are not just a reporting number.

---

## 3. AWS Well-Architected — Reliability Pillar / Change Management

- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/change-management.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html

Supports:

- workload reliability must account for both internal and external change
- deployments, patches, and traffic changes can create reliability risk
- systems should be designed to accommodate change
- recovery, monitoring, capacity, and change management are core reliability concerns

### Verified nuance

Change is not an exception to reliability engineering.

It is one of the normal operating conditions a reliable system must handle.

---

## 4. Microsoft Azure Well-Architected — Reliability Targets

- https://learn.microsoft.com/en-us/azure/well-architected/reliability/metrics

Supports:

- reliability targets should map to important workload/user flows
- reliability includes availability and recoverability
- targets should be defined jointly by business and technical stakeholders
- RTO, RPO, MTTR, and MTBF are distinct recovery/reliability measures
- targets should be realistic and tested
- untested recovery metrics should not be treated as guaranteed

### Verified nuance

Reliability targets should be tied to **specific workload flows**, not assumed to apply uniformly across the entire system.

---

## 5. Microsoft Azure Well-Architected — Self-Healing / Self-Preservation

- https://learn.microsoft.com/en-us/azure/well-architected/reliability/self-preservation

Supports:

- design for redundancy
- design for self-preservation and self-healing
- graceful degradation can preserve business functionality during component failure
- monitoring/alerting should detect degraded conditions
- automated rerouting or alternate paths may preserve service where appropriate

### Verified nuance

Self-healing is bounded by architecture.

It does not mean every fault can be repaired automatically.

---

## 6. Microsoft Azure Well-Architected — Monitoring Reliability

- https://learn.microsoft.com/en-us/azure/well-architected/reliability/monitoring

Supports:

- measure time to detect, respond, and recover
- validate recoverability through tests and real incidents
- track failover readiness, failover success, backup/restore success, replication lag, and manual intervention
- telemetry retention matters during incidents
- operational delays and unclear procedures affect recovery

### Verified nuance

Recovery performance is not only a software property.

Human access, documentation, ownership, and procedures can materially affect recovery time.

---

## 7. Microsoft Azure Well-Architected — Reliability Design Principles

- https://learn.microsoft.com/en-us/azure/well-architected/reliability/

Supports:

- design for business requirements
- design for resilience
- design for recovery
- design for operations
- keep designs appropriately simple
- use failure-mode analysis
- test failover and recovery assumptions

### Verified nuance

More redundancy or more complexity is not automatically better reliability.

Reliability design should remain proportional to business need.

---

# Verified Claim Map

| Topic claim | Verification | Primary source family |
|---|---|---|
| Reliability should be tied to user/business-important flows | Verified | Google SRE; Azure WAF |
| Availability is one dimension of reliability | Verified | Azure WAF |
| Reliability includes recoverability | Verified | Azure WAF |
| SLI measures behavior; SLO sets a target; SLA is a commitment | Verified | Google SRE |
| 100% reliability is usually the wrong default target | Verified | Google SRE |
| Error budget represents allowed unreliability | Verified | Google SRE |
| Reliability targets require business/engineering trade-offs | Verified | Google SRE; Azure WAF |
| Change is a reliability risk | Verified | AWS WAF |
| Graceful degradation can preserve critical functionality | Verified | Azure WAF |
| Redundancy must be evaluated against failure domains | Verified at mental-model level | Azure WAF |
| Recovery should be tested, not assumed | Verified | Azure WAF |
| RTO and RPO are different recovery objectives | Verified | Azure WAF |
| MTTR definitions must be stated explicitly | Verified with nuance | Azure WAF |
| Monitoring/alerting affects recovery speed | Verified | Azure WAF |
| Backup success alone does not prove recovery success | Verified in recovery guidance | Azure WAF |
| Capacity and failover readiness should be monitored | Verified | Azure WAF |
| Human procedures/ownership influence recovery | Verified | Azure WAF |

---

# Verified Nuances / Corrections

## 1. Reliability Is Broader Than Availability

The D00 topic is correct to distinguish reliability from uptime/availability.

A service can be:

- technically reachable
- but too slow
- returning incorrect responses
- exposing stale data beyond tolerance
- unable to recover within required time

Therefore reliability should be framed around **acceptable service for important user flows**.

## 2. Critical User Journeys / Flows Are the Right Anchor

Reliability targets should be attached to specific flows such as:

~~~text
Sign In
Checkout
Payment
Message Publish
Record Retrieval
~~~

This is stronger than assigning one generic reliability number to the whole platform.

## 3. SLI, SLO, and SLA Must Stay Separate

Canonical D00 interpretation:

~~~text
SLI
→ measured service behavior

SLO
→ target for that behavior

SLA
→ formal commitment / agreement, often with business consequences
~~~

Do not use these terms interchangeably.

## 4. Error Budget = Allowed Unreliability

At D00:

~~~text
100% - SLO
→ conceptual error budget
~~~

But the important lesson is operational:

> Error budgets should influence decisions about risk, change, and reliability work.

## 5. 100% Is Usually the Wrong Default

The curriculum should avoid teaching maximum reliability as an absolute objective.

Higher reliability can create disproportionate cost and complexity.

Targets should align with user need and business value.

## 6. MTTR Is Ambiguous Without a Definition

"MTTR" may be expanded as:

- mean time to restore
- mean time to recover
- mean time to repair

The metric must be explicitly defined before use.

Averages can also hide severe tail incidents.

## 7. RTO and RPO Are Different

~~~text
RTO
→ maximum acceptable recovery time

RPO
→ maximum acceptable data-loss window
~~~

They answer different questions and must not be merged into one "DR target."

## 8. Recovery Must Be Proven

A backup does not prove recoverability.

A failover design does not prove failover success.

Recovery confidence comes from:

- restore testing
- failover exercises
- measured recovery timing
- validation of restored service/data
- clear ownership and access

## 9. Redundancy Requires Independence

More replicas are only useful when they do not share the same critical failure mode.

Correlated dependencies such as:

- one zone
- one storage system
- one network path
- one identity provider
- one control plane

can defeat superficial redundancy.

## 10. Graceful Degradation Is a Reliability Strategy

When a noncritical dependency fails, the system may preserve important flows by reducing functionality.

Example:

~~~text
Recommendation service unavailable
→ Checkout remains available
~~~

This is valid only when business correctness allows it.

## 11. Change Is a Normal Reliability Input

Changes include:

- deployments
- configuration updates
- security patches
- infrastructure changes
- traffic spikes
- dependency changes

Reliable systems must accommodate these changes safely.

## 12. Alert Quality Matters

Alerts should help operators decide what action is needed.

Component-level metrics can be useful evidence, but user-impact signals and service objectives should guide priority.

## 13. Recovery Is Both Technical and Operational

Recovery time depends on:

- system behavior
- observability
- permissions/access
- runbooks
- ownership
- decision speed
- validation procedures

Reliability is therefore a socio-technical property.

## 14. Capacity Headroom Supports Recovery

Failover, rescheduling, traffic spikes, retries, and maintenance may all consume extra capacity.

A system with no headroom may be unable to recover even when redundancy exists.

## 15. Production Readiness Should Be Evidence-Based

Before launch, confidence should come from defined targets, known dependencies/failure modes, observability, tested recovery paths, capacity understanding, and ownership.

---

# Evidence Decision

The following D00-T012 areas are now eligible for **DOC-VERIFIED** status:

- reliability vs availability
- user-centered / flow-centered reliability
- resilience and recoverability
- failure-model thinking
- redundancy and independence
- graceful degradation
- failover/recovery thinking
- SLI/SLO/SLA mental models
- error-budget mental model
- reliability-vs-cost trade-offs
- end-to-end dependency reliability
- observability and alert quality
- change risk
- recovery timing
- RTO/RPO
- backup vs tested recovery
- incident readiness
- capacity/failover readiness
- production readiness

The following remain intentionally preview-level pending later domains:

- formal SLO mathematics
- burn rates
- error-budget policy automation
- multi-region DR implementation
- chaos engineering execution
- incident command systems
- quantitative capacity engineering
- detailed MTBF/MTTF statistical interpretation
- platform-specific failover design

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured exercises:

- map a critical user journey
- classify availability vs durability vs resilience failures
- map failure domains and blast radius
- compare redundant but correlated designs
- design graceful degradation
- evaluate failover assumptions
- define simple SLI/SLO examples
- model error budget conceptually
- model capacity headroom during failure
- distinguish backup from proven recovery
- build a detection-to-recovery timeline
- evaluate production readiness

These become the D00-T012 practical package.

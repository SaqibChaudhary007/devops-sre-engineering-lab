# D00-T005 — Applied Infrastructure Scenario

## Scenario

A production web application runs like this:

~~~text
Users
  ↓
Load Balancer
  ↓
┌───────────────┬───────────────┐
│ VM App A      │ VM App B      │
└───────────────┴───────────────┘
          ↓
     Shared Database
          ↓
     Remote Storage
~~~

Observed behavior during an incident:

~~~text
App CPU:                  35–45%
App memory:               normal
User latency:             high
Database latency:         elevated
One physical host:        reported unhealthy
App A and App B:          both became unavailable at the same time
Storage latency:          elevated
Network errors:           intermittent
Traffic:                  normal
Recent change:            VM placement changed during maintenance
~~~

The operations team initially says:

> "CPU is normal, so infrastructure is healthy."

## Task 1 — Challenge the Assumption

Explain why normal application CPU does not prove infrastructure health.

Consider:

- host failure
- storage latency
- network errors
- shared dependencies
- guest-visible vs physical infrastructure

## Task 2 — Failure-Domain Reasoning

Both VMs disappeared when one physical host failed.

What does this suggest about their placement?

Explain:

- why two VMs may not provide meaningful redundancy
- what physical dependency may have been shared
- what evidence you would request before claiming host-level or zone-level resilience

## Task 3 — Request / Dependency Path

Draw the infrastructure path:

~~~text
User
→ Load Balancer
→ VM
→ Guest OS
→ Virtual Resources
→ Hypervisor / Host
→ Network / Storage Dependencies
→ Database
~~~

For each layer, write one possible failure and one piece of evidence.

## Task 4 — Storage Reasoning

Storage latency is elevated.

Answer:

1. What symptoms could remote/shared storage latency cause?
2. Why does seeing a block device inside the guest not prove physical-local storage?
3. What evidence would you need to understand storage persistence and dependency?
4. How could shared storage become a common failure point?

## Task 5 — Capacity and Headroom

After App A and App B are restored, traffic is split across two VMs.

Assume each normally operates at about 45% of its effective application capacity.

If one VM becomes unavailable:

1. What approximate demand may remain for the surviving VM?
2. Why is CPU alone insufficient for deciding whether failover will succeed?
3. Which other resources/dependencies need headroom?

## Task 6 — Senior Engineer Response

Write an investigation sequence using:

~~~text
Impact
→ Guest Evidence
→ Virtualization / Placement
→ Network Path
→ Storage Path
→ Shared Dependencies
→ Failure Domain
→ Capacity / Headroom
→ Safe Mitigation
→ Root Cause
→ Prevention
~~~

## Task 7 — SRE View

Answer:

1. Which infrastructure signals affect user-facing SLOs?
2. How can host failure propagate to multiple workloads?
3. What would indicate saturation even if CPU is low?
4. How should failover capacity be validated?
5. What should be monitored at compute, storage, and network layers?

## Task 8 — Architect View

The business requires higher availability next year.

Evaluate the design in terms of:

- host placement
- rack/zone separation
- storage dependency
- database redundancy
- network path
- load-balancer design
- failover capacity
- mutable vs immutable replacement
- IaC
- cost
- operational complexity

Do not answer with "add more servers" without proving that the added resources are in independent failure domains.

## Task 9 — IaC and Change Control

The maintenance team moved VMs manually.

Explain how a versioned infrastructure definition and review process could improve:

- traceability
- repeatability
- rollback/recovery planning
- placement intent
- auditability

Also explain why IaC would not, by itself, guarantee a correct design.

## Success Standard

A strong answer identifies shared failure domains, storage/network dependencies, and headroom as separate concerns. It rejects CPU-only diagnosis, distinguishes observed evidence from assumptions, and proposes resilience improvements based on real failure-domain separation rather than raw instance count.

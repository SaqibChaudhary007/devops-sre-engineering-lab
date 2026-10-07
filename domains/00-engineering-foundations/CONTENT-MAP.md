# D00 Content Mapping

GitHub is the permanent knowledge base. Public content is the distribution and teach-back layer.

## Priorities

- **P1 Flagship** — deep video/article/lab/scenario
- **P2 Core** — standalone content
- **P3 Supporting** — micro lesson, short, diagram or section
- **P4 Reference** — documentation/cheat sheet

## Signature Series

- How It Really Works
- Why Does It Exist
- Under the Hood
- Follow the Request
- Build-Break-Fix
- Production Room
- Think Like an SRE
- Alert to RCA
- 5 Levels
- Architecture With Saqib
- Engineering Trade-Offs
- Real DevOps Interview
- Don't Do This in Prod
- Learn in Public

## D00-T001 — How Computers Work

Priority: **P1**

Visual package:

1. [Computer System Overview](../../docs/diagrams/D00/D00-T001/DIA-D00-001-computer-system-overview.md)
2. [Memory & Storage Hierarchy](../../docs/diagrams/D00/D00-T001/DIA-D00-002-memory-hierarchy.md)
3. [Application to Hardware Flow](../../docs/diagrams/D00/D00-T001/DIA-D00-003-application-to-hardware-flow.md)
4. [Bottleneck & Queueing Mental Model](../../docs/diagrams/D00/D00-T001/DIA-D00-004-bottleneck-queueing.md)
5. [Process & Resource Relationship](../../docs/diagrams/D00/D00-T001/DIA-D00-005-process-resource-relationship.md)

## D00-T002 — Operating System Mental Model

Priority: **P1**

Visual package:

1. [Operating System Overview](../../docs/diagrams/D00/D00-T002/DIA-D00-006-operating-system-overview.md)
2. [User Space, System Calls & Kernel Boundary](../../docs/diagrams/D00/D00-T002/DIA-D00-007-user-kernel-boundary.md)
3. [Process States & CPU Scheduling](../../docs/diagrams/D00/D00-T002/DIA-D00-008-process-states-scheduling.md)
4. [Application I/O Through the Kernel](../../docs/diagrams/D00/D00-T002/DIA-D00-009-application-io-kernel-flow.md)
5. [Virtual Machine vs Container OS Model](../../docs/diagrams/D00/D00-T002/DIA-D00-010-vm-vs-container.md)

These diagrams can later be reused in deep videos, Shorts, LinkedIn carousels, articles, practical explanations and teach-back material.


## D00-T003 — Software Engineering Foundations

Priority: **P1**

Visual package:

1. [Source to Process Lifecycle](../../docs/diagrams/D00/D00-T003/DIA-D00-011-source-to-process-lifecycle.md)
2. [Compiler vs Runtime-Driven Execution](../../docs/diagrams/D00/D00-T003/DIA-D00-012-compiler-vs-runtime.md)
3. [Dependency Graph](../../docs/diagrams/D00/D00-T003/DIA-D00-013-dependency-graph.md)
4. [Build-Time vs Runtime Dependencies](../../docs/diagrams/D00/D00-T003/DIA-D00-014-buildtime-vs-runtime-dependencies.md)
5. [Build Once, Promote the Artifact](../../docs/diagrams/D00/D00-T003/DIA-D00-015-build-once-promote.md)
6. [Build vs Startup vs Runtime Failure](../../docs/diagrams/D00/D00-T003/DIA-D00-016-failure-stage-model.md)

Recommended content angles:

- **How It Really Works:** Source Code to Production Process
- **Under the Hood:** Compiler vs Runtime
- **Build-Break-Fix:** Missing Configuration After a Green CI Build
- **5 Levels:** Explain an Artifact from Beginner to Architect
- **Production Room:** CI Passed but Production Failed


## D00-T004 — Application Architecture Fundamentals

Priority: **P1**

Visual package:

1. [Client → Server → Data](../../docs/diagrams/D00/D00-T004/DIA-D00-017-client-server-data.md)
2. [Three-Tier Architecture](../../docs/diagrams/D00/D00-T004/DIA-D00-018-three-tier-architecture.md)
3. [Monolith vs Microservices](../../docs/diagrams/D00/D00-T004/DIA-D00-019-monolith-vs-microservices.md)
4. [Synchronous vs Asynchronous Communication](../../docs/diagrams/D00/D00-T004/DIA-D00-020-sync-vs-async.md)
5. [Stateful vs Stateless Scaling](../../docs/diagrams/D00/D00-T004/DIA-D00-021-stateful-vs-stateless.md)
6. [Request Path & Failure Propagation](../../docs/diagrams/D00/D00-T004/DIA-D00-022-request-path-failure-propagation.md)

Recommended content angles:

- **Follow the Request:** Trace a User Request Through the Architecture
- **Architecture With Saqib:** Monolith vs Microservices Without Hype
- **Think Like an SRE:** Why a Healthy App Can Still Be Slow
- **Build-Break-Fix:** Local State Breaks Horizontal Scaling
- **5 Levels:** Explain Stateless Architecture from Beginner to Architect


## D00-T005 — Infrastructure Foundations

Priority: **P1**

Visual package:

1. [Physical Server Resource Model](../../docs/diagrams/D00/D00-T005/DIA-D00-023-physical-server-resource-model.md)
2. [Bare Metal vs Virtual Machine](../../docs/diagrams/D00/D00-T005/DIA-D00-024-bare-metal-vs-virtual-machine.md)
3. [Local vs Shared Storage](../../docs/diagrams/D00/D00-T005/DIA-D00-025-local-vs-shared-storage.md)
4. [Network Path: Client → Load Balancer → Compute](../../docs/diagrams/D00/D00-T005/DIA-D00-026-network-path-client-loadbalancer-compute.md)
5. [Failure Domains: Host → Rack → Zone → Region](../../docs/diagrams/D00/D00-T005/DIA-D00-027-failure-domains.md)
6. [Capacity, Headroom & Failover](../../docs/diagrams/D00/D00-T005/DIA-D00-028-capacity-headroom-failover.md)

Recommended content angles:

- **How It Really Works:** What Infrastructure Actually Means
- **Under the Hood:** Physical Host vs Virtual Machine
- **Follow the Request:** DNS → Load Balancer → Compute → Dependency
- **Think Like an SRE:** Why Two VMs May Still Share One Failure Domain
- **5 Levels:** Explain Capacity and Headroom from Beginner to Architect


## D00-T006 — Cloud Mental Models

Priority: **P1**

Visual package:

1. [Traditional Infrastructure vs Cloud Control Plane](../../docs/diagrams/D00/D00-T006/DIA-D00-029-traditional-vs-cloud-control-plane.md)
2. [Control Plane vs Data Plane](../../docs/diagrams/D00/D00-T006/DIA-D00-030-control-plane-vs-data-plane.md)
3. [IaaS vs PaaS vs SaaS Responsibility Stack](../../docs/diagrams/D00/D00-T006/DIA-D00-031-service-model-responsibility-stack.md)
4. [Region / Zone / Resource Failure Domains](../../docs/diagrams/D00/D00-T006/DIA-D00-032-region-zone-failure-domains.md)
5. [Elasticity & Autoscaling Loop](../../docs/diagrams/D00/D00-T006/DIA-D00-033-elasticity-autoscaling-loop.md)
6. [Cloud Responsibility / Cost / Governance Triangle](../../docs/diagrams/D00/D00-T006/DIA-D00-034-responsibility-cost-governance.md)

Recommended content angles:

- **How It Really Works:** Cloud Is More Than Someone Else's Server
- **Under the Hood:** Control Plane vs Data Plane During an Incident
- **Think Like an SRE:** Why Autoscaling Can Still Fail
- **Architecture With Saqib:** IaaS vs PaaS vs SaaS Responsibility Boundaries
- **5 Levels:** Explain Cloud Failure Domains from Beginner to Architect


## D00-T007 — DevOps Foundations

Priority: **P1**

Visual package:

1. [Traditional Siloed Delivery vs DevOps Flow](../../docs/diagrams/D00/D00-T007/DIA-D00-035-siloed-vs-devops-flow.md)
2. [Idea → Production → Feedback Loop](../../docs/diagrams/D00/D00-T007/DIA-D00-036-idea-production-feedback-loop.md)
3. [Queue / Handoff / Bottleneck Model](../../docs/diagrams/D00/D00-T007/DIA-D00-037-queue-handoff-bottleneck.md)
4. [CI vs Continuous Delivery vs Continuous Deployment](../../docs/diagrams/D00/D00-T007/DIA-D00-038-ci-cd-continuous-deployment.md)
5. [Delivery Performance: Throughput, Instability & Recovery](../../docs/diagrams/D00/D00-T007/DIA-D00-039-delivery-performance-metrics.md)
6. [DevOps vs SRE vs Platform Engineering](../../docs/diagrams/D00/D00-T007/DIA-D00-040-devops-sre-platform-engineering.md)

Recommended content angles:

- **Why Does It Exist:** Why DevOps Is Not a Tool or Team
- **How It Really Works:** Idea → Production → Feedback
- **Production Room:** Why Work Waits More Than It Works
- **Think Like an SRE:** Delivery Metrics Without Gaming Them
- **Architecture With Saqib:** DevOps vs SRE vs Platform Engineering
- **5 Levels:** Explain CI/CD from Beginner to Architect


## D00-T008 — Infrastructure as Code Mental Model

Priority: **P1**

Visual package:

1. [Manual Infrastructure vs Infrastructure as Code](../../docs/diagrams/D00/D00-T008/DIA-D00-041-manual-vs-infrastructure-as-code.md)
2. [Desired State vs Actual State](../../docs/diagrams/D00/D00-T008/DIA-D00-042-desired-vs-actual-state.md)
3. [Declarative vs Imperative](../../docs/diagrams/D00/D00-T008/DIA-D00-043-declarative-vs-imperative.md)
4. [Plan → Apply → Infrastructure Lifecycle](../../docs/diagrams/D00/D00-T008/DIA-D00-044-plan-apply-lifecycle.md)
5. [IaC State / Dependency / Locking Model](../../docs/diagrams/D00/D00-T008/DIA-D00-045-state-dependency-locking.md)
6. [IaC Change Risk: Review → Blast Radius → Recovery](../../docs/diagrams/D00/D00-T008/DIA-D00-046-review-blast-radius-recovery.md)

Recommended content angles:

- **Why Does It Exist:** Why Infrastructure as Code Is More Than Terraform
- **How It Really Works:** Desired State → Plan → Apply → Reality
- **Under the Hood:** Why State and Dependency Graphs Matter
- **Production Room:** The Plan Was Clean, but Production Still Failed
- **Architecture With Saqib:** How State Boundaries Control Blast Radius
- **5 Levels:** Explain IaC from Beginner to Architect


## D00-T009 — CI/CD Mental Model

Priority: **P1**

Visual package:

1. [CI vs Continuous Delivery vs Continuous Deployment](../../docs/diagrams/D00/D00-T009/DIA-D00-047-ci-vs-continuous-delivery-vs-deployment.md)
2. [Source → Build → Validate → Artifact → Promote → Deploy](../../docs/diagrams/D00/D00-T009/DIA-D00-048-source-build-validate-artifact-promote-deploy.md)
3. [Build Once / Promote Same Artifact](../../docs/diagrams/D00/D00-T009/DIA-D00-049-build-once-promote-same-artifact.md)
4. [Pipeline Feedback & Failure Loop](../../docs/diagrams/D00/D00-T009/DIA-D00-050-pipeline-feedback-failure-loop.md)
5. [Deployment vs Release](../../docs/diagrams/D00/D00-T009/DIA-D00-051-deployment-vs-release.md)
6. [CI/CD + IaC + GitOps Relationship](../../docs/diagrams/D00/D00-T009/DIA-D00-052-cicd-iac-gitops-relationship.md)

Recommended content angles:

- **Why Does It Exist:** CI/CD Is Not Jenkins or YAML
- **How It Really Works:** Commit → Artifact → Production → Feedback
- **Under the Hood:** Why Build Once / Promote Same Artifact Matters
- **Production Room:** Why "Retry Until Green" Hides Delivery Problems
- **Think Like an SRE:** A Successful Deploy Is Not a Healthy Service
- **Architecture With Saqib:** CI/CD + IaC + GitOps Without Confusing the Boundaries
- **5 Levels:** Explain CI/CD from Beginner to Architect


## D00-T010 — Containers & Orchestration Mental Model

Priority: **P1**

Visual package:

1. [Virtual Machine vs Container](../../docs/diagrams/D00/D00-T010/DIA-D00-053-vm-vs-container.md)
2. [Image → Container → Runtime → Host](../../docs/diagrams/D00/D00-T010/DIA-D00-054-image-container-runtime-host.md)
3. [Image Layers + Writable Container Layer](../../docs/diagrams/D00/D00-T010/DIA-D00-055-image-layers-writable-layer.md)
4. [Desired Replicas → Scheduler → Nodes → Reconciliation](../../docs/diagrams/D00/D00-T010/DIA-D00-056-replicas-scheduler-nodes-reconciliation.md)
5. [Service Discovery + Load Balancing Across Replicas](../../docs/diagrams/D00/D00-T010/DIA-D00-057-service-discovery-load-balancing.md)
6. [Container Failure vs Node Failure vs Orchestrator Recovery](../../docs/diagrams/D00/D00-T010/DIA-D00-058-container-node-orchestrator-recovery.md)

Recommended content angles:

- **Why Does It Exist:** Why Containers Are Not Lightweight VMs
- **How It Really Works:** Image → Runtime → Container → Host
- **Under the Hood:** Image Layers, Writable State, and Persistence
- **Production Room:** Restarting Is Not the Same as Recovering
- **Think Like an SRE:** Replica Count Does Not Guarantee Availability
- **Architecture With Saqib:** Desired State, Scheduling, and Bounded Self-Healing
- **5 Levels:** Explain Containers & Orchestration from Beginner to Architect


## D00-T011 — Distributed Systems Foundations

Priority: **P1**

Visual package:

1. [Local Call vs Network Call](../../docs/diagrams/D00/D00-T011/DIA-D00-059-local-call-vs-network-call.md)
2. [Partial Failure & Ambiguous Timeout](../../docs/diagrams/D00/D00-T011/DIA-D00-060-partial-failure-ambiguous-timeout.md)
3. [Retry → Duplicate → Idempotency Key](../../docs/diagrams/D00/D00-T011/DIA-D00-061-retry-duplicate-idempotency.md)
4. [Replication → Lag → Stale Read](../../docs/diagrams/D00/D00-T011/DIA-D00-062-replication-lag-stale-read.md)
5. [Partition Trade-Off / CAP Mental Model](../../docs/diagrams/D00/D00-T011/DIA-D00-063-partition-cap-mental-model.md)
6. [Timeout + Retry + Backoff + Circuit Breaker Failure Loop](../../docs/diagrams/D00/D00-T011/DIA-D00-064-timeout-retry-backoff-circuit-breaker.md)

Recommended content angles:

- **Why Does It Exist:** Why Distributed Systems Are Harder Than "Many Servers"
- **How It Really Works:** Network Call → Timeout → Uncertainty → Recovery Decision
- **Under the Hood:** Retry, Duplicate Effects, and Idempotency
- **Production Room:** The Request Timed Out, but the Payment Still Happened
- **Think Like an SRE:** How Retries Turn a Slow Dependency into an Outage
- **Architecture With Saqib:** CAP Without the "Choose Two" Myth
- **5 Levels:** Explain Distributed Systems from Beginner to Architect


## D00-T012 — Reliability Engineering Foundations

Priority: **P1**

Visual package:

1. [Reliability vs Availability vs Durability vs Resilience](../../docs/diagrams/D00/D00-T012/DIA-D00-065-reliability-availability-durability-resilience.md)
2. [User Journey → Dependency Chain → Reliability Outcome](../../docs/diagrams/D00/D00-T012/DIA-D00-066-user-journey-dependency-reliability.md)
3. [Failure Domain → Blast Radius → Redundancy Placement](../../docs/diagrams/D00/D00-T012/DIA-D00-067-failure-domain-blast-radius-redundancy.md)
4. [Detect → Contain → Recover → Validate → Learn](../../docs/diagrams/D00/D00-T012/DIA-D00-068-detect-contain-recover-validate-learn.md)
5. [SLI → SLO → Error Budget Mental Model](../../docs/diagrams/D00/D00-T012/DIA-D00-069-sli-slo-error-budget.md)
6. [Capacity Headroom → Failure → Failover / Degradation](../../docs/diagrams/D00/D00-T012/DIA-D00-070-capacity-headroom-failure-recovery.md)

Recommended content angles:

- **Why Does It Exist:** Reliability Is More Than Uptime
- **How It Really Works:** User Journey → Failure → Detection → Recovery
- **Under the Hood:** Redundancy, Failure Domains, and Blast Radius
- **Production Room:** Why Backup Does Not Mean Recovery
- **Think Like an SRE:** SLI → SLO → Error Budget
- **Architecture With Saqib:** How Much Reliability Is Enough?
- **5 Levels:** Explain Reliability Engineering from Beginner to Architect


## D00-T013 — SRE Foundations

Priority: **P1**

Visual package:

1. [User Journey → SLI → SLO → Error Budget → Decision](../../docs/diagrams/D00/D00-T013/DIA-D00-071-user-journey-sli-slo-error-budget-decision.md)
2. [Page vs Ticket vs Dashboard](../../docs/diagrams/D00/D00-T013/DIA-D00-072-page-ticket-dashboard.md)
3. [Incident: Detect → Mitigate → Recover → Learn](../../docs/diagrams/D00/D00-T013/DIA-D00-073-incident-detect-mitigate-recover-learn.md)
4. [Toil → Automation → Engineering Capacity](../../docs/diagrams/D00/D00-T013/DIA-D00-074-toil-automation-engineering-capacity.md)
5. [Error Budget → Change Velocity / Reliability Trade-Off](../../docs/diagrams/D00/D00-T013/DIA-D00-075-error-budget-change-velocity-reliability.md)
6. [Production Readiness → Operate → Incident → Improvement](../../docs/diagrams/D00/D00-T013/DIA-D00-076-production-readiness-operate-improve.md)

Recommended content angles:

- **Why Does It Exist:** SRE Is More Than Monitoring and On-Call
- **How It Really Works:** User Journey → SLI → SLO → Error Budget → Decision
- **Under the Hood:** Toil, Automation, and Sustainable Engineering Capacity
- **Production Room:** Mitigate First, Then Learn Deeply
- **Think Like an SRE:** Which Signals Should Page a Human?
- **Architecture With Saqib:** Safe Velocity Through Error Budgets and Readiness Gates
- **5 Levels:** Explain SRE from Beginner to Architect


## D00-T014 — Observability Foundations

Priority: **P1**

Visual package:

1. [System → Instrumentation → Telemetry → Correlation → Insight](../../docs/diagrams/D00/D00-T014/DIA-D00-077-system-instrumentation-telemetry-correlation-insight.md)
2. [Metrics vs Logs vs Traces vs Events](../../docs/diagrams/D00/D00-T014/DIA-D00-078-metrics-logs-traces-events.md)
3. [User Journey → Trace → Spans → Logs / Metrics](../../docs/diagrams/D00/D00-T014/DIA-D00-079-user-journey-trace-spans-logs-metrics.md)
4. [RED vs USE vs Golden Signals](../../docs/diagrams/D00/D00-T014/DIA-D00-080-red-use-golden-signals.md)
5. [Change Marker → Symptom → Dependency → Root-Cause Hypothesis](../../docs/diagrams/D00/D00-T014/DIA-D00-081-change-symptom-dependency-hypothesis.md)
6. [Cardinality / Sampling / Retention / Cost Trade-Off](../../docs/diagrams/D00/D00-T014/DIA-D00-082-cardinality-sampling-retention-cost.md)

Recommended content angles:

- **Why Does It Exist:** Observability Is More Than Dashboards
- **How It Really Works:** Instrumentation → Telemetry → Correlation → Insight
- **Follow the Request:** Trace One Checkout Across Services
- **Under the Hood:** Cardinality, Sampling, Retention, and Cost
- **Production Room:** Correlation Is Not Causation
- **Think Like an SRE:** Start with User Impact, Not Random Commands
- **Architecture With Saqib:** Designing an Observability Platform That Does Not Drown in Noise
- **5 Levels:** Explain Observability from Beginner to Architect


## D00-T015 — Security Foundations

Priority: **P1**

Visual package:

1. [Asset → Threat → Vulnerability → Risk → Control](../../docs/diagrams/D00/D00-T015/DIA-D00-083-asset-threat-vulnerability-risk-control.md)
2. [Identity → Authentication → Authorization → Least Privilege → Audit](../../docs/diagrams/D00/D00-T015/DIA-D00-084-identity-authn-authz-least-privilege-audit.md)
3. [Trust Boundary → Control → Detection → Response](../../docs/diagrams/D00/D00-T015/DIA-D00-085-trust-boundary-control-detection-response.md)
4. [Secret Lifecycle: Create → Store → Distribute → Use → Rotate → Revoke](../../docs/diagrams/D00/D00-T015/DIA-D00-086-secret-lifecycle.md)
5. [Source → Build → Artifact → Registry → Deployment → Runtime Trust Chain](../../docs/diagrams/D00/D00-T015/DIA-D00-087-software-supply-chain-trust.md)
6. [Defense in Depth → Blast Radius Reduction](../../docs/diagrams/D00/D00-T015/DIA-D00-088-defense-in-depth-blast-radius.md)

Recommended content angles:

- **Why Does It Exist:** Security Is Risk Management, Not a Firewall
- **How It Really Works:** Identity → Authentication → Authorization → Least Privilege
- **Under the Hood:** The Secret Lifecycle Nobody Should Skip
- **Production Room:** What Happens When One Credential Has Too Much Reach?
- **Think Like an SRE:** Security Controls That Can Hurt Reliability
- **Architecture With Saqib:** Trust Boundaries, Supply Chain, and Blast Radius
- **5 Levels:** Explain Security from Beginner to Architect


## D00-T016 — Automation Mental Models

Priority: **P1**

Visual package:

1. [Trigger → Preconditions → State → Action → Validation → Feedback](../../docs/diagrams/D00/D00-T016/DIA-D00-089-trigger-preconditions-state-action-validation-feedback.md)
2. [Current State ↔ Desired State → Reconciliation Loop](../../docs/diagrams/D00/D00-T016/DIA-D00-090-current-desired-reconciliation-loop.md)
3. [Idempotency / Duplicate Execution / Retry Safety](../../docs/diagrams/D00/D00-T016/DIA-D00-091-idempotency-duplicate-retry-safety.md)
4. [Partial Failure → Rollback / Roll-Forward / Compensation](../../docs/diagrams/D00/D00-T016/DIA-D00-092-partial-failure-recovery-options.md)
5. [Human Approval → Guardrails → Automated Action → Validation](../../docs/diagrams/D00/D00-T016/DIA-D00-093-human-approval-guardrails-action-validation.md)
6. [Automation Blast Radius: Scope / Rate / Identity / Environment / Stop Conditions](../../docs/diagrams/D00/D00-T016/DIA-D00-094-automation-blast-radius-guardrails.md)

Recommended content angles:

- **Why Does It Exist:** Automation Is More Than Scripting
- **How It Really Works:** Trigger → State → Action → Validation
- **Under the Hood:** Idempotency, Duplicate Execution, and Retry Safety
- **Build Break Fix:** What Happens When Automation Runs Twice?
- **Production Room:** Why Rollback Is Not Always Possible
- **Think Like an SRE:** Bound Self-Healing Before It Amplifies Failure
- **Architecture With Saqib:** Designing Maximum Safe Automation Blast Radius
- **5 Levels:** Explain Automation from Beginner to Architect


## D00-T017 — Systems Thinking

Priority: **P1**

Visual package:

1. [System Boundary → Components → Relationships → Flows → Outcome](../../docs/diagrams/D00/D00-T017/DIA-D00-095-system-boundary-components-flows-outcome.md)
2. [Stock / Flow / Queue Accumulation](../../docs/diagrams/D00/D00-T017/DIA-D00-096-stock-flow-queue-accumulation.md)
3. [Reinforcing vs Balancing Feedback Loops](../../docs/diagrams/D00/D00-T017/DIA-D00-097-reinforcing-vs-balancing-feedback.md)
4. [Local Optimization vs Global Outcome](../../docs/diagrams/D00/D00-T017/DIA-D00-098-local-vs-global-optimization.md)
5. [Dependency Chain → Cascading Failure → Blast Radius](../../docs/diagrams/D00/D00-T017/DIA-D00-099-dependency-cascade-blast-radius.md)
6. [Intervention → First-Order Effect → Second-Order Effect → New System State](../../docs/diagrams/D00/D00-T017/DIA-D00-100-intervention-second-order-effects.md)

Recommended content angles:

- **Why Does It Exist:** Healthy Components Can Still Produce a Broken System
- **How It Really Works:** Boundary → Flow → Constraint → Feedback → Outcome
- **Under the Hood:** Stocks, Flows, Delays, and Feedback Loops
- **Production Room:** Retry Storms as Reinforcing Feedback
- **Think Like an SRE:** Find the System Bottleneck, Not the Loudest Metric
- **Architecture With Saqib:** Hidden Coupling, Shared Failure Domains, and Second-Order Effects
- **5 Levels:** Explain Systems Thinking from Beginner to Architect

## Rule

Research once, verify it, build the canonical topic, then repurpose it into the right formats without duplicating technical truth across multiple places.

# D00-T010 — Applied Orchestration Scenario

## Scenario

A customer-facing API is deployed as a containerized workload.

Current design:

~~~text
Desired replicas = 4
Nodes = 3
Stable service endpoint = customer-api
Persistent dependency = managed database
Image = customer-api:latest
~~~

Initial placement:

~~~text
Node A
- Replica 1
- Replica 2

Node B
- Replica 3

Node C
- Replica 4
~~~

Current problems:

~~~text
- all replicas use image tag customer-api:latest
- the exact digest is not recorded
- customer uploads are written to the container writable layer
- readiness and liveness use the same endpoint
- one replica repeatedly crashes and restarts
- Node A becomes unavailable
- cluster spare capacity is limited
- a replacement workload remains unscheduled
- the database is reachable from some nodes but not others
- production logs live only inside the containers
- a rolling update to v2 starts, but new replicas fail readiness
- the team says "Kubernetes will self-heal everything"
~~~

## Task 1 — Layer the System

Map:

~~~text
Image
→ Container
→ Runtime
→ Node / Host
→ Orchestrator
→ Service
→ Dependency
~~~

For each layer, identify one possible failure mode.

## Task 2 — Image Identity

Explain why:

~~~text
customer-api:latest
~~~

is weak production evidence.

Define a stronger traceability model using:

~~~text
Commit
→ Build
→ Image Digest
→ Deployment
→ Running Replica
~~~

## Task 3 — Data Durability

Customer uploads are stored in the writable container layer.

Explain:

- what can happen when a container is replaced
- why the design is unsafe
- where durable uploads should live conceptually
- how workload lifecycle and storage lifecycle should be separated

## Task 4 — Health Design

The same endpoint is used for readiness and liveness.

Explain why this can be dangerous.

Design separate questions for:

- startup
- liveness
- readiness
- service/SLO health

## Task 5 — Restart Loop

Replica 3 repeatedly crashes and restarts.

Use:

~~~text
Impact
→ Container Status
→ Exit / Crash Evidence
→ Configuration
→ Dependency Health
→ Host Conditions
→ Change History
→ Root Cause
~~~

Explain why restart is not enough.

## Task 6 — Node Failure

Node A fails and two replicas disappear.

Analyze:

- observed replicas
- blast radius
- service capacity
- replacement demand
- remaining node capacity
- expected orchestrator behavior

## Task 7 — Unschedulable Replacement

One replacement stays pending because no suitable node has enough resources.

Explain:

- why reconciliation can still be working correctly
- why desired state is not reached
- what evidence to inspect
- why "self-healing" depends on capacity

## Task 8 — Service Discovery

Explain why clients should use:

~~~text
Stable Service
→ Healthy/Ready Replica Set
~~~

instead of individual replica addresses.

## Task 9 — Partial Network Failure

The database is reachable from Node B but not Node C.

Explain why:

- a replica may be alive
- readiness may fail
- service capacity may shrink
- the problem may be network/path-specific rather than application-code-specific

## Task 10 — Rolling Update

Version v2 replicas start but fail readiness.

Explain:

- what should happen to traffic
- why rollout should slow/stop
- what evidence to inspect
- why liveness alone is insufficient

## Task 11 — Stateful Variant

Assume each replica now has unique persistent identity and storage.

Explain why:

> "Just reschedule it anywhere"

is incomplete.

Discuss:

- storage attachment
- identity
- ordering
- consistency
- recovery time

## Task 12 — Observability

Logs exist only inside each container.

Explain why this is weak for ephemeral workloads.

Design an evidence model using:

- centralized logs
- metrics
- orchestration events
- image/version identity
- node data
- deployment/change markers

## Task 13 — Security

The workload runs with unnecessary root privileges and mounts a broad host path.

Explain the risk at a high level.

Recommend principles:

- least privilege
- minimal host access
- trusted image identity
- controlled secrets
- restricted network access

## Task 14 — Senior Engineer Response

Use:

~~~text
Impact
→ Image Identity
→ Container Status
→ Host / Node
→ Desired vs Observed State
→ Scheduler / Capacity
→ Health
→ Service Discovery
→ Storage / Dependencies
→ Recovery
~~~

## Task 15 — SRE View

Connect the incident to:

- availability
- error rate
- latency
- saturation
- replica health
- rescheduling time
- SLO impact
- blast radius

## Task 16 — Architect View

Design a safer target model covering:

- image identity
- workload placement
- replica spread
- spare capacity
- health separation
- persistent storage
- service discovery
- observability
- stateful recovery
- security boundaries
- CI/CD + IaC + orchestration ownership

## Success Standard

A strong answer separates runtime layers and avoids magical thinking about orchestration.

It should identify:

- weak image identity
- ephemeral-data risk
- health-probe design problems
- restart-loop evidence
- node-level blast radius
- unschedulable-capacity limits
- network/path dependency failure
- rolling-update readiness failure
- stateful recovery complexity
- missing centralized observability
- bounded self-healing

# D00-T010 Assessment Package — Containers & Orchestration Mental Model

This package evaluates whether the learner can reason about containers and orchestration as layered runtime and control-system concepts rather than as Docker/Kubernetes commands.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Orchestration Scenario](applied-scenario.md)
3. [Senior / SRE / Architect Follow-Ups](interview-followups.md)
4. [Teach-Back Assessment](teach-back.md)
5. [Rubric & Remediation Guide](rubric.md)

## Recommended Order

Knowledge Check
→ Applied Scenario
→ Follow-Ups
→ Teach-Back
→ Rubric Review

## Topic Competency Guidance

Recommended minimum:

- Knowledge Check: 80%
- Applied Scenario: 75%
- Follow-Up Depth: FD-3
- Reasoning Level: at least L3
- Teach-Back: 4/5 average
- No critical misconception around image/container/runtime/host boundaries, persistence, probes, reconciliation, scheduling, replica availability, stateful recovery, self-healing limits, or Kubernetes/runtime separation

## Critical Misconceptions

A learner should not leave this topic believing that:

- a container is a lightweight virtual machine
- an image is the same thing as a running container
- container-local writable data is automatically durable
- restart equals root-cause recovery
- startup, liveness, and readiness are interchangeable
- replica count alone guarantees availability
- an orchestrator creates capacity automatically
- service instances have permanent addresses
- stateful workloads can be treated like stateless replicas
- Kubernetes is the container runtime
- orchestration removes host/network/storage failures
- self-healing means every failure is automatically repaired

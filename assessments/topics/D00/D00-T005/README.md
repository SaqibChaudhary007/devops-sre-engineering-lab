# D00-T005 Assessment Package — Infrastructure Foundations

This package evaluates whether the learner can reason about physical and virtual infrastructure, compute, memory, storage, networking, failure domains, capacity, redundancy, high availability, infrastructure change, and operational trade-offs.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Infrastructure Scenario](applied-scenario.md)
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
- No critical misconception about virtualization, storage persistence, failure domains, high availability, utilization, saturation, or IaC

## Critical Misconceptions

A learner should not leave this topic believing that:

- a VM is a physical machine
- one vCPU always equals one dedicated physical core
- two servers automatically mean high availability
- low CPU means infrastructure is healthy
- a block device visible in a guest proves physically local storage
- all cloud zones/regions have identical semantics
- redundancy is the same thing as high availability
- infrastructure as code automatically makes infrastructure correct
- cloud eliminates infrastructure failures

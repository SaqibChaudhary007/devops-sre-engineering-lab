---
id: DIA-D00-040
domain: D00
topic: D00-T007
title: DevOps vs SRE vs Platform Engineering
type: relationship-diagram
status: published
---

# DIA-D00-040 — DevOps vs SRE vs Platform Engineering

## Purpose

Show overlap without treating DevOps, SRE, and platform engineering as synonyms.

~~~mermaid
flowchart TB
    DEVOPS[DevOps<br/>Flow • Feedback • Shared Ownership • Automation]

    DEVOPS --> SRE[SRE<br/>Reliability Engineering • SLOs • Toil • Recovery]
    DEVOPS --> PLATFORM[Platform Engineering<br/>Internal Products • Self-Service • Paved Roads]

    SRE --> OUTCOME[Reliable Delivery Outcomes]
    PLATFORM --> OUTCOME
~~~

## DevOps

Broad operating principles around:

- flow
- feedback
- collaboration
- automation
- shared outcomes

## SRE

A reliability-focused engineering discipline that can implement many DevOps principles.

## Platform Engineering

Builds reusable internal platform capabilities that can make good delivery practices easier and reduce cognitive load.

## Important Boundaries

~~~text
DevOps ≠ SRE
DevOps ≠ Platform Engineering
SRE ≠ Platform Engineering
~~~

They can reinforce one another.

## Architect Connection

The right organizational model depends on team size, system criticality, reliability requirements, platform maturity, and operational capability.

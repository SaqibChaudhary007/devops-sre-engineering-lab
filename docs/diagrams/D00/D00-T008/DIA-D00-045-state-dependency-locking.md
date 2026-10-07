---
id: DIA-D00-045
domain: D00
topic: D00-T008
title: IaC State Dependency Locking Model
type: architecture-diagram
status: published
---

# DIA-D00-045 — IaC State / Dependency / Locking Model

## Purpose

Show how some IaC systems connect configuration, resource identity, dependencies, and concurrency control.

~~~mermaid
flowchart TB
    CODE[Infrastructure Definition] --> ENGINE[IaC Engine]
    STATE[(State / Resource Mapping)]
    ENGINE <--> STATE
    ENGINE --> API[Provider / Platform API]
    API --> INFRA[Real Infrastructure]

    A[Engineer / Pipeline A] --> LOCK{Lock Supported?}
    B[Engineer / Pipeline B] --> LOCK
    LOCK --> ENGINE
~~~

## Dependency Example

~~~text
Network
→ Subnet
→ Load Balancer
→ Application
→ Database
~~~

## Important Nuances

- explicit user-managed state is tool-specific, not universal
- remote state does not automatically mean locking
- locking depends on tool/backend capability
- locking protects concurrent mutation, not bad intent
- cross-state dependencies still require coordination

## Architect Connection

State boundaries influence ownership, access control, recovery, and blast radius.

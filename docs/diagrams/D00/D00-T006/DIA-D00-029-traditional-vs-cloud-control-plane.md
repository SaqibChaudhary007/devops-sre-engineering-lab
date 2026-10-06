---
id: DIA-D00-029
domain: D00
topic: D00-T006
title: Traditional Infrastructure vs Cloud Control Plane
type: comparison-diagram
status: published
---

# DIA-D00-029 — Traditional Infrastructure vs Cloud Control Plane

## Purpose

Show the operational shift from ticket/manual provisioning to programmable infrastructure.

## Traditional Provisioning

~~~mermaid
flowchart LR
    REQ1[Requirement] --> TICKET[Ticket / Human Process]
    TICKET --> ADMIN[Infrastructure Team]
    ADMIN --> BUILD[Provision / Configure]
    BUILD --> RESOURCE1[Infrastructure Resource]
~~~

## Cloud Provisioning

~~~mermaid
flowchart LR
    REQ2[Requirement] --> CODE[Portal / CLI / API / IaC]
    CODE --> CP[Cloud Control Plane]
    CP --> RESOURCE2[Compute / Network / Storage / Managed Service]
~~~

## Key Lesson

The biggest shift is not only where hardware lives.

It is that infrastructure and platform capabilities become programmable services.

## Risk Connection

Faster provisioning also means faster:

- misconfiguration
- overspending
- insecure exposure
- uncontrolled sprawl

Cloud speed therefore requires governance.

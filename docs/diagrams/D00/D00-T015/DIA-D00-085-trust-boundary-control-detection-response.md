---
id: DIA-D00-085
domain: D00
topic: D00-T015
title: Trust Boundary Control Detection Response
type: trust-boundary-diagram
status: published
---

# DIA-D00-085 — Trust Boundary → Control → Detection → Response

## Purpose

Show how crossing a trust boundary should trigger explicit security decisions.

~~~mermaid
flowchart LR
    ACTOR[Actor / System] --> BOUNDARY[Trust Boundary]
    BOUNDARY --> VERIFY[Verify Identity / Context]
    VERIFY --> POLICY[Authorization / Policy]
    POLICY --> CONTROL[Preventive Control]
    CONTROL --> EVIDENCE[Audit / Telemetry]
    EVIDENCE --> DETECT[Detection]
    DETECT --> RESPOND[Contain / Respond]
    RESPOND --> RECOVER[Recover / Re-establish Trust]
~~~

## Examples of Trust Boundaries

~~~text
Internet → Edge
Developer → Source Repository
CI/CD → Production
Application → Database
Cloud Account A → Cloud Account B
~~~

## Key Lesson

Zero Trust does not mean "trust nobody."

It means no implicit trust simply because an actor is inside a network or owned by the organization.

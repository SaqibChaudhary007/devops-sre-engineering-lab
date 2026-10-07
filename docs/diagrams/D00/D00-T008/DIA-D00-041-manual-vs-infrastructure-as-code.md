---
id: DIA-D00-041
domain: D00
topic: D00-T008
title: Manual Infrastructure vs Infrastructure as Code
type: comparison-diagram
status: published
---

# DIA-D00-041 — Manual Infrastructure vs Infrastructure as Code

## Purpose

Show the operational shift from one-off manual change to versioned, reviewable infrastructure change.

## Manual Model

~~~mermaid
flowchart LR
    REQ1[Requirement] --> HUMAN[Human Login / Ticket]
    HUMAN --> CHANGE1[Click / Command]
    CHANGE1 --> INFRA1[Infrastructure]
~~~

Risks may include undocumented steps, drift, weak auditability, inconsistent environments, and person-dependent knowledge.

## IaC Model

~~~mermaid
flowchart LR
    REQ2[Requirement] --> DEF[Infrastructure Definition]
    DEF --> REVIEW[Review]
    REVIEW --> VALIDATE[Validate / Preview]
    VALIDATE --> APPLY[Apply]
    APPLY --> INFRA2[Infrastructure]
    INFRA2 --> OBS[Observe]
~~~

## Key Lesson

IaC moves infrastructure change into an engineering workflow.

It improves repeatability and traceability, but does not guarantee correctness.

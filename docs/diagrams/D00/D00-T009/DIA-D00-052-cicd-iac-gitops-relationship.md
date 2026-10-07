---
id: DIA-D00-052
domain: D00
topic: D00-T009
title: CI/CD IaC GitOps Relationship
type: architecture-diagram
status: published
---

# DIA-D00-052 — CI/CD + IaC + GitOps Relationship

## Purpose

Show how software build, infrastructure change, and GitOps reconciliation can work together without treating them as synonyms.

~~~mermaid
flowchart TB
    SRC[Application Source] --> CI[CI: Build / Test]
    CI --> ART[Artifact Repository]

    IAC[IaC Definitions] --> IACPIPE[IaC Validation / Apply Path]
    IACPIPE --> PLATFORM[Infrastructure / Platform]

    ART --> DELIVERY[Delivery Workflow]
    DELIVERY --> GIT[Desired State in Git]
    GIT --> RECON[GitOps Reconciler]
    RECON --> PLATFORM
    PLATFORM --> RUNTIME[Running Application]
~~~

## Push vs Pull

~~~text
Push-style CI/CD:
Pipeline → Target Environment

GitOps:
Desired State in Git → Reconciler Pulls → Environment Converges
~~~

## Key Lesson

CI, IaC, and GitOps solve different parts of delivery.

They can be composed into one operating model, but they are not interchangeable.

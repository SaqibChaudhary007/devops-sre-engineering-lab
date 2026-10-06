---
id: DIA-D00-015
domain: D00
topic: D00-T003
title: Build Once, Promote the Artifact
type: delivery-diagram
status: published
---

# DIA-D00-015 — Build Once, Promote the Artifact

## Purpose

Explain the delivery principle of producing one versioned artifact and promoting that same artifact through environments.

~~~mermaid
flowchart TB
    COMMIT[Source Commit] --> BUILD[Build Once]
    BUILD --> ART[Artifact v2.4.1]

    ART --> DEV[Development]
    ART --> QA[QA / Test]
    ART --> STAGE[Staging]
    ART --> PROD[Production]

    CFG1[Dev Config] --> DEV
    CFG2[QA Config] --> QA
    CFG3[Stage Config] --> STAGE
    CFG4[Prod Config] --> PROD
~~~

## Core Idea

~~~text
Same Artifact
+
Environment-Specific Configuration
=
Different Environment Behavior
~~~

## Why This Helps

It improves:

- traceability
- rollback confidence
- environment consistency
- debugging
- release identity

## Important Nuance

"Build once, promote" is a delivery principle, not a universal rule for every possible platform or build model.

## SRE Connection

During an incident, being able to prove the exact artifact deployed in every environment reduces uncertainty.

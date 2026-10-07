---
id: DIA-D00-048
domain: D00
topic: D00-T009
title: Source Build Validate Artifact Promote Deploy
type: lifecycle-diagram
status: published
---

# DIA-D00-048 — Source → Build → Validate → Artifact → Promote → Deploy

## Purpose

Show the full delivery path from source revision to runtime feedback.

~~~mermaid
flowchart LR
    SRC[Source Revision] --> BUILD[Build]
    BUILD --> VALIDATE[Validate]
    VALIDATE --> ART[Artifact]
    ART --> STORE[Artifact Repository]
    STORE --> DEV[Dev]
    DEV --> STAGE[Staging]
    STAGE --> PROD[Production]
    PROD --> VERIFY[Verify]
    VERIFY --> OBS[Observe]
    OBS --> LEARN[Learn]
~~~

## Traceability Chain

~~~text
Commit SHA
→ Build ID
→ Artifact ID / Digest
→ Deployment
→ Environment
→ Runtime Outcome
~~~

## Key Lesson

CI/CD should make change traceable from source to production outcome.

---
id: DIA-D00-087
domain: D00
topic: D00-T015
title: Software Supply Chain Trust
type: supply-chain-diagram
status: published
---

# DIA-D00-087 — Source → Build → Artifact → Registry → Deployment → Runtime Trust Chain

## Purpose

Show the software-delivery path as a chain of identities, evidence, permissions, and verification decisions.

~~~mermaid
flowchart LR
    SRC[Source] --> BUILD[Build]
    BUILD --> ART[Artifact]
    ART --> REG[Registry]
    REG --> DEPLOY[Deployment]
    DEPLOY --> RUN[Runtime]

    SRC -. review / identity .-> EVID[Trust Evidence]
    BUILD -. builder / provenance .-> EVID
    ART -. digest / signature concept .-> EVID
    REG -. promotion / access .-> EVID
    DEPLOY -. policy / approval .-> EVID
    EVID --> VERIFY[Verify Against Expectations]
    VERIFY --> RUN
~~~

## Key Lesson

Provenance answers:

~~~text
Where did this artifact come from?
How was it produced?
By which build process / identity?
~~~

But provenance is evidence, not automatic trust.

Trust also depends on the source, builder, policy, integrity of the evidence, and actual verification.

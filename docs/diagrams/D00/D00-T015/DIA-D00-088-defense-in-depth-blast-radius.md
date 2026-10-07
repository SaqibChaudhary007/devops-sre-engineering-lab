---
id: DIA-D00-088
domain: D00
topic: D00-T015
title: Defense in Depth Blast Radius Reduction
type: defense-in-depth-diagram
status: published
---

# DIA-D00-088 — Defense in Depth → Blast Radius Reduction

## Purpose

Show how complementary controls limit the impact of a single failure without treating "more controls" as automatically better.

~~~mermaid
flowchart TB
    ASSET[Critical Asset / Production Service]

    ID[Identity Control] --> ASSET
    AUTHZ[Least Privilege] --> ASSET
    SEG[Segmentation / Isolation] --> ASSET
    SECRET[Secret Separation] --> ASSET
    VERIFY[Artifact / Change Verification] --> ASSET
    AUDIT[Audit / Monitoring] --> ASSET
    BACKUP[Protected Recovery Path] --> ASSET

    ASSET --> FAIL{One Control Fails}
    FAIL --> LIMIT[Other Controls Limit Reach]
    LIMIT --> SMALLER[Smaller Blast Radius]
    SMALLER --> RECOVER[Detect / Contain / Recover]
~~~

## Key Lesson

Defense in depth means complementary controls addressing meaningful failure modes.

It does not mean adding random controls that increase complexity without reducing real risk.

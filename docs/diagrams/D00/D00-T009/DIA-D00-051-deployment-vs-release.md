---
id: DIA-D00-051
domain: D00
topic: D00-T009
title: Deployment vs Release
type: concept-diagram
status: published
---

# DIA-D00-051 — Deployment vs Release

## Purpose

Show why code can be present in production without being exposed to users.

~~~mermaid
flowchart LR
    ART[Artifact] --> DEPLOY[Deploy to Production]
    DEPLOY --> FLAG{Feature Enabled?}
    FLAG -->|No| HIDDEN[Code Present, Feature Hidden]
    FLAG -->|Yes| RELEASE[Feature Released to Users]
~~~

## Key Distinction

~~~text
Deployment
→ software version is placed in an environment

Release
→ functionality becomes available to users
~~~

## Key Lesson

Deployment and release can be decoupled through feature flags or other controlled-exposure mechanisms.

This can reduce release coupling but introduces lifecycle and operational complexity.

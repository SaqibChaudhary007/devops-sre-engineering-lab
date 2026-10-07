---
id: DIA-D00-086
domain: D00
topic: D00-T015
title: Secret Lifecycle
type: secret-lifecycle-diagram
status: published
---

# DIA-D00-086 — Secret Lifecycle

## Purpose

Show that secrets management is a lifecycle problem rather than only a storage problem.

~~~mermaid
flowchart LR
    CREATE[Create] --> STORE[Store]
    STORE --> DISTRIBUTE[Distribute]
    DISTRIBUTE --> USE[Use]
    USE --> ROTATE[Rotate]
    ROTATE --> REVOKE[Revoke]
    REVOKE --> AUDIT[Audit / Review]
    AUDIT --> CREATE
~~~

## Safety Questions at Every Stage

~~~text
Who can access it?
How is access authenticated?
What is the scope?
How long is it valid?
How is use audited?
How is it rotated?
How is it revoked?
~~~

## Key Lesson

Short-lived credentials reduce exposure duration, but scope, issuance, identity, monitoring, and revocation still matter.

Secrets should not be treated as ordinary version-controlled configuration.

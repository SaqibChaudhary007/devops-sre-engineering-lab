---
id: DIA-D00-084
domain: D00
topic: D00-T015
title: Identity Authentication Authorization Least Privilege Audit
type: identity-access-diagram
status: published
---

# DIA-D00-084 — Identity → Authentication → Authorization → Least Privilege → Audit

## Purpose

Show the identity and access-control chain without collapsing authentication and authorization into the same concept.

~~~mermaid
flowchart LR
    I[Identity<br/>Human / Workload] --> AUTHN[Authentication<br/>Prove Identity]
    AUTHN --> AUTHZ[Authorization<br/>Allowed Actions]
    AUTHZ --> LP[Least Privilege<br/>Scope + Action + Duration]
    LP --> ACCESS[Access]
    ACCESS --> AUDIT[Audit Evidence]
    AUDIT --> REVIEW[Review / Revoke / Improve]
~~~

## Key Distinction

~~~text
Authentication
→ Who / what are you?

Authorization
→ What are you allowed to do?
~~~

## Key Lesson

Strong authentication does not justify broad authorization.

Least privilege should consider resource scope, permitted action, duration, and conditions.

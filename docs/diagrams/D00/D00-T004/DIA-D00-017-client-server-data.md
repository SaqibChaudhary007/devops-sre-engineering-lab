---
id: DIA-D00-017
domain: D00
topic: D00-T004
title: Client Server Data
type: architecture-diagram
status: published
---

# DIA-D00-017 — Client → Server → Data

## Purpose

Show the simplest useful application architecture and the role changes across interactions.

~~~mermaid
flowchart LR
    USER[User] --> CLIENT[Client / Browser]
    CLIENT -->|Request| APP[Application Server]
    APP -->|Query / Command| DATA[(Data Store)]
    DATA -->|Data / Result| APP
    APP -->|Response| CLIENT
~~~

## Role View

~~~text
Browser → client to application

Application → server to browser
Application → client to database

Database → server to application
~~~

## Key Lesson

Client and server are interaction roles, not permanent labels.

## Troubleshooting Connection

When a user reports failure, ask which hop failed:

~~~text
Client
→ Network
→ Application
→ Data
→ Response
~~~

## Architect Connection

Even this simple architecture already creates boundaries for latency, ownership, scaling and failure.

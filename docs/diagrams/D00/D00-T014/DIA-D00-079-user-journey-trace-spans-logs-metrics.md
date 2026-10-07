---
id: DIA-D00-079
domain: D00
topic: D00-T014
title: User Journey Trace Spans Logs Metrics
type: distributed-correlation-diagram
status: published
---

# DIA-D00-079 — User Journey → Trace → Spans → Logs / Metrics

## Purpose

Show how one user request can connect distributed trace spans to logs and service metrics.

~~~mermaid
flowchart LR
    USER[Checkout User Journey] --> TRACE[Trace ID]

    TRACE --> API[API Span]
    TRACE --> AUTH[Auth Span]
    TRACE --> ORDER[Order Span]
    TRACE --> PAY[Payment Span]
    TRACE --> DB[Database Span]

    API --> L1[Structured Logs]
    AUTH --> L2[Structured Logs]
    ORDER --> L3[Structured Logs]
    PAY --> L4[Structured Logs]
    DB --> L5[Structured Logs]

    API --> M1[Service Metrics]
    ORDER --> M2[Service Metrics]
    PAY --> M3[Dependency Metrics]
~~~

## Correlation Model

~~~text
Trace ID
→ distributed request identity

Span
→ one unit of work

Structured Logs
→ detailed event evidence

Metrics
→ aggregate behavior
~~~

## Key Lesson

Request IDs, workflow/correlation IDs, and trace IDs are related concepts but not universal synonyms.

The durable requirement is to preserve enough identity to connect related evidence across components.

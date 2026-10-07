---
id: DIA-D00-066
domain: D00
topic: D00-T012
title: User Journey Dependency Chain Reliability Outcome
type: end-to-end-diagram
status: published
---

# DIA-D00-066 — User Journey → Dependency Chain → Reliability Outcome

## Purpose

Show why reliability should be anchored to an important user journey rather than isolated infrastructure health.

~~~mermaid
flowchart LR
    USER[User<br/>Checkout] --> DNS[DNS]
    DNS --> LB[Load Balancer]
    LB --> APP[Application]
    APP --> AUTH[Authentication]
    APP --> DB[Database]
    APP --> PAY[Payment Provider]
    APP --> Q[Queue]
    Q --> WORK[Worker]

    DNS --> OUTCOME[User-Visible Outcome]
    LB --> OUTCOME
    AUTH --> OUTCOME
    DB --> OUTCOME
    PAY --> OUTCOME
    WORK --> OUTCOME
~~~

## Critical Question

~~~text
Can the user complete the important action
correctly and within acceptable time?
~~~

## Key Lesson

Healthy components do not automatically imply a reliable end-to-end user journey.

A weak critical dependency can dominate the outcome.

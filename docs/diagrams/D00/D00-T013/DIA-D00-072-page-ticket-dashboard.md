---
id: DIA-D00-072
domain: D00
topic: D00-T013
title: Page vs Ticket vs Dashboard
type: operations-decision-diagram
status: published
---

# DIA-D00-072 — Page vs Ticket vs Dashboard

## Purpose

Show how SRE separates urgent interruption from planned work and contextual telemetry.

~~~mermaid
flowchart TB
    SIGNAL[Operational Signal] --> URGENT{Urgent User Impact?}
    URGENT -->|Yes| ACTION{Immediate Human Action Needed?}
    ACTION -->|Yes| PAGE[Page]
    ACTION -->|No| TICKET[Ticket / Planned Follow-Up]
    URGENT -->|No| TREND{Action Needed Soon?}
    TREND -->|Yes| TICKET
    TREND -->|No| DASH[Dashboard / Context]
~~~

## Decision Model

~~~text
Page
→ urgent + actionable + immediate response

Ticket
→ action required, but not immediate interruption

Dashboard
→ context, investigation, awareness
~~~

## Key Lesson

The names and tools vary by organization.

The durable principle is **urgency + actionability + user impact**.

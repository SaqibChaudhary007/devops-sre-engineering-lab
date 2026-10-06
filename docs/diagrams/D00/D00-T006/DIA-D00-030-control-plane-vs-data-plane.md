---
id: DIA-D00-030
domain: D00
topic: D00-T006
title: Control Plane vs Data Plane
type: architecture-diagram
status: published
---

# DIA-D00-030 — Control Plane vs Data Plane

## Purpose

Separate resource management from workload-serving behavior.

~~~mermaid
flowchart TB
    ENGINEER[Engineer / Automation] --> API[Cloud API]
    API --> CP[Control Plane]
    CP --> CFG[Resource Configuration]

    USER[User] --> DP[Data Plane Resource]
    DP --> APP[Application / Service]
    APP --> DEP[(Data / Dependency)]
~~~

## Control-Plane Examples

- create VM
- change firewall rule
- create database
- change autoscaling policy
- assign permissions

## Data-Plane Examples

- serve user requests
- query a database
- read an object
- process a message

## Failure Insight

~~~text
Control plane degraded
≠
existing workload automatically unavailable

Data plane degraded
≠
cloud management API necessarily unavailable
~~~

## SRE Connection

User-facing SLIs usually reflect the workload/data path, not whether an engineer can open the cloud portal.

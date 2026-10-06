---
id: DIA-D00-023
domain: D00
topic: D00-T005
title: Physical Server Resource Model
type: infrastructure-diagram
status: published
---

# DIA-D00-023 — Physical Server Resource Model

## Purpose

Show the core hardware resources underneath operating systems, VMs, containers, and applications.

~~~mermaid
flowchart TB
    SERVER[Physical Server]

    SERVER --> CPU[CPU / Compute]
    SERVER --> MEM[RAM / Memory]
    SERVER --> DISK[Local Storage / Disk]
    SERVER --> NIC[Network Interface]
    SERVER --> POWER[Power / Cooling Dependencies]
~~~

## Mental Model

~~~text
Physical Server
├── Compute
├── Memory
├── Storage
├── Network
└── Physical dependencies
~~~

## Key Lesson

Infrastructure is more than "a server." A workload depends on several resource and physical layers at once.

## Troubleshooting Connection

Low CPU does not prove the system is healthy.

The real constraint could be:

- memory pressure
- storage latency
- network saturation
- physical host problems
- downstream dependencies

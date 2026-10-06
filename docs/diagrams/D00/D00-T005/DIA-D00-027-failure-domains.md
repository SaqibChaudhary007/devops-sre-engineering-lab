---
id: DIA-D00-027
domain: D00
topic: D00-T005
title: Failure Domains Host Rack Zone Region
type: reliability-diagram
status: published
---

# DIA-D00-027 — Failure Domains: Host → Rack → Zone → Region

## Purpose

Show why redundancy must be evaluated against what can fail together.

~~~mermaid
flowchart TB
    REGION[Region]

    REGION --> ZA[Zone A]
    REGION --> ZB[Zone B]

    ZA --> RACKA[Rack A]
    ZA --> RACKB[Rack B]
    ZB --> RACKC[Rack C]

    RACKA --> HOST1[Host 1]
    RACKA --> HOST2[Host 2]
    RACKB --> HOST3[Host 3]
    RACKC --> HOST4[Host 4]

    HOST1 --> VMA[VM A]
    HOST2 --> VMB[VM B]
    HOST4 --> VMC[VM C]
~~~

## Failure-Domain Questions

Two VMs exist. Ask:

~~~text
Same host?
Same rack?
Same switch?
Same storage?
Same power?
Same zone?
Same region?
~~~

## Weak Redundancy

~~~text
VM A + VM B
both on Host 1
→ one host failure removes both
~~~

## Stronger Separation

~~~text
VM A in Zone A
VM C in Zone B
→ one zone-level event is less likely to remove both
~~~

Provider topology and guarantees vary.

## Key Lesson

> Instance count is not the same as failure-domain independence.

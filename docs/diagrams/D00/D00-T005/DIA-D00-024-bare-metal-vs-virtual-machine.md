---
id: DIA-D00-024
domain: D00
topic: D00-T005
title: Bare Metal vs Virtual Machine
type: comparison-diagram
status: published
---

# DIA-D00-024 — Bare Metal vs Virtual Machine

## Purpose

Compare a workload running directly on physical hardware with a guest VM running through a virtualization layer.

## Bare-Metal Workload

~~~mermaid
flowchart TB
    APP1[Application]
    OS1[Operating System]
    HW1[Physical Hardware]

    APP1 --> OS1
    OS1 --> HW1
~~~

## Virtual Machine

~~~mermaid
flowchart TB
    APP2[Application]
    GUEST[Guest Operating System]
    VIRT[Virtual CPU / Memory / Disk / NIC]
    HYP[Hypervisor / Virtualization Layer]
    HW2[Physical Hardware]

    APP2 --> GUEST
    GUEST --> VIRT
    VIRT --> HYP
    HYP --> HW2
~~~

## Important Nuance

A hypervisor may itself run directly on physical hardware.

Therefore, in this topic, **bare-metal workload** means the general-purpose workload/OS is not running inside a VM.

## Failure-Domain Connection

Several VMs may share one physical host.

~~~text
Host fails
  ↓
Multiple guests may disappear together
~~~

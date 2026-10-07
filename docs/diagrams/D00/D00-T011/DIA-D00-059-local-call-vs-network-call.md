---
id: DIA-D00-059
domain: D00
topic: D00-T011
title: Local Call vs Network Call
type: comparison-diagram
status: published
---

# DIA-D00-059 — Local Call vs Network Call

## Purpose

Show why a remote call introduces latency, transport, independent failure, and uncertainty that do not exist in the same way for an in-process call.

## Local Call

~~~mermaid
flowchart LR
    A1[Caller] --> B1[Local Function / Component]
    B1 --> A1
~~~

## Network Call

~~~mermaid
flowchart LR
    A2[Caller] --> N1[Network Path]
    N1 --> B2[Remote Service]
    B2 --> N2[Network Path]
    N2 --> A2
~~~

## New Questions Introduced by Distribution

~~~text
Did the request arrive?
Did the remote side process it?
Was the response lost?
Is the remote side slow or failed?
Is the network path degraded?
~~~

## Key Lesson

A network call is not simply a slower local call.

It introduces independent failure and uncertainty.

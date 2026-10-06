---
id: DIA-D00-009
domain: D00
topic: D00-T002
title: Application I/O Through the Kernel
type: flow-diagram
status: published
---

# DIA-D00-009 — Application I/O Through the Kernel

## Purpose

Show how a user-space application reaches files and network resources through OS interfaces.

~~~mermaid
flowchart TB
    APP[Application Process]

    APP -->|open / read / write| SC1[System Call Interface]
    APP -->|socket / connect / send / receive| SC2[System Call Interface]

    SC1 --> VFS[Filesystem / VFS Layer]
    VFS --> BLOCK[Block I/O]
    BLOCK --> STORAGE[Storage Device]

    SC2 --> NET[Kernel Network Stack]
    NET --> NIC[Network Interface]
    NIC --> REMOTE[Remote System]

    STORAGE -->|Completion / Data| APP
    REMOTE -->|Response / Data| APP
~~~

## Important Clarification

This is a teaching abstraction. Actual kernel paths contain more layers and asynchronous behavior.

## Key Lesson

The application does not usually operate raw hardware directly. The kernel coordinates the I/O path.

## Troubleshooting Connection

Application latency can come from file I/O wait, filesystem behavior, storage latency, socket wait, network latency or a remote dependency.

## SRE Connection

Host-level I/O telemetry can explain service degradation, while request latency and errors show user impact.

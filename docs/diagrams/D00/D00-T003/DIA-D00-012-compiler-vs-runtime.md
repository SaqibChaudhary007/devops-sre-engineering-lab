---
id: DIA-D00-012
domain: D00
topic: D00-T003
title: Compiler vs Runtime-Driven Execution
type: comparison-diagram
status: published
---

# DIA-D00-012 — Compiler vs Runtime-Driven Execution

## Purpose

Compare two common software execution models without treating "compiled" and "interpreted" as an absolute language classification.

## Native/Ahead-of-Time Style

~~~mermaid
flowchart TB
    SRC[Source Code] --> COMP[Compiler / Toolchain]
    COMP --> OBJ[Object / Intermediate Output]
    OBJ --> LINK[Link / Package]
    LINK --> EXE[Executable Artifact]
    EXE --> OS[Operating System]
    OS --> CPU[CPU]
~~~

## Runtime-Driven Style

~~~mermaid
flowchart TB
    SRC2[Source / Bytecode] --> RT[Runtime / VM / Interpreter]
    RT --> OS2[Operating System]
    OS2 --> CPU2[CPU]
~~~

## Important Nuance

Real systems may combine:

- ahead-of-time compilation
- bytecode
- interpretation
- JIT compilation
- cached compiled forms

Therefore the useful question is:

> What execution model does this implementation actually use?

## Examples

~~~text
C / Go:
often compiled to native executable

Java:
source → class files → JVM

Python / CPython:
source → bytecode/runtime execution

JavaScript / Node.js:
source → JavaScript runtime
~~~

These are simplified examples, not universal rules for every implementation.

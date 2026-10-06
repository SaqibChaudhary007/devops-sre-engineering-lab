---
id: D00-T003
domain: D00
title: Software Engineering Foundations
level:
  - L1
  - L2
  - L3
priority: P1
status: published
estimated_time:
  theory: 4-6h
  practical: 1-2h
  assessment: 1-2h
prerequisites:
  required:
    - D00-T001
    - D00-T002
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - How It Really Works
  - Under the Hood
  - Five Levels
---

# 00.03 — Software Engineering Foundations

## Start Here

In 00.01, you learned how computers provide CPU, memory, storage, networking and I/O.

In 00.02, you learned how the operating system manages those resources for running processes.

Now we connect the next layer:

> How does human-written source code become a runnable application?

This topic builds the software-engineering mental model needed before CI/CD, containers, Kubernetes, cloud deployments and production troubleshooting.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- source code
- programming language
- compiler
- interpreter
- runtime
- dependency
- package
- library
- framework
- build process
- build tool
- artifact
- executable
- configuration
- environment
- versioning
- source control at a high level
- how source becomes something the OS can execute
- why software can work on one machine and fail on another
- why reproducible builds matter
- why dependencies create operational risk
- why build-time and runtime problems are different

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)
- [00.02 — Operating System Mental Model](../00-02-operating-system-mental-model/README.md)

You should already understand:

- CPU, memory, storage and network
- program vs process
- user space vs kernel space
- process execution
- files and filesystem abstraction
- process/resource relationships

---

# Learning Package Navigation

Use this page as the canonical learner entry point.

Move through the package in this order:

1. **Learn** — complete the conceptual sections on this page.
2. **Verify** — review the [D00-T003 Source Verification](../../../../docs/sources/D00/D00-T003-source-verification.md).
3. **Visualize** — review the [D00-T003 Visual Package](../../../../docs/diagrams/D00/D00-T003/README.md).
4. **Observe** — complete [OBS-D00-005 — Observe Source → Runtime → Process](../../../../labs/observation/D00/OBS-D00-005-observe-source-runtime-process.md).
5. **Build** — complete [OBS-D00-006 — Compile Source and Inspect the Artifact](../../../../labs/observation/D00/OBS-D00-006-compile-and-inspect-artifact.md).
6. **Break / Fix** — complete [EXP-D00-003 — Configuration, Startup Failure and Exit Status](../../../../labs/experiments/D00/EXP-D00-003-configuration-startup-exit-status.md).
7. **Assess** — complete the [D00-T003 Assessment Package](../../../../assessments/topics/D00/D00-T003/README.md).
8. **Teach Back** — explain the lifecycle at Beginner, Engineer, Senior, SRE and Architect levels.
9. **Continue** — move to 00.04 only after the completion gate is satisfied.

## Visual Package

The dedicated diagrams are:

- [DIA-D00-011 — Source to Process Lifecycle](../../../../docs/diagrams/D00/D00-T003/DIA-D00-011-source-to-process-lifecycle.md)
- [DIA-D00-012 — Compiler vs Runtime-Driven Execution](../../../../docs/diagrams/D00/D00-T003/DIA-D00-012-compiler-vs-runtime.md)
- [DIA-D00-013 — Dependency Graph](../../../../docs/diagrams/D00/D00-T003/DIA-D00-013-dependency-graph.md)
- [DIA-D00-014 — Build-Time vs Runtime Dependencies](../../../../docs/diagrams/D00/D00-T003/DIA-D00-014-buildtime-vs-runtime-dependencies.md)
- [DIA-D00-015 — Build Once, Promote the Artifact](../../../../docs/diagrams/D00/D00-T003/DIA-D00-015-build-once-promote.md)
- [DIA-D00-016 — Build vs Startup vs Runtime Failure](../../../../docs/diagrams/D00/D00-T003/DIA-D00-016-failure-stage-model.md)

## Practical Package

- [OBS-D00-005 — Observe Source → Runtime → Process](../../../../labs/observation/D00/OBS-D00-005-observe-source-runtime-process.md)
- [OBS-D00-006 — Compile Source and Inspect the Artifact](../../../../labs/observation/D00/OBS-D00-006-compile-and-inspect-artifact.md)
- [EXP-D00-003 — Configuration, Startup Failure and Exit Status](../../../../labs/experiments/D00/EXP-D00-003-configuration-startup-exit-status.md)

The practical assets remain **DRAFT** until they are executed end-to-end and promoted to `LAB-VERIFIED`.

## Assessment Package

The [D00-T003 Assessment Package](../../../../assessments/topics/D00/D00-T003/README.md) includes:

- 40-question knowledge check
- applied source/build/artifact/configuration scenario
- Senior/SRE/Architect follow-ups
- teach-back assessment
- scoring rubric
- remediation map

---

# 3. The Software Lifecycle Mental Model

A simplified software lifecycle:

~~~text
Idea / Requirement
      ↓
Source Code
      ↓
Dependencies
      ↓
Build / Package
      ↓
Artifact
      ↓
Configuration
      ↓
Runtime Environment
      ↓
Process
      ↓
Users / Other Systems
~~~

This is one of the most important mental models for DevOps.

CI/CD, Docker, Kubernetes and cloud platforms all operate around parts of this lifecycle.

---

# 4. What Is Source Code?

Source code is human-readable instructions written in a programming language.

Examples of languages:

- C
- C++
- Go
- Java
- Python
- JavaScript
- Rust
- C#

Example:

~~~python
print("hello")
~~~

A human can read this.

A CPU does not directly execute Python source text as machine instructions.

There must be a language/runtime/toolchain layer between source and CPU execution.

---

# 5. Programming Language

A programming language defines:

- syntax
- semantics
- data types
- control structures
- functions
- modules/packages
- rules for expressing software behavior

Different languages choose different execution models.

Examples:

~~~text
C / C++     → usually compiled to native machine code
Go          → commonly compiled to native executable
Java        → commonly compiled to bytecode and executed by JVM
Python      → commonly executed through Python runtime/interpreter
JavaScript  → commonly executed by a JavaScript runtime
~~~

These are high-level models. Real implementations may use JIT compilation, bytecode, ahead-of-time compilation or hybrid approaches.

---

# 6. Machine Code

Ultimately, the CPU executes machine instructions defined by its instruction-set architecture.

Examples:

- x86-64
- ARM64

A software toolchain must eventually produce or execute instructions compatible with the machine architecture.

This explains why:

> A binary built for one architecture may not run directly on another.

Example:

~~~text
x86-64 binary
≠
ARM64 binary
~~~

unless an appropriate compatibility/emulation layer exists.

---

# 7. Compiler

A compiler translates source code from one representation into another, often toward machine code or an intermediate representation.

Simplified:

~~~text
Source Code
   ↓
Compiler
   ↓
Object Code / Intermediate Code
   ↓
Linking / Packaging
   ↓
Executable / Artifact
~~~

For native compiled software, the final result may be an executable containing machine code.

---

# 8. Interpreter

An interpreter executes or evaluates program instructions through a runtime rather than requiring a standalone native executable produced in the same way as traditional ahead-of-time compilation.

Simplified:

~~~text
Source Code
   ↓
Interpreter / Runtime
   ↓
Execution
~~~

Examples commonly associated with interpreted/runtime-driven workflows include:

- Python
- shell scripts
- JavaScript

The distinction between "compiled" and "interpreted" is not always absolute.

Modern runtimes may:

- compile to bytecode
- use JIT compilation
- cache compiled forms
- translate code during execution

The correct engineering lesson is:

> Understand the actual execution model of the language/runtime you are operating.

---

# 9. Runtime

A runtime is the environment/software needed to execute an application.

Examples:

- Python runtime
- JVM
- .NET runtime
- Node.js runtime

A runtime may provide:

- memory management
- garbage collection
- libraries
- threading
- exception handling
- module loading
- JIT compilation
- OS interaction

Conceptually:

~~~text
Application Code
    ↓
Language Runtime
    ↓
Operating System
    ↓
Hardware
~~~

---

# 10. Compiled vs Runtime-Driven Application

## Native compiled model

~~~text
Source
  ↓
Compiler
  ↓
Executable
  ↓
Operating System
  ↓
CPU
~~~

## Runtime-driven model

~~~text
Source / Bytecode
  ↓
Runtime / VM / Interpreter
  ↓
Operating System
  ↓
CPU
~~~

Neither model is automatically "better."

They have different trade-offs in:

- portability
- startup behavior
- deployment
- runtime dependencies
- debugging
- performance

---

# 11. Library

A library is reusable code that another application can call.

Examples:

~~~text
Application
  ├── HTTP library
  ├── database library
  ├── logging library
  └── authentication library
~~~

Libraries reduce duplicated implementation effort.

But each dependency also introduces:

- versioning risk
- security risk
- compatibility risk
- maintenance responsibility

---

# 12. Framework

A framework provides a larger structure or application model.

Examples conceptually:

- web framework
- UI framework
- application framework

A library usually provides capabilities that your code calls.

A framework often defines more of the application's structure and lifecycle.

This distinction is useful, but exact boundaries vary.

---

# 13. Dependency

A dependency is software your application relies on.

Dependencies may include:

- libraries
- frameworks
- runtimes
- OS packages
- external services
- databases
- message brokers

This means dependency can exist at different layers.

~~~text
Source Dependency
Runtime Dependency
System Dependency
Network Dependency
~~~

A strong engineer always asks:

> What must exist for this application to build and run successfully?

---

# 14. Package

A package is a distributable unit used by an ecosystem/package manager.

Examples:

~~~text
Python package
npm package
RPM package
DEB package
Java package/archive
~~~

Package systems help manage:

- versions
- installation
- metadata
- dependencies
- distribution

Do not confuse package with application artifact in every context. Sometimes the terms overlap.

---

# 15. Dependency Graph

Applications rarely have only direct dependencies.

Example:

~~~text
Application
├── Library A
│   ├── Library C
│   └── Library D
└── Library B
    └── Library D
~~~

This creates a dependency graph.

A transitive dependency is a dependency of one of your dependencies.

That matters because a problem may exist in software your team did not directly add.

---

# 16. Versioning

Software changes over time.

Version numbers help identify releases.

Example:

~~~text
1.0.0
1.1.0
2.0.0
~~~

Versioning allows teams to reason about:

- compatibility
- upgrades
- fixes
- rollback
- dependency constraints

You will study semantic versioning and release strategies more deeply later.

At this stage:

> Version is part of software identity.

---

# 17. Source Control

Source control records changes to source code and related files.

Git is the most common tool you will study later.

A simple mental model:

~~~text
Source Files
   ↓
Version Control
   ↓
History
   ↓
Branches / Changes
   ↓
Review / Merge
~~~

Source control supports:

- collaboration
- history
- rollback
- review
- traceability

Deep Git belongs to D03.

---

# 18. Build Process

A build transforms source and supporting inputs into a deployable/testable output.

Depending on the language, a build may include:

- dependency resolution
- compilation
- transpilation
- linking
- tests
- static analysis
- packaging
- asset generation

Simplified:

~~~text
Source
+ Dependencies
+ Build Configuration
        ↓
      Build
        ↓
     Artifact
~~~

---

# 19. Build Tool

Build tools automate repeatable build steps.

Examples across ecosystems include:

- Make
- Maven
- Gradle
- npm scripts
- build systems integrated into language tooling

The important concept is not the tool name.

It is:

> The build should be predictable, repeatable and automatable.

---

# 20. Artifact

An artifact is an output produced by a build or packaging process that can be stored, tested, promoted or deployed.

Examples:

- executable binary
- JAR file
- ZIP/TAR package
- compiled static site
- container image
- package file

Conceptually:

~~~text
Commit
  ↓
Build
  ↓
Artifact
  ↓
Test
  ↓
Promote
  ↓
Deploy
~~~

This is the bridge into CI/CD.

---

# 21. Source vs Artifact

This distinction is foundational.

## Source

What developers edit.

## Artifact

What delivery systems deploy or promote.

Example:

~~~text
Git source code
      ↓
Build pipeline
      ↓
Application artifact
      ↓
Production
~~~

A mature delivery system should not rebuild differently for every environment without a strong reason.

---

# 22. Immutable Artifact Mental Model

A useful DevOps principle:

> Build once, promote the same artifact through environments.

Conceptually:

~~~text
Source Commit
     ↓
Build
     ↓
Artifact v1
  ┌──┼──┐
  ↓  ↓  ↓
Dev QA Prod
~~~

This reduces the risk that:

> "Production got a different build."

Environment-specific behavior should generally come from configuration rather than silently modifying the artifact.

---

# 23. Configuration

Configuration controls application behavior without changing core source code.

Examples:

- database host
- port
- log level
- feature flags
- API endpoint
- timeout
- environment mode

Conceptually:

~~~text
Artifact
+
Configuration
=
Running Application Behavior
~~~

This distinction becomes critical in CI/CD, containers and Kubernetes.

---

# 24. Configuration vs Code

A useful rule:

## Code

Defines software behavior/logic.

## Configuration

Selects or tunes behavior for an environment.

Example:

~~~text
Code:
"Connect to configured database"

Configuration:
DB_HOST=db.prod.example
~~~

Do not hardcode environment-specific values into source when they should be configuration.

---

# 25. Environment

An environment is a context where software runs.

Examples:

- local development
- development
- test
- QA
- staging
- production

An environment may differ by:

- configuration
- infrastructure
- secrets
- dependencies
- data
- scale
- permissions
- network access

This is why "works on my machine" is a real engineering problem.

---

# 26. "Works on My Machine"

Suppose the application works locally but fails in production.

Possible differences:

~~~text
Language/runtime version
OS libraries
Architecture
Configuration
Environment variables
Permissions
Network access
Database version
Dependency version
Filesystem path
Timezone
Locale
Secrets
Resource limits
~~~

So the problem may not be source code alone.

It may be environmental inconsistency.

---

# 27. Reproducible Build

A reproducible or deterministic build aims to produce predictable outputs from controlled inputs.

At a practical level, this means controlling things such as:

- source revision
- dependency versions
- build-tool version
- runtime/toolchain version
- configuration inputs
- build environment

The goal:

~~~text
Same controlled inputs
        ↓
Predictable build result
~~~

This improves confidence, debugging and supply-chain traceability.

---

# 28. Dependency Locking

If dependencies can change unexpectedly, a build can change even when application source does not.

Conceptually:

~~~text
Same Source
+
Different Dependency Version
=
Different Behavior
~~~

Lock files or explicit version constraints help control this risk.

Different ecosystems implement this differently.

---

# 29. Build-Time vs Runtime Dependency

This distinction is important.

## Build-time dependency

Needed to create the artifact.

Examples:

- compiler
- build tool
- development headers

## Runtime dependency

Needed while the application executes.

Examples:

- language runtime
- shared library
- database
- external API

A system can:

~~~text
Build successfully
but
Fail at runtime
~~~

because the runtime dependency is missing or incompatible.

---

# 30. Static vs Dynamic Linking — Preview

Native applications may include dependencies in different ways.

## Static linking

Required library code may be included in the produced binary.

## Dynamic linking

The executable may depend on shared libraries available at runtime.

Conceptually:

~~~text
Executable
  ↓
Needs Shared Library
  ↓
OS Loader
  ↓
Application Runs
~~~

This is only a preview.

Deep linker/loader behavior belongs later.

---

# 31. Application Startup

A simplified startup flow:

~~~text
Artifact exists on storage
       ↓
Runtime / loader starts
       ↓
Dependencies loaded
       ↓
Configuration read
       ↓
Process created
       ↓
Application initializes
       ↓
Network listeners / connections created
       ↓
Application becomes ready
~~~

Failure can occur at any step.

---

# 32. Build Failure vs Startup Failure vs Runtime Failure

## Build Failure

The artifact cannot be produced.

Examples:

- compilation error
- dependency resolution failure
- test failure

## Startup Failure

Artifact exists, but process cannot initialize.

Examples:

- missing configuration
- missing library
- port already in use
- permission denied

## Runtime Failure

Application starts but fails during operation.

Examples:

- dependency timeout
- memory leak
- database failure
- unexpected input
- resource exhaustion

This classification helps troubleshooting.

---

# 33. Logs and Error Messages

Software communicates failures through:

- logs
- exit codes
- exceptions
- error responses
- metrics
- traces

A useful engineering habit:

> Read the actual failure evidence before changing the system.

Do not immediately:

~~~text
restart
reinstall
rebuild
scale
~~~

without understanding the failure stage.

---

# 34. Exit Code — Preview

When a process finishes, it returns an exit status to the operating system.

A simple convention:

~~~text
0      → success
nonzero → some form of failure
~~~

Exact meanings depend on the program.

CI/CD systems use exit codes heavily to determine whether steps succeed or fail.

---

# 35. Application Version Identity

In production, you should be able to answer:

> What exact software version is running?

Useful identity can include:

~~~text
Application version
Git commit
Build number
Artifact version
Container image digest
Deployment version
~~~

Without version identity, troubleshooting and rollback become much harder.

---

# 36. Software Supply Chain — Introductory Mental Model

Software does not come only from your own source code.

~~~text
Your Source
+ Third-Party Dependencies
+ Build Tools
+ Base Runtime
+ Packages
        ↓
      Artifact
~~~

Every input introduces:

- trust
- provenance
- security
- compatibility
- maintenance considerations

Deep software supply-chain security belongs later.

---

# 37. Why Containers Became Useful

One historical problem:

> Software behaved differently because runtime environments differed.

Containers help package application runtime requirements into a more consistent deployment unit.

Conceptually:

~~~text
Application
+ Runtime
+ Libraries
+ Filesystem Content
        ↓
   Container Image
~~~

But containers do not eliminate:

- kernel dependencies
- architecture compatibility
- external dependencies
- configuration
- network requirements

---

# 38. Why CI/CD Exists

Manual build and deployment steps create inconsistency.

A delivery pipeline automates stages such as:

~~~text
Commit
  ↓
Build
  ↓
Test
  ↓
Package
  ↓
Artifact
  ↓
Deploy
  ↓
Validate
~~~

CI/CD will be studied deeply in D20.

At this stage, understand:

> CI/CD automates the software delivery lifecycle; it does not replace the lifecycle itself.

---

# 39. Senior Engineer Perspective

A senior engineer asks:

~~~text
What exact source revision?
What dependency versions?
What build produced this?
Which artifact is deployed?
What runtime does it require?
Which configuration is active?
What changed?
Can we reproduce the build?
Can we roll back safely?
~~~

When debugging:

> Identify the layer before choosing the tool.

---

# 40. SRE Perspective

SRE cares about how software lifecycle decisions affect reliability.

Examples:

~~~text
Unpinned dependency
        ↓
Unexpected build change
        ↓
Different production behavior
        ↓
Reliability incident
~~~

or:

~~~text
Artifact has no version identity
        ↓
Rollback uncertain
        ↓
Longer incident recovery
~~~

Delivery quality is a reliability concern.

---

# 41. Architect Perspective

An architect evaluates:

- runtime choice
- deployment model
- dependency strategy
- artifact model
- versioning
- portability
- support lifecycle
- build reproducibility
- operational skill
- security
- upgrade strategy

A technology choice is not only:

> Which language is fastest?

It is also:

> Can we build, operate, secure, upgrade and support this system reliably?

---

# 42. Common Beginner Mistakes

## Mistake 1

"Source code is what production runs."

Production usually runs an artifact/process derived from source.

## Mistake 2

"If it compiles, it will run."

Runtime dependencies/configuration may still fail.

## Mistake 3

"If it works locally, the application is correct."

Environment differences can invalidate that conclusion.

## Mistake 4

"Dependencies are only development concerns."

Dependencies are operational and security concerns too.

## Mistake 5

"CI/CD fixes software problems."

CI/CD automates build, test and delivery processes. It cannot make an incorrect design correct.

## Mistake 6

"Container image means environment differences are gone."

External dependencies, kernel, architecture, configuration and infrastructure still matter.

---

# 43. Five-Level Explanation

## L1 — Foundation

Developers write source code. Tools transform or execute it so the operating system can run an application.

## L2 — Engineer

Applications depend on toolchains, runtimes, libraries, configuration and build outputs called artifacts.

## L3 — Senior Engineer

Reliable delivery requires controlled dependencies, reproducible builds, versioned artifacts, environment-aware configuration and clear failure-stage diagnosis.

## L4 — SRE

Build and release quality directly affects reliability through change risk, rollback capability, observability and production consistency.

## L5 — Architect

Language, runtime, dependency, packaging and artifact strategies create long-term trade-offs across performance, security, operability, portability, cost and supportability.

---

# 44. What You Must Retain

Before moving on, retain:

- source code is not the same as a running application
- CPU executes machine instructions, often through a compiler/runtime toolchain
- compiler, interpreter and runtime are different concepts
- dependencies exist at build time and runtime
- a build produces an artifact
- the deployed artifact should have clear identity/version
- configuration should be separated from core code where appropriate
- environment differences cause real production failures
- build success does not guarantee startup/runtime success
- reproducibility reduces uncertainty
- dependency versions affect behavior
- artifacts connect development to delivery
- CI/CD automates this lifecycle
- containers package part of the runtime environment but not the entire world around the application

---

# 45. Practical Package

Complete the practical assets:

1. [OBS-D00-005 — Observe Source → Runtime → Process](../../../../labs/observation/D00/OBS-D00-005-observe-source-runtime-process.md)
2. [OBS-D00-006 — Compile Source and Inspect the Artifact](../../../../labs/observation/D00/OBS-D00-006-compile-and-inspect-artifact.md)
3. [EXP-D00-003 — Configuration, Startup Failure and Exit Status](../../../../labs/experiments/D00/EXP-D00-003-configuration-startup-exit-status.md)

These labs turn the mental model into observable behavior.

---

# 46. Assessment Package

Complete the [D00-T003 Assessment Package](../../../../assessments/topics/D00/D00-T003/README.md).

It tests:

- compilation vs runtime-driven execution
- source vs artifact
- build-time vs runtime dependency
- configuration vs code
- reproducibility
- environment drift
- failure-stage reasoning
- Senior/SRE/Architect trade-offs

---

# 47. Visual Package

Review the [D00-T003 Visual Package](../../../../docs/diagrams/D00/D00-T003/README.md).

The package includes:

1. Source → Build → Artifact → Runtime → Process
2. Compiler vs Runtime-Driven Execution
3. Dependency Graph
4. Build-Time vs Runtime Dependency
5. Build Once → Promote Artifact
6. Build vs Startup vs Runtime Failure

---

# 48. Completion Gate

Before moving on, confirm that you can:

- explain source → build/runtime → artifact → process
- distinguish compiler, interpreter and runtime
- distinguish direct, transitive, build-time and runtime dependencies
- explain source vs artifact
- explain configuration vs code
- explain why a green build does not prove production health
- classify build, startup and runtime failures
- explain why exact artifact identity matters
- explain the purpose and limits of dependency locking
- explain why reproducibility reduces uncertainty
- complete the practical package
- score at least 80% on the knowledge check
- demonstrate at least L3 / FD-3 reasoning
- teach the lifecycle clearly without relying on notes

# 49. What Comes Next

After D00-T003 is completed, continue to:

## 00.04 — Application Architecture Fundamentals

That topic connects individual software artifacts into systems:

- client/server
- three-tier architecture
- monolith
- microservices
- APIs
- state
- data stores

---

# 50. Sources & Evidence

Planned authoritative source families for verification:

- language/runtime official documentation
- GNU compiler/build documentation
- Python documentation
- Java/JVM documentation
- Node.js documentation
- package-manager documentation
- Git documentation
- reproducible-build guidance
- software supply-chain standards/guidance

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification pass: complete
- practical package: authored as DRAFT; LAB-VERIFICATION pending
- assessment package: authored and cross-linked
- visual package: authored and cross-linked
- canonical learner journey: integrated

Detailed verification record:

- [D00-T003 Source Verification](../../../../docs/sources/D00/D00-T003-source-verification.md)

Verified nuances:

- compiled vs interpreted is not a strict language binary
- dependency locking improves repeatability but is not full reproducibility
- artifacts are ecosystem/context dependent
- build-once/promote is a delivery principle rather than a universal law
- container images package user-space content, not the host kernel


## Topic Package Status

**D00-T003 is structurally complete.**

Remaining quality work is operational verification of the practical labs. Once those labs are successfully executed on supported environments, their evidence status can be promoted from DRAFT to LAB-VERIFIED.

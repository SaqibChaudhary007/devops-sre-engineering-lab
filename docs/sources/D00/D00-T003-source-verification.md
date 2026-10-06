# D00-T003 Source Verification — Software Engineering Foundations

## Verification Goal

Verify the core factual claims in **00.03 — Software Engineering Foundations** against primary or authoritative documentation before treating the topic as DOC-VERIFIED.

## Verification Status

**Result:** Core claims verified.

**Evidence level:** E2 — documented by primary/official sources.

This verification does not mean every language ecosystem behaves identically. The topic intentionally teaches portable mental models and marks implementation-specific behavior as examples.

## Verified Claim Map

| Topic claim | Verification | Source |
|---|---|---|
| GCC compilation can include preprocessing, compilation, assembly and linking stages | Verified | GNU GCC manual |
| Compiling without linking can produce object files | Verified | GNU GCC manual |
| Java source can be compiled into class files executed by the JVM | Verified | Oracle javac / JVM documentation |
| CPython compiles Python source into bytecode used by the interpreter/runtime | Verified | Python documentation |
| Node.js provides a JavaScript runtime/process model and module system | Verified | Node.js documentation |
| Git provides source-history, commit, branch and merge workflows | Verified | Git official reference |
| Semantic Versioning uses MAJOR.MINOR.PATCH with defined compatibility meaning | Verified | Semantic Versioning specification |
| npm lockfiles record an exact dependency tree to improve repeatable installs | Verified | npm documentation |
| Reproducible builds depend on controlled source, build environment and build instructions | Verified | Reproducible Builds definition |
| Container images can package application files, binaries, libraries and configuration | Verified | Docker documentation |
| Container images use immutable layers | Verified | Docker documentation |

## Primary Sources

### GNU Compiler Collection

- https://gcc.gnu.org/onlinedocs/gcc/Invoking-GCC.html
- https://gcc.gnu.org/onlinedocs/gcc/Overall-Options.html
- https://gcc.gnu.org/onlinedocs/gcc/Link-Options.html

Supports the simplified model of preprocessing, compilation, assembly, linking, object files and executables.

### Python

- https://docs.python.org/3/reference/executionmodel.html
- https://docs.python.org/3/glossary.html#term-bytecode

Supports the claim that CPython uses compiled bytecode internally and an interpreter/runtime executes program behavior.

Important nuance: "interpreted language" is an oversimplification. Python implementations may compile to bytecode and use different execution techniques.

### Java / JVM

- https://docs.oracle.com/en/java/javase/26/docs/specs/man/javac.html
- https://docs.oracle.com/en/java/javase/26/vm/index.html

Supports the model:

~~~text
Java Source
→ javac
→ Class Files
→ JVM
→ Operating System
~~~

### Node.js

- https://nodejs.org/api/process.html
- https://nodejs.org/api/modules.html

Supports Node.js as a JavaScript runtime with a process model and module loading system.

### Git

- https://git-scm.com/docs

Supports the topic's high-level source-control concepts including commit, branch, merge and history.

### Semantic Versioning

- https://semver.org/

Supports MAJOR.MINOR.PATCH semantics. The topic treats SemVer as one versioning model, not a universal requirement.

### npm Dependency Locking

- https://docs.npmjs.com/files/package-lock.json/
- https://docs.npmjs.com/cli/install/

Supports the claim that lockfiles capture resolved dependency trees and help installations use consistent dependency versions.

Important nuance: a lockfile improves dependency repeatability but does not by itself guarantee fully bit-for-bit reproducible builds.

### Reproducible Builds

- https://reproducible-builds.org/docs/definition/

Defines a reproducible build as one where the same source, build environment and build instructions can recreate bit-for-bit identical specified artifacts.

### Docker Images

- https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/
- https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers/

Supports the claim that images package application/runtime filesystem content and use immutable layers.

## Verified Nuances / Corrections

### 1. Compiled vs Interpreted Is Not a Strict Language Property

Prefer:

> Languages and implementations use execution models that may include ahead-of-time compilation, bytecode, interpreters, JIT compilation or combinations of these.

### 2. Build Artifact Is Context-Dependent

Artifact is a build/delivery term, not one universal file type.

Examples include executable binaries, JARs, package archives, static-site outputs and container images.

### 3. Lockfile Is Not Full Reproducibility

Dependency locking controls one important input. Full reproducibility may also depend on toolchain versions, environment, source revision, build instructions, locale, timestamps and OS packages.

### 4. Build Once, Promote Is a Delivery Principle

It is a recommended delivery model intended to improve traceability and reduce environment-specific rebuild differences, not a universal law.

### 5. Container Images Do Not Package the Host Kernel

Container images package user-space application/runtime content. Common Linux containers still use the host kernel, preserving the boundary established in D00-T002.

## Evidence Decision

The following D00-T003 areas are now eligible for **DOC-VERIFIED** status:

- compiler/build pipeline mental model
- runtime/interpreter mental model
- Java/JVM example
- Python bytecode/runtime example
- Node.js runtime example
- source-control mental model
- semantic-versioning example
- dependency-locking principle
- reproducible-build definition
- container-image packaging model

## Not Yet LAB-VERIFIED

Documentation verification is not laboratory verification.

The following still require hands-on execution:

- compiling a native program
- inspecting a produced executable
- comparing native vs Python execution
- producing a controlled startup/configuration failure
- inspecting exit status
- demonstrating artifact identity

Those become the D00-T003 practical package.

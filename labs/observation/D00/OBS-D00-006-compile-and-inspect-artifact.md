---
id: OBS-D00-006
domain: D00
topics:
  - D00-T003
level: L2
type: observation
status: draft
estimated_time: 40-60m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-006 — Compile Source and Inspect the Artifact

## Objective

Observe a simple native compilation flow:

~~~text
C Source
→ Compiler
→ Executable Artifact
→ Process
~~~

## Safety

This lab compiles and runs a tiny local program.

## Prerequisites

- D00-T003
- Linux shell
- GCC installed

Check:

~~~bash
gcc --version
~~~

If GCC is unavailable, do not install packages without permission. Mark the lab as not runnable in that environment.

## 1. Create C Source

~~~bash
mkdir -p /tmp/d00-t003-native
cd /tmp/d00-t003-native

cat > hello.c <<'C'
#include <stdio.h>

int main(void) {
    printf("Hello from compiled code\n");
    return 0;
}
C
~~~

Inspect it:

~~~bash
cat hello.c
file hello.c
~~~

## 2. Compile to an Object File

~~~bash
gcc -c hello.c -o hello.o
~~~

Inspect:

~~~bash
file hello.o
ls -lh hello.c hello.o
~~~

At this point you have an object file, not the final executable.

## 3. Link the Executable

~~~bash
gcc hello.o -o hello
~~~

Inspect:

~~~bash
file hello
ls -lh hello
~~~

## 4. Run the Artifact

~~~bash
./hello
echo $?
~~~

## 5. Compare Source and Artifact

Run:

~~~bash
sha256sum hello.c hello.o hello
~~~

These hashes identify the exact byte content of each file at this moment.

### Mental Model

~~~text
hello.c
  ↓ compile
hello.o
  ↓ link
hello
  ↓ execute
Process
~~~

## 6. Architecture Connection

Inspect:

~~~bash
uname -m
file hello
~~~

Compare the machine architecture with the executable description.

## Questions

1. What is the difference between hello.c and hello?
2. Why is hello.o not the same thing as the final executable?
3. What role did the compiler/linker workflow play?
4. Why can architecture matter when moving native binaries between machines?
5. Why is the produced executable an artifact?

## Validation Checklist

- [ ] Created source code
- [ ] Produced an object file
- [ ] Produced an executable
- [ ] Ran the artifact
- [ ] Observed successful exit status
- [ ] Compared source/object/executable identities
- [ ] Connected artifact to architecture

## Interview Connection

Question:

> What is the difference between source code and a deployable artifact?

A strong answer explains that source is developer-authored input while an artifact is a produced output intended for testing, distribution or deployment.

## Cleanup

~~~bash
rm -rf /tmp/d00-t003-native
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution on supported environments.

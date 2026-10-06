
---
id: OBS-D00-004
domain: D00
topics:
  - D00-T002
level: L2
type: observation
status: draft
estimated_time: 35-50m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-004 — Observe System Calls

## Objective

See that a user-space application relies on the kernel for operations such as opening files, writing output and interacting with the operating system.

## Why This Matters

The system-call boundary is one of the most important transitions in operating-system design.

~~~text
Application
   ↓
System Call
   ↓
Kernel
   ↓
Resource
~~~

## Safety

This lab traces a simple local command only.

## Prerequisites

- D00-T002
- Linux shell
- strace installed

Check:

~~~bash
strace -V
~~~

If strace is unavailable, mark this lab as not runnable yet and do not install packages unless you have permission to do so.

---

## 1. Trace a Simple Command

Run:

~~~bash
strace -o /tmp/d00-strace.txt echo "hello operating system"
~~~

Now inspect the first lines:

~~~bash
head -30 /tmp/d00-strace.txt
~~~

You may see calls related to:

- opening files
- memory mappings
- reading
- writing
- process termination

Exact output differs by distribution and library/runtime version.

---

## 2. Find the Write Operation

Run:

~~~bash
grep -E 'write\(' /tmp/d00-strace.txt | tail
~~~

Find the call that writes the text to standard output.

### Mental Model

~~~text
echo program
   ↓
write system call
   ↓
kernel
   ↓
terminal / output device
~~~

---

## 3. Trace File Access

Create a small file:

~~~bash
echo "kernel boundary lab" > /tmp/d00-os-lab.txt
~~~

Trace reading it:

~~~bash
strace -o /tmp/d00-cat-strace.txt cat /tmp/d00-os-lab.txt
~~~

Search for file-related calls:

~~~bash
grep -E 'openat|read\(|close\(' /tmp/d00-cat-strace.txt | head -30
~~~

### Think

- Did the application directly read physical disk sectors?
- Which layer provided the file abstraction?

---

## 4. Observe Failed Access

Trace a missing file:

~~~bash
strace -o /tmp/d00-missing-strace.txt cat /tmp/this-file-does-not-exist
~~~

Then:

~~~bash
grep -E 'ENOENT|openat' /tmp/d00-missing-strace.txt | tail -10
~~~

Observe that an application error can originate from a kernel-returned error condition.

---

## 5. Connect to Production Troubleshooting

Imagine an application logs:

~~~text
Permission denied
No such file or directory
Connection refused
Too many open files
~~~

These often correspond to OS/kernel-level conditions visible through system calls.

This is why system-call tracing can be useful later in Linux troubleshooting.

---

## Validation Checklist

- [ ] Traced a simple command
- [ ] Identified a write system call
- [ ] Traced a file read
- [ ] Observed a failed file lookup
- [ ] Explained why applications need kernel services

## Interview Connection

Question: Why can a user-space process not just access hardware directly?

Strong answer: controlled kernel interfaces enforce protection, abstraction, portability and resource management.

## Cleanup

~~~bash
rm -f /tmp/d00-strace.txt /tmp/d00-cat-strace.txt /tmp/d00-missing-strace.txt /tmp/d00-os-lab.txt
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after execution on supported environments.


---
id: OBS-D00-003
domain: D00
topics:
  - D00-T002
level: L1-L2
type: observation
status: draft
estimated_time: 35-50m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-003 — Observe the Operating System Boundary

## Objective

Observe the difference between user-space processes and kernel-provided system information.

The goal is to connect this mental model:

~~~text
User Process
   ↓
Operating System Interface
   ↓
Kernel
   ↓
Hardware / Resources
~~~

to a real Linux system.

## Safety

This lab is read-only.

## Prerequisites

- D00-T001 — How Computers Work
- D00-T002 — Operating System Mental Model
- Linux shell access

---

## 1. Identify the Kernel

Run:

~~~bash
uname -r
uname -a
~~~

Observe the running kernel version and machine architecture.

Then:

~~~bash
cat /proc/version
~~~

### Think

- Is the kernel the same thing as the shell?
- Is the kernel the same thing as the Linux distribution?

---

## 2. Observe User Space

List some running processes:

~~~bash
ps -eo pid,ppid,user,stat,comm --sort=pid | head -25
~~~

Observe:

- PID
- parent PID
- user
- process state
- command

### Mental Model

~~~text
Applications / daemons / shells
        ↓
      User Space
        ↓
      Kernel
~~~

---

## 3. Observe Kernel-Exposed Process Information

Choose your current shell PID:

~~~bash
echo $$
~~~

Then inspect:

~~~bash
cat /proc/$$/status | head -30
~~~

and:

~~~bash
ls -l /proc/$$/fd | head
~~~

Observe that the kernel exposes information about the process through the virtual /proc filesystem.

### Think

- Is /proc simply a normal disk directory?
- What kind of runtime information can the OS expose about a process?

---

## 4. Observe Kernel Resource Views

CPU information:

~~~bash
cat /proc/cpuinfo | head -30
~~~

Memory information:

~~~bash
head -20 /proc/meminfo
~~~

Mounted filesystems:

~~~bash
cat /proc/mounts | head -20
~~~

Network interfaces:

~~~bash
cat /proc/net/dev
~~~

### Key Lesson

The kernel maintains and exposes system state across CPU, memory, filesystems, processes and networking.

---

## 5. Observe Process Ownership

Run:

~~~bash
ps -o pid,user,group,comm -p $$
~~~

Then:

~~~bash
id
~~~

Observe:

- your UID/user
- groups
- process ownership

### Think

Why does the operating system associate processes with identities?

Connect this to:

- permissions
- security
- blast radius
- access control

---

## 6. Observe a Privilege Boundary

Try reading a generally accessible file:

~~~bash
cat /etc/os-release
~~~

Now inspect a file that is commonly restricted to privileged users:

~~~bash
ls -l /etc/shadow
~~~

Do not attempt to bypass permissions.

### Think

- Why should every process not have unrestricted access?
- How does this protect the system?

---

## Validation Checklist

- [ ] Kernel version identified
- [ ] User-space processes observed
- [ ] /proc process state inspected
- [ ] CPU/memory/filesystem/network kernel views inspected
- [ ] User and group identity observed
- [ ] Permission boundary recognized

## Expected Learning Result

You should be able to explain that applications run as user-space processes while the kernel manages privileged resources and exposes controlled interfaces and system state.

## Troubleshooting Connection

When an application fails, useful questions include:

- Is the process present?
- Which user owns it?
- What state is it in?
- Does it have access to the required file/device?
- What does the kernel report about system resources?

## Teach-Back

Explain why user space and kernel space are separated, using one security example and one reliability example.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution on supported environments.

---
id: OBS-D00-005
domain: D00
topics:
  - D00-T003
level: L1-L2
type: observation
status: draft
estimated_time: 30-45m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-005 — Observe Source → Runtime → Process

## Objective

Connect source code to a real running process.

~~~text
Source File
→ Language Runtime
→ Process
→ Operating System
~~~

## Safety

This is a local, short-lived observation exercise.

## Prerequisites

- D00-T001
- D00-T002
- D00-T003
- Python 3
- Linux shell

## 1. Create Source Code

~~~bash
mkdir -p /tmp/d00-t003-source-runtime
cd /tmp/d00-t003-source-runtime

cat > hello.py <<'PY'
import os
import time

print("Hello from source code")
print("PID:", os.getpid())
time.sleep(30)
PY
~~~

Inspect the source:

~~~bash
cat hello.py
file hello.py
~~~

## 2. Run the Source Through the Runtime

~~~bash
python3 hello.py &
APP_PID=$!
echo "$APP_PID"
~~~

Immediately inspect:

~~~bash
ps -o pid,ppid,user,stat,%cpu,%mem,etime,cmd -p "$APP_PID"
~~~

## 3. Identify the Runtime

~~~bash
command -v python3
python3 --version
~~~

Then inspect the process executable link:

~~~bash
readlink -f /proc/"$APP_PID"/exe
~~~

## 4. Connect the Layers

Explain what each layer is:

~~~text
hello.py
   ↓
python3 runtime
   ↓
Linux process
   ↓
Operating system
   ↓
CPU / memory / I/O
~~~

## 5. Observe Completion

Wait for the process:

~~~bash
wait "$APP_PID"
echo $?
~~~

The final command prints the process exit status.

## Questions

1. Is hello.py itself the running process?
2. What program actually appears as the process executable?
3. Why does the Python runtime need the operating system?
4. What is the difference between source code and process state?
5. What does exit status 0 normally indicate?

## Validation Checklist

- [ ] Created a source file
- [ ] Identified the language runtime
- [ ] Started the application
- [ ] Observed its PID/process
- [ ] Connected source → runtime → OS
- [ ] Observed the exit status

## Teach-Back

Explain why this statement is incomplete:

> "Production runs the source code."

## Cleanup

~~~bash
rm -rf /tmp/d00-t003-source-runtime
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution on supported environments.

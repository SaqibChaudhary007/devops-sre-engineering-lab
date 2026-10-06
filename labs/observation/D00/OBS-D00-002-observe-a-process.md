
---
id: OBS-D00-002
domain: D00
topics:
  - D00-T001
level: L1-L2
type: observation
status: draft
estimated_time: 30-45m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-002 — Observe a Process

## Objective

Connect:

~~~text
Program → Process → Operating System → CPU / Memory
~~~

to a real Linux system.

## Why This Matters

Files stored on disk are not the same thing as running processes. Before systemd, Docker or Kubernetes, understand the basic unit doing work: a process.

## Safety

Run this only on a lab/workstation environment. The lab starts a simple local Python web server and stops it afterward.

## Prerequisites

- D00-T001
- Python 3
- Linux shell

Check:

~~~bash
python3 --version
~~~

## 1. Find the Program

~~~bash
command -v python3
ls -l "$(command -v python3)"
~~~

Think: Is the executable file itself a process?

## 2. Start a Process

~~~bash
mkdir -p /tmp/d00-process-lab
cd /tmp/d00-process-lab
echo "D00 process lab" > index.html
python3 -m http.server 8000
~~~

Leave this terminal running.

## 3. Find the Process

Open another terminal:

~~~bash
pgrep -af "python3 -m http.server"
~~~

Record the PID and command.

Then inspect it:

~~~bash
ps -o pid,ppid,user,stat,%cpu,%mem,etime,cmd -p <PID>
~~~

Replace <PID> with the real PID.

## 4. Observe Process State

~~~bash
cat /proc/<PID>/status | head -30
~~~

Look for Name, State, Pid, PPid, Threads and memory fields.

Mental model:

~~~text
Executable on storage
      ↓
OS starts it
      ↓
Process receives PID
      ↓
Process has memory/state
      ↓
Scheduler gives CPU time
~~~

## 5. Generate Work

~~~bash
curl http://127.0.0.1:8000/
for i in {1..10}; do curl -s http://127.0.0.1:8000/ >/dev/null; done
~~~

Then inspect again:

~~~bash
ps -o pid,stat,%cpu,%mem,etime,cmd -p <PID>
~~~

Think:
- What was the process doing while idle?
- What changed when requests arrived?

## 6. Observe the Listening Socket

~~~bash
ss -ltnp | grep ':8000'
~~~

Connect:

~~~text
Process
  ↓
Socket
  ↓
TCP port 8000
  ↓
Client request
~~~

## 7. Stop the Process

Return to the server terminal and press Ctrl+C.

Verify:

~~~bash
pgrep -af "python3 -m http.server"
curl --max-time 2 http://127.0.0.1:8000/
~~~

The endpoint should no longer be served by that process.

## Validation Checklist

- [ ] Found the executable on disk
- [ ] Started a process
- [ ] Identified its PID
- [ ] Observed CPU/memory fields
- [ ] Observed process state
- [ ] Sent traffic to the process
- [ ] Observed the listening socket
- [ ] Stopped the process
- [ ] Verified endpoint unavailability afterward

## Troubleshooting Connection

For an unavailable application:
1. Is its process running?
2. Is it listening on the expected address and port?
3. Is it healthy or stuck?
4. Can requests reach it?

## Interview Connection

Question: What is the difference between a program and a process?

Strong answer: A program is executable code/data stored as an artifact. A process is a running instance with execution state, memory, identifiers and OS-managed resources.

## Teach-Back

Explain:

~~~text
File on disk
→ Process
→ PID
→ CPU / Memory
→ Socket
→ Request
~~~

## Cleanup

~~~bash
rm -rf /tmp/d00-process-lab
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution.

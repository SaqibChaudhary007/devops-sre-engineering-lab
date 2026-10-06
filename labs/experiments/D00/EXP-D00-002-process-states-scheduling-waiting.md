
---
id: EXP-D00-002
domain: D00
topics:
  - D00-T002
level: L2-L3
type: experiment
status: draft
estimated_time: 40-60m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# EXP-D00-002 — Process States, Scheduling and Waiting

## Objective

Observe that a process can exist without actively using CPU, and connect process state to the idea of waiting.

## Safety

This experiment uses short-lived local processes only.

Do not run on production/shared systems.

## Prerequisites

- D00-T001
- D00-T002
- Python 3

---

# Experiment A — Sleeping Process

Start a sleeping process:

~~~bash
sleep 60 &
SLEEP_PID=$!
echo "$SLEEP_PID"
~~~

Inspect it:

~~~bash
ps -o pid,ppid,stat,%cpu,%mem,etime,cmd -p "$SLEEP_PID"
~~~

Observe the STAT column.

### Think

- Is the process alive?
- Is it actively consuming CPU?
- What is it doing?

This demonstrates:

> Process exists ≠ process is currently executing.

---

# Experiment B — CPU-Active Process

Run a bounded CPU workload in the background:

~~~bash
python3 - <<'PY' &
import time
end = time.time() + 20
x = 0
while time.time() < end:
    x = (x * 3 + 7) % 10000019
PY
CPU_PID=$!
echo "$CPU_PID"
~~~

Immediately inspect:

~~~bash
ps -o pid,ppid,stat,%cpu,%mem,etime,cmd -p "$CPU_PID"
~~~

Run it a few times while the process is active.

### Compare

~~~text
Sleeping process
vs
CPU-active process
~~~

Record:

~~~text
Sleeping process state:
Sleeping process CPU:
CPU workload state:
CPU workload CPU:
~~~

---

# Experiment C — Observe Scheduler Competition

First see how many logical CPUs are available:

~~~bash
nproc
~~~

Then run two short CPU workers:

~~~bash
python3 - <<'PY' &
import time
end=time.time()+15
while time.time()<end:
    pass
PY
P1=$!

python3 - <<'PY' &
import time
end=time.time()+15
while time.time()<end:
    pass
PY
P2=$!
~~~

Observe:

~~~bash
top -p "$P1","$P2"
~~~

Press q after observing.

### Think

- If the system has many CPUs, did both receive CPU time simultaneously?
- If CPU capacity were constrained, what would happen to runnable work?
- Why does scheduling matter to latency?

---

# Experiment D — Waiting as a Troubleshooting Idea

Consider two applications:

~~~text
Application A: high CPU, performing computation
Application B: low CPU, waiting for network response
~~~

Which one can still be slow?

Answer: both.

The reason differs:

~~~text
A → computation bottleneck
B → waiting/dependency bottleneck
~~~

This is one of the most important operating-system troubleshooting mental models.

---

## Validation Checklist

- [ ] Observed a sleeping process
- [ ] Observed a CPU-active process
- [ ] Compared process states and CPU usage
- [ ] Observed multiple runnable workloads
- [ ] Explained why an alive process can consume almost no CPU
- [ ] Explained why low CPU can still mean poor application performance

## Senior Engineer Connection

When a service is slow, ask:

> Is the process running, runnable, blocked, sleeping or waiting on something?

Do not rely only on process existence.

## SRE Connection

Process state and host metrics help explain why an SLI is degrading, but the user-facing signal remains the reliability outcome.

## Cleanup

~~~bash
kill "$SLEEP_PID" 2>/dev/null || true
wait "$CPU_PID" 2>/dev/null || true
wait "$P1" 2>/dev/null || true
wait "$P2" 2>/dev/null || true
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution.

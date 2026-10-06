
---
id: EXP-D00-001
domain: D00
topics:
  - D00-T001
level: L2
type: experiment
status: draft
estimated_time: 30-45m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# EXP-D00-001 — Resource Consumption Experiment

## Objective

Create small, bounded workloads and observe how workload changes resource usage.

~~~text
Workload
→ Resource Demand
→ Observable System Behavior
~~~

## Safety

Lab environment only.

- Do not run on production/shared infrastructure.
- CPU activity is bounded to about 20 seconds.
- Memory allocation is bounded to about 100 MiB.
- Stop with Ctrl+C if the system behaves unexpectedly.

## Prerequisites

- OBS-D00-001 recommended
- Python 3
- Linux shell

# Experiment A — CPU Work

## Baseline

Open Terminal A:

~~~bash
top
~~~

## Generate bounded CPU work

In Terminal B:

~~~bash
python3 - <<'PY'
import time
end = time.time() + 20
x = 0
while time.time() < end:
    x = (x * 3 + 1) % 10000019
print("completed", x)
PY
~~~

Record:

~~~text
CPU before:
CPU during:
Process using CPU:
CPU after:
~~~

Questions:
1. Did total system CPU reach 100%?
2. How does the number of logical CPUs affect what you see?
3. Why can one busy process coexist with spare system capacity?

# Experiment B — Temporary Memory Allocation

Baseline:

~~~bash
free -h
~~~

Allocate about 100 MiB temporarily:

~~~bash
python3 - <<'PY'
import time
size = 100 * 1024 * 1024
data = bytearray(size)
for i in range(0, size, 4096):
    data[i] = 1
print("Holding about 100 MiB for 20 seconds...")
time.sleep(20)
print("Released on process exit.")
PY
~~~

While it runs:

~~~bash
free -h
~~~

After it exits:

~~~bash
free -h
~~~

Record:

~~~text
Available memory before:
Available memory during:
Available memory after:
~~~

Questions:
1. Did available memory change?
2. Did values return to exactly the same numbers?
3. Why should small changes not automatically be called a memory problem?

# Experiment C — Network Counter Change

Identify the default interface:

~~~bash
IFACE=$(ip route | awk '/default/ {print $5; exit}')
echo "$IFACE"
ip -s link show "$IFACE"
~~~

Generate a small request:

~~~bash
curl -s https://example.com/ >/dev/null
~~~

Check again:

~~~bash
ip -s link show "$IFACE"
~~~

Questions:
1. Did RX/TX counters increase?
2. Why can network activity occur with very little CPU impact?
3. What would you measure to understand latency rather than only bytes/packets?

## Correlation Table

| Workload | CPU | Memory | Storage | Network |
|---|---|---|---|---|
| Idle | Baseline | Baseline | Baseline | Baseline |
| CPU loop | Increase expected | Small | Minimal | Minimal |
| 100 MiB allocation | Small | Increase expected | Minimal | Minimal |
| HTTP request | Small | Small | Minimal | RX/TX increase expected |

Actual values vary by environment.

## Core Reasoning

A changed metric is evidence, not automatic root cause.

The useful question is:

> What is the workload doing, what resource is limiting it, and what is it waiting for?

## SRE Connection

Resource metrics are diagnostic signals. User-facing latency, errors and availability determine whether reliability is affected.

## Validation Checklist

- [ ] CPU baseline observed
- [ ] Bounded CPU workload observed
- [ ] Memory before/during/after observed
- [ ] Network counters before/after request observed
- [ ] Explained why resource changes are not automatically root causes

## Cleanup

The CPU and memory processes exit automatically. No persistent files are created.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution on supported environments.

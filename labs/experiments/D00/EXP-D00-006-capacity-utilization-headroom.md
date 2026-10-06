---
id: EXP-D00-006
domain: D00
topics:
  - D00-T005
level: L2-L3
type: experiment
status: draft
estimated_time: 35-50m
environment:
  - Personal Linux VM or lab workstation
evidence_status:
  - DRAFT
---

# EXP-D00-006 — Capacity, Utilization, and Headroom with a Bounded Workload

## Objective

Observe the difference between:

- total capacity
- current utilization
- temporary load
- remaining headroom

without performing an uncontrolled stress test.

## Safety

Run this experiment **only on a personal lab VM/workstation or explicitly approved test environment**.

Do not run it on production, shared school/work systems, or infrastructure you do not control.

The workload below:

- uses one Python process
- runs for about 8 seconds
- performs CPU work only
- stops automatically

If the machine is already overloaded, skip the experiment.

## Prerequisites

- D00-T005
- Python 3
- Linux shell

## 1. Record Baseline Capacity

~~~bash
nproc
free -h
uptime
~~~

If available:

~~~bash
lscpu | grep -E 'CPU\(s\)|Core|Thread|Model name'
~~~

Record:

~~~text
Logical CPU capacity:
Memory capacity:
Load average before:
~~~

## 2. Record Baseline Utilization

~~~bash
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head
~~~

If available:

~~~bash
vmstat 1 3
~~~

Do not interpret one number in isolation.

## 3. Start One Bounded CPU Worker

~~~bash
python3 - <<'PY' &
import time
end = time.time() + 8
x = 0
while time.time() < end:
    x = (x * 1664525 + 1013904223) & 0xffffffff
print(x)
PY

WORKER_PID=$!
echo "worker_pid=$WORKER_PID"
~~~

## 4. Observe the Worker

While it runs:

~~~bash
ps -p "$WORKER_PID" -o pid,stat,%cpu,%mem,etime,cmd
~~~

If the process finishes before you inspect it, repeat the experiment once.

Do not extend the duration or add multiple workers just to create a bigger number.

## 5. Observe System-Level Effect

While the bounded process runs, if available:

~~~bash
vmstat 1 5
~~~

Then:

~~~bash
uptime
~~~

## 6. Wait for Automatic Completion

~~~bash
wait "$WORKER_PID"
echo "exit_status=$?"
~~~

The process should stop on its own.

## 7. Capacity vs Utilization

Suppose the system exposes 8 logical CPUs and one process consumes roughly one CPU's worth of execution time.

The important lesson is not the exact percentage reported by a particular tool.

The lesson is:

~~~text
Capacity
≠
Current Utilization
≠
Saturation
≠
Headroom
~~~

Tools can report CPU percentages using different conventions.

## 8. Headroom Mental Model

Example only:

~~~text
Normal load consumes part of system capacity
          ↓
Unused capacity remains
          ↓
Traffic spike or failure occurs
          ↓
Remaining capacity absorbs additional work
~~~

If normal operation already consumes nearly all effective capacity, failover can cause saturation.

## 9. Failover Thought Experiment

Assume:

~~~text
Two application instances
Each handles ~45% of total traffic capacity
~~~

If one disappears:

~~~text
Remaining instance may need to handle ~90%
~~~

Now ask:

- Is there enough CPU?
- Is there enough memory?
- Is the database able to handle the same traffic?
- Are network/storage limits also sufficient?

Headroom must be evaluated across the dependency chain.

## 10. SRE Connection

Low utilization can still coexist with:

- high storage latency
- blocked I/O
- dependency waits
- connection exhaustion
- queue growth

High utilization can also be normal if latency and saturation remain controlled.

## 11. Architect Connection

Capacity planning asks:

~~~text
Normal demand
+ growth
+ spikes
+ failure reserve
+ maintenance reserve
=
required effective capacity
~~~

## Questions

1. What was the system's CPU capacity?
2. How did one bounded worker change utilization?
3. Did the experiment prove the system was saturated?
4. Why is headroom important during instance failure?
5. Why would CPU headroom alone be insufficient for an application with a database dependency?
6. Why should capacity planning use workload behavior rather than one utilization threshold?

## Validation Checklist

- [ ] Recorded CPU/memory capacity
- [ ] Recorded baseline utilization
- [ ] Ran only the bounded single-process workload
- [ ] Observed the worker
- [ ] Confirmed automatic completion
- [ ] Explained capacity vs utilization vs saturation
- [ ] Explained headroom and failover capacity

## Cleanup

No persistent resources are created.

If the process is still running unexpectedly:

~~~bash
kill "$WORKER_PID" 2>/dev/null || true
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after successful end-to-end execution on supported lab environments.

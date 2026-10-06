---
id: EXP-D00-005
domain: D00
topics:
  - D00-T004
level: L2-L3
type: experiment
status: draft
estimated_time: 45-60m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# EXP-D00-005 — Observe Synchronous Dependency Latency Propagation

## Objective

Demonstrate that a slow downstream dependency can make an upstream service slow even when the upstream service itself is healthy.

## Architecture

~~~text
Client
  ↓
Frontend API
  ↓ synchronous call
Dependency API
~~~

## Safety

Both services run locally. The dependency delay is deliberately bounded to one second.

## Prerequisites

- D00-T004
- Python 3
- curl

## 1. Create the Slow Dependency

~~~bash
mkdir -p /tmp/d00-t004-dependency
cd /tmp/d00-t004-dependency

cat > dependency.py <<'PY'
from http.server import BaseHTTPRequestHandler, HTTPServer
import time

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        time.sleep(1)
        body = b'{"dependency":"ok"}'
        self.send_response(200)
        self.send_header("Content-Type", "application/json")
        self.send_header("Content-Length", str(len(body)))
        self.end_headers()
        self.wfile.write(body)

HTTPServer(("127.0.0.1", 8101), Handler).serve_forever()
PY
~~~

Start:

~~~bash
python3 dependency.py
~~~

## 2. Create the Frontend API

In another terminal:

~~~bash
cd /tmp/d00-t004-dependency

cat > frontend.py <<'PY'
from http.server import BaseHTTPRequestHandler, HTTPServer
from urllib.request import urlopen
import time

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        start = time.time()

        with urlopen("http://127.0.0.1:8101/", timeout=3) as response:
            dependency_body = response.read()

        elapsed = time.time() - start
        body = (
            f'frontend=ok dependency_seconds={elapsed:.3f} '
            f'dependency_body={dependency_body.decode()}\n'
        ).encode()

        self.send_response(200)
        self.send_header("Content-Type", "text/plain")
        self.send_header("Content-Length", str(len(body)))
        self.end_headers()
        self.wfile.write(body)

HTTPServer(("127.0.0.1", 8100), Handler).serve_forever()
PY

python3 frontend.py
~~~

## 3. Measure End-to-End Latency

In a third terminal:

~~~bash
curl -s -o /dev/null -w 'total_seconds=%{time_total}\n' http://127.0.0.1:8100/
~~~

Run several times.

Expected observation:

The frontend request takes roughly as long as the downstream dependency delay, plus small local overhead.

Exact values vary.

## 4. Compare Direct Dependency Latency

~~~bash
curl -s -o /dev/null -w 'dependency_seconds=%{time_total}\n' http://127.0.0.1:8101/
~~~

Now compare:

~~~text
Dependency latency
vs
Frontend end-to-end latency
~~~

## 5. Architecture Meaning

The frontend process may have:

- low CPU
- normal memory
- no local failure

and still produce slow user responses because it is waiting synchronously.

~~~text
Dependency slow
    ↓
Frontend waits
    ↓
Request latency grows
    ↓
Users experience slowness
~~~

## Questions

1. Which service originated the delay?
2. Which service exposed the user-visible symptom?
3. Why would scaling the frontend not necessarily fix this?
4. What evidence would help prove the dependency is the bottleneck?
5. How could timeouts, async processing or caching change the architecture?
6. What risks would retries introduce if the dependency were already overloaded?

## Senior Engineer Connection

The component reporting high latency is not necessarily the root cause.

## SRE Connection

Distributed tracing and dependency latency metrics help explain where an SLI is being consumed.

## Architect Connection

Synchronous dependencies couple user latency to downstream response time.

## Validation Checklist

- [ ] Started dependency service
- [ ] Started frontend service
- [ ] Measured frontend latency
- [ ] Measured dependency latency
- [ ] Correlated the two
- [ ] Explained why upstream health metrics alone can mislead

## Cleanup

Stop both servers with Ctrl+C, then:

~~~bash
rm -rf /tmp/d00-t004-dependency
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution.

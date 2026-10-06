---
id: EXP-D00-004
domain: D00
topics:
  - D00-T004
level: L2
type: experiment
status: draft
estimated_time: 40-60m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# EXP-D00-004 — Local State vs Replaceable Instances

## Objective

Observe why local in-memory state makes interchangeable instances harder.

## Mental Model

~~~text
Stateless-style instance
→ any instance can handle a request

Local-state instance
→ future behavior may depend on which instance receives the request
~~~

## Safety

This experiment runs two small localhost servers only.

## Prerequisites

- D00-T004
- Python 3
- curl

## 1. Create the Demo Server

~~~bash
mkdir -p /tmp/d00-t004-state
cd /tmp/d00-t004-state

cat > counter.py <<'PY'
from http.server import BaseHTTPRequestHandler, HTTPServer
import os

PORT = int(os.environ["PORT"])
INSTANCE = os.environ["INSTANCE"]
counter = 0

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        global counter
        counter += 1
        body = f"instance={INSTANCE} local_counter={counter}\n".encode()
        self.send_response(200)
        self.send_header("Content-Type", "text/plain")
        self.send_header("Content-Length", str(len(body)))
        self.end_headers()
        self.wfile.write(body)

HTTPServer(("127.0.0.1", PORT), Handler).serve_forever()
PY
~~~

## 2. Start Two Instances

Terminal A:

~~~bash
PORT=8001 INSTANCE=A python3 counter.py
~~~

Terminal B:

~~~bash
PORT=8002 INSTANCE=B python3 counter.py
~~~

## 3. Alternate Requests

Terminal C:

~~~bash
curl -s http://127.0.0.1:8001/
curl -s http://127.0.0.1:8002/
curl -s http://127.0.0.1:8001/
curl -s http://127.0.0.1:8002/
~~~

Observe that each process maintains its own counter.

Example concept:

~~~text
Instance A → local_counter 1
Instance B → local_counter 1
Instance A → local_counter 2
Instance B → local_counter 2
~~~

## 4. Architecture Meaning

Imagine the counter represented:

- shopping cart state
- login session
- workflow progress

If a load balancer sends each request to any instance, local-only state can create inconsistent behavior.

## 5. Externalized-State Thought Experiment

A more horizontally scalable design might look like:

~~~text
           ┌→ Instance A ─┐
Client → LB               ├→ Shared State Store
           └→ Instance B ─┘
~~~

Both instances use the same external state source.

## Questions

1. Why are A and B not fully interchangeable in the demo?
2. What happens if Instance A disappears?
3. Why can externalizing session/state improve replaceability?
4. Does "stateless application instance" mean the whole system has no state?
5. What new dependency appears when state is externalized?

## Senior Engineer Connection

State placement affects:

- scaling
- failover
- deployment
- recovery
- debugging

## SRE Connection

Local-only state can turn instance replacement into user-visible impact.

## Architect Connection

Externalizing state improves replaceability but introduces a shared dependency whose availability and latency must be designed.

## Validation Checklist

- [ ] Started two instances
- [ ] Observed independent local state
- [ ] Explained why random routing can expose inconsistent state
- [ ] Explained the benefit and cost of external state

## Cleanup

Stop both servers with Ctrl+C, then:

~~~bash
rm -rf /tmp/d00-t004-state
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution.

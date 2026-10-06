---
id: OBS-D00-007
domain: D00
topics:
  - D00-T004
level: L1-L2
type: observation
status: draft
estimated_time: 35-50m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-007 — Trace a Request Through Client → API → Data

## Objective

Observe a complete local request path:

~~~text
Client
→ API
→ Data
→ API
→ Client
~~~

## Why This Matters

Architecture diagrams become useful only when you can connect each box and arrow to real behavior.

## Safety

This lab runs only on localhost and uses temporary files.

## Prerequisites

- D00-T001
- D00-T002
- D00-T003
- D00-T004
- Python 3
- curl

## 1. Create a Tiny API

~~~bash
mkdir -p /tmp/d00-t004-request-path
cd /tmp/d00-t004-request-path

cat > app.py <<'PY'
from http.server import BaseHTTPRequestHandler, HTTPServer
import json
import time

DATA = {
    "101": {"id": 101, "name": "Example Order", "status": "ready"}
}

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        start = time.time()

        if self.path.startswith("/orders/"):
            order_id = self.path.rsplit("/", 1)[-1]
            order = DATA.get(order_id)

            if order:
                body = json.dumps(order).encode()
                self.send_response(200)
            else:
                body = json.dumps({"error": "not found"}).encode()
                self.send_response(404)

            self.send_header("Content-Type", "application/json")
            self.send_header("Content-Length", str(len(body)))
            self.end_headers()
            self.wfile.write(body)

            elapsed = (time.time() - start) * 1000
            print(f"path={self.path} elapsed_ms={elapsed:.2f}")
            return

        body = b'{"error":"unknown route"}'
        self.send_response(404)
        self.send_header("Content-Type", "application/json")
        self.send_header("Content-Length", str(len(body)))
        self.end_headers()
        self.wfile.write(body)

HTTPServer(("127.0.0.1", 8000), Handler).serve_forever()
PY
~~~

Start it:

~~~bash
python3 app.py
~~~

Leave this terminal running.

## 2. Act as the Client

In another terminal:

~~~bash
curl -i http://127.0.0.1:8000/orders/101
~~~

Observe:

- request path
- HTTP status
- response headers
- JSON body
- API-side log

## 3. Follow the Request

Map what happened:

~~~text
curl client
   ↓
TCP/HTTP request
   ↓
Python API process
   ↓
route lookup
   ↓
in-memory data lookup
   ↓
JSON response
   ↓
client
~~~

## 4. Trigger a Not-Found Response

~~~bash
curl -i http://127.0.0.1:8000/orders/999
~~~

Compare the request with the first one.

## 5. Inspect the Listening Process

~~~bash
ss -ltnp | grep ':8000'
~~~

Then find the process:

~~~bash
pgrep -af "python3 app.py"
~~~

## Questions

1. Which component acted as the client?
2. Which component acted as the server?
3. What was the API contract for the request?
4. Where was the data stored in this lab?
5. What would change if the data were in a remote database?
6. Where could latency be introduced?

## Validation Checklist

- [ ] Started the API
- [ ] Sent a successful request
- [ ] Observed request/response headers and body
- [ ] Triggered a 404 response
- [ ] Identified the listening process/port
- [ ] Drew the end-to-end request path

## Troubleshooting Connection

When a user says "the API is slow," think in stages:

~~~text
Client
→ Network
→ Listener
→ Application Logic
→ Data Dependency
→ Response
~~~

## Cleanup

Stop the server with Ctrl+C, then:

~~~bash
rm -rf /tmp/d00-t004-request-path
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution on supported environments.

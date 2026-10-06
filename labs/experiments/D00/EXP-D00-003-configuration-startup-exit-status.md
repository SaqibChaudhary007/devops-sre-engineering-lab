---
id: EXP-D00-003
domain: D00
topics:
  - D00-T003
level: L2-L3
type: experiment
status: draft
estimated_time: 40-60m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# EXP-D00-003 — Configuration, Startup Failure and Exit Status

## Objective

Demonstrate that an application can have valid source code and still fail because required runtime configuration is missing.

~~~text
Valid Source
+ Runtime
+ Missing Configuration
=
Startup Failure
~~~

## Safety

This experiment uses only a temporary local Python script and environment variable.

## Prerequisites

- D00-T003
- Python 3
- Linux shell

## 1. Create the Application

~~~bash
mkdir -p /tmp/d00-t003-config
cd /tmp/d00-t003-config

cat > app.py <<'PY'
import os
import sys

greeting = os.getenv("DEMO_GREETING")

if not greeting:
    print("ERROR: DEMO_GREETING is required", file=sys.stderr)
    sys.exit(2)

print(greeting)
sys.exit(0)
PY
~~~

## 2. Run Without Required Configuration

~~~bash
unset DEMO_GREETING
python3 app.py
STATUS=$?
echo "exit_status=$STATUS"
~~~

Expected behavior:

- the program starts through Python
- startup validation fails
- the process exits nonzero
- no source-code change was required to create the failure

## 3. Supply Configuration

~~~bash
export DEMO_GREETING="Hello from configured runtime"
python3 app.py
STATUS=$?
echo "exit_status=$STATUS"
~~~

Expected result:

~~~text
Hello from configured runtime
exit_status=0
~~~

## 4. Prove Source Did Not Change

Before and after configuration changes:

~~~bash
sha256sum app.py
~~~

The source hash should remain unchanged unless the file itself was modified.

### Mental Model

~~~text
Same Source
Same Runtime
Different Configuration
        ↓
Different Runtime Result
~~~

## 5. Classify the Failure

Was the first failure:

- build failure?
- startup failure?
- runtime/operational failure?

For this exercise, treat it as a **startup/configuration failure** because the application cannot complete initialization successfully without required configuration.

## 6. Production Reasoning

Imagine production logs:

~~~text
ERROR: DATABASE_URL is required
~~~

Weak response:

> Rebuild the application.

Better first reasoning:

~~~text
What configuration is required?
Is it present?
Is the correct environment using it?
Did configuration change?
Is the secret/config source available?
~~~

## 7. Artifact Identity Connection

Run:

~~~bash
sha256sum app.py
python3 --version
~~~

Record:

~~~text
Source hash:
Python runtime version:
Configuration value present? yes/no
Exit status:
~~~

This demonstrates that application identity is more than source alone.

## Questions

1. Why did the first run fail even though the source file was valid?
2. Why did the second run succeed without rebuilding anything?
3. How is configuration different from code?
4. Why should deployment systems record artifact/runtime/configuration identity?
5. Why is a nonzero exit status useful to CI/CD and service managers?

## Senior Engineer Connection

Before rebuilding or redeploying, determine the failure stage:

~~~text
Build
Startup
Runtime
Dependency
Configuration
~~~

## SRE Connection

Clear startup errors and exit statuses reduce time to detection and recovery.

## Architect Connection

Configuration design affects portability, security, deployment consistency and operational complexity.

## Validation Checklist

- [ ] Created a valid source file
- [ ] Produced a controlled startup/configuration failure
- [ ] Observed nonzero exit status
- [ ] Corrected configuration without modifying code
- [ ] Observed successful exit status
- [ ] Demonstrated unchanged source identity

## Cleanup

~~~bash
unset DEMO_GREETING
rm -rf /tmp/d00-t003-config
~~~

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution.

# D00-T003 — Applied Scenario

## Scenario

A team reports:

> "The application passed CI, but the new release fails immediately in production."

Known facts:

~~~text
Source commit:       unchanged since successful QA
CI build:            passed
Unit tests:          passed
Artifact version:    app-2.4.1
QA environment:      healthy
Production deploy:   process exits immediately
Production log:      "ERROR: DATABASE_URL is required"
CPU/memory:          normal
Previous version:    app-2.4.0
~~~

## Task 1 — Classify the Failure

Answer:

1. Is this primarily a build failure, startup failure or runtime failure?
2. What evidence supports your classification?
3. What evidence tells you the artifact was successfully created?

## Task 2 — Form Hypotheses

List your top four hypotheses.

Consider:

- missing configuration
- incorrect environment variable
- secret/config source failure
- deployment manifest difference
- version mismatch
- artifact mismatch

For each hypothesis, state:

- why it is plausible
- what evidence supports it
- what evidence you would collect next

## Task 3 — Avoid Weak Responses

Explain why these responses are weak:

- "Rebuild the application."
- "CPU and memory are normal, so production is healthy."
- "The code must be broken."
- "Just roll back without collecting any evidence."

## Task 4 — Source vs Artifact Reasoning

Suppose QA and production are both intended to run artifact `app-2.4.1`.

What evidence would you collect to confirm they are actually running the same artifact?

Consider:

- artifact checksum
- image digest
- package version
- Git commit/build metadata
- deployment record

## Task 5 — Configuration Reasoning

What would you inspect to determine why `DATABASE_URL` is missing?

Examples:

- deployment configuration
- secret/config injection
- environment variables
- environment-specific values
- access permissions
- naming mistakes
- recent configuration changes

## Task 6 — Senior Engineer Response

Write a troubleshooting sequence using:

~~~text
Impact
→ Failure Stage
→ Exact Version
→ Artifact Identity
→ Configuration
→ Runtime Dependencies
→ Evidence
→ Safe Mitigation
→ Root Cause
→ Prevention
~~~

## Task 7 — SRE View

Answer:

1. How can artifact/version identity reduce incident recovery time?
2. Why is a startup failure a reliability problem even if infrastructure metrics look normal?
3. Which deployment/release signals would help detect this quickly?
4. What should be observable about release identity in production?

## Task 8 — Architect View

Suppose this type of incident happens repeatedly across environments.

What design/process improvements would you evaluate?

Consider:

- build-once/promote
- immutable artifacts
- configuration contracts
- schema/validation for required config
- startup validation
- secret/config delivery
- environment parity
- automated pre-deploy checks
- release metadata
- rollback strategy

## Success Standard

A strong answer identifies this as a startup/configuration problem, confirms artifact identity before blaming source code, requests targeted evidence and proposes prevention through stronger configuration and release discipline.

# D00 Sources & Evidence

D00 follows the repository-wide [Sources & Evidence Model](../../docs/sources/README.md).

## Evidence Tags

- `[S]` Standard / Specification
- `[D]` Official Documentation
- `[A]` Authoritative Engineering Reference
- `[R]` Reputable Reference
- `[L]` Lab Verified
- `[P]` Sanitized Production Pattern
- `[I-R]` Reported Interview Question
- `[I-P]` Practice Interview Question
- `[I-PS]` Production-Scenario Interview Question
- `[C]` Community Source
- `[AI-DRAFT]` AI-assisted, not yet verified

## Domain 00 Source Strategy

Prefer standards and official documentation for factual behavior, authoritative engineering literature for mental models, labs for reproducible behavior, and anonymized production patterns for operational context.

AI output is never treated as technical authority.

## Topic Verification Records

- [D00-T003 — Software Engineering Foundations](../../docs/sources/D00/D00-T003-source-verification.md) — core claims DOC-VERIFIED

- [D00-T004 — Application Architecture Fundamentals](../../docs/sources/D00/D00-T004-source-verification.md) — core claims DOC-VERIFIED

- [D00-T005 — Infrastructure Foundations](../../docs/sources/D00/D00-T005-source-verification.md) — core claims DOC-VERIFIED

- [D00-T006 — Cloud Mental Models](../../docs/sources/D00/D00-T006-source-verification.md) — core claims DOC-VERIFIED

- [D00-T007 — DevOps Foundations](../../docs/sources/D00/D00-T007-source-verification.md) — core claims DOC-VERIFIED; DORA metrics updated to current five-metric model

- [D00-T008 — Infrastructure as Code Mental Model](../../docs/sources/D00/D00-T008-source-verification.md) — core claims DOC-VERIFIED; state, locking, idempotence, plan, drift, import, and GitOps nuances verified

- [D00-T009 — CI/CD Mental Model](../../docs/sources/D00/D00-T009-source-verification.md) — core claims DOC-VERIFIED; CI/CD definitions, build-once/promote, artifacts, runners, concurrency, environment controls, credentials, provenance, and GitOps boundaries verified

- [D00-T010 — Containers & Orchestration Mental Model](../../docs/sources/D00/D00-T010-source-verification.md) — core claims DOC-VERIFIED; OCI image/runtime model, layers, runtime/host boundaries, cgroups, storage, Kubernetes reconciliation, scheduling, health, self-healing, and stateful/stateless nuances verified

- [D00-T011 — Distributed Systems Foundations](../../docs/sources/D00/D00-T011-source-verification.md) — core claims DOC-VERIFIED; partial failure, ambiguous timeout, retries/backoff/jitter, duplicate handling, delivery semantics, CAP, circuit breaker/bulkhead, queues/backpressure, failure domains, and cascading-failure nuances verified

- [D00-T012 — Reliability Engineering Foundations](../../docs/sources/D00/D00-T012-source-verification.md) — core claims DOC-VERIFIED; user-centered reliability, SLI/SLO/SLA, error budgets, recovery targets, redundancy/independence, graceful degradation, change risk, observability, capacity headroom, and tested recovery nuances verified

- [D00-T013 — SRE Foundations](../../docs/sources/D00/D00-T013-source-verification.md) — core claims DOC-VERIFIED; SRE operating model, SLI/SLO/SLA, error budgets, toil, paging/on-call, incident learning, release engineering, progressive delivery, capacity, and production-readiness nuances verified

- [D00-T014 — Observability Foundations](../../docs/sources/D00/D00-T014-source-verification.md) — core claims DOC-VERIFIED; observability/monitoring boundaries, telemetry/instrumentation, cross-signal correlation, trace context, structured telemetry, cardinality, latency distributions, sampling/retention, security, cost, dashboards, and alerting nuances verified

- [D00-T015 — Security Foundations](../../docs/sources/D00/D00-T015-source-verification.md) — core claims DOC-VERIFIED; security-risk framing, Zero Trust, authentication/authorization, least privilege, secrets lifecycle, secure defaults, cryptographic boundaries, CI/CD trust, supply-chain provenance, cloud shared responsibility, and security/reliability nuances verified

- [D00-T016 — Automation Mental Models](../../docs/sources/D00/D00-T016-source-verification.md) — core claims DOC-VERIFIED; automation value, toil reduction, desired/current state, reconciliation, idempotency, retry/backoff/jitter/timeout safety, partial failure, approval boundaries, guardrails, identity, observability, and bounded remediation nuances verified

- [D00-T017 — Systems Thinking](../../docs/sources/D00/D00-T017-source-verification.md) — core claims DOC-VERIFIED; system boundaries, relationships, emergent behavior, stocks/flows, feedback loops, delays, local-vs-global optimization, retries, backpressure, autoscaling, cascading failure, common-mode dependencies, and second-order effects verified

- [D00-T018 — Failure Thinking](../../docs/sources/D00/D00-T018-source-verification.md) — core claims DOC-VERIFIED; failure-mode analysis, blast radius, cascading failure, overload, retry amplification, graceful degradation, fault isolation, backup/restore, RTO/RPO, partition/quorum preview, recovery validation, game days, and chaos-testing boundaries verified

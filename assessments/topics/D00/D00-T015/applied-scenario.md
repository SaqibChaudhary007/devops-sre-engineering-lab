# D00-T015 — Applied Security Scenario

## Scenario

A customer-facing application uses:

~~~text
Customer
→ Public API
→ Application Service
→ Database
→ Queue
→ Worker
~~~

Its delivery path is:

~~~text
Developer
→ Source Repository
→ CI/CD Runner
→ Artifact Registry
→ Deployment Pipeline
→ Production
~~~

Current operating model:

~~~text
- all developers share one administrator account
- CI/CD uses a long-lived static credential
- application and worker use the same database credential
- database password is committed in configuration
- production and backup deletion use the same identity
- artifact promotion has no verification step
- pipeline can deploy to all environments
- audit logging is incomplete
- emergency access never expires
- dependency ownership is unclear
- cloud service is assumed to be "secure because managed"
~~~

A security review must be performed before a major release.

## Task 1 — Identify Assets

Identify the highest-value assets, including:

- customer data
- identities
- source
- deployment credentials
- artifacts
- production configuration
- backups
- audit evidence
- service availability

Explain why each matters.

## Task 2 — Map Trust Boundaries

Map key trust boundaries across:

- Internet → API
- developer → source repository
- CI/CD → registry
- deployment pipeline → production
- application → database
- production → backup system

Explain what security decision is required at each boundary.

## Task 3 — Threat / Weakness / Risk

For each of these conditions:

- shared administrator account
- hard-coded database password
- broad CI/CD credential
- unverified artifact
- same identity for production and backup deletion
- permanent emergency access

describe:

~~~text
Asset
Threat
Weakness
Exposure
Impact
Risk
~~~

Do not describe exploitation techniques.

## Task 4 — Identity Model

Redesign identities for:

- developer
- administrator
- CI/CD pipeline
- application
- worker
- backup operator/process

Explain why human and workload identities should be separate.

## Task 5 — Authentication vs Authorization

For each identity, define:

~~~text
Authentication
→ how identity is established

Authorization
→ what resource/action is allowed
~~~

Explain why strong authentication does not justify broad access.

## Task 6 — Least Privilege

Build a conceptual matrix:

~~~text
Identity
Resource
Action
Scope
Duration
Approval
Audit
~~~

Identify permissions that should be narrowed.

## Task 7 — Emergency Access

Replace permanent emergency access with:

~~~text
Need
→ Approval
→ Temporary Grant
→ Audit
→ Expiry / Revocation
~~~

Explain how this supports both security and reliability.

## Task 8 — Secrets Lifecycle

For the database credential, design:

~~~text
Create
→ Store
→ Distribute
→ Use
→ Rotate
→ Revoke
→ Audit
~~~

Explain why committing the secret to source is weak design.

## Task 9 — Short-Lived Credentials

Compare the current long-lived CI/CD credential with a short-lived scoped credential.

Discuss:

- exposure window
- scope
- issuance
- monitoring
- revocation
- operational complexity

Explain why short-lived is not automatically safe.

## Task 10 — Audit and Detection

Define the events that should be recorded for:

- authentication
- authorization failure
- privilege change
- secret access
- pipeline approval
- artifact promotion
- deployment
- backup delete/restore

Explain why preventive controls are incomplete without detective evidence.

## Task 11 — Artifact and Supply-Chain Trust

Design a safe conceptual flow:

~~~text
Source
→ Reviewed Build
→ Artifact Identity
→ Provenance Evidence
→ Controlled Promotion
→ Verification
→ Deployment
~~~

Explain why provenance alone does not prove trust.

## Task 12 — CI/CD Security

Review:

- pipeline identity
- environment permissions
- secret access
- review gates
- artifact publishing
- auditability

Explain why CI/CD is a production-grade security boundary.

## Task 13 — Shared Responsibility

For the managed cloud service, explain:

- what the provider may operate
- what the customer still owns
- why identities/data/configuration remain important customer responsibilities

Do not assume one shared-responsibility boundary fits all services.

## Task 14 — Defense in Depth and Blast Radius

Design complementary controls such as:

- identity
- least privilege
- environment separation
- secret separation
- artifact verification
- audit
- monitoring
- backup isolation

Explain what happens if one control fails.

## Task 15 — Security vs Reliability Trade-Off

Reason through:

- emergency access vs least privilege
- urgent patching vs change risk
- aggressive blocking vs availability
- segmentation vs recovery access

Use balanced operating principles rather than absolute rules.

## Task 16 — Production Readiness

Score:

~~~text
Ready
Partially Ready
Not Ready
~~~

for:

- assets identified
- data classified
- trust boundaries mapped
- human/workload identity separated
- least privilege reviewed
- secret lifecycle defined
- audit logging ready
- pipeline permissions scoped
- artifact verification defined
- dependency ownership defined
- backup access separated
- incident/recovery ownership clear

## Task 17 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Asset
→ Threat
→ Trust Boundary
→ Identity
→ Permission
→ Control
→ Evidence
→ Risk Reduction
~~~

### SRE

Connect:

- security monitoring
- emergency access
- blast radius
- auditability
- recovery trust
- operational ownership

### Architect

Redesign:

- identity boundaries
- CI/CD trust
- environment separation
- backup security
- artifact trust
- security/reliability trade-offs
- launch-readiness gates

## Success Standard

A strong answer should explicitly reject:

- authentication = authorization
- shared admin identity = acceptable convenience
- short-lived credential = automatically safe
- secrets = normal config
- encryption = complete security
- provenance = automatic trust
- managed cloud service = no customer security responsibility
- prevention = no need for detection/response

---
id: EXP-D00-007
domain: D00
topics:
  - D00-T006
level: L2-L3
type: experiment
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - No cloud account required
evidence_status:
  - DRAFT
---

# EXP-D00-007 — Compare IaaS, PaaS, SaaS, and Serverless Responsibility Boundaries

## Objective

Model how operational responsibility shifts as the abstraction level increases.

## Safety

This is a provider-neutral local exercise.

No cloud account, deployment, credentials, or paid service is required.

## 1. Start with the Responsibility Stack

Use these layers:

~~~text
Physical Facility
Physical Hardware
Virtualization
Operating System
Runtime / Middleware
Application
Data
Identity / Access
Configuration
Monitoring
Backup / Recovery
~~~

## 2. Build Four Models

Create four columns:

~~~text
IaaS
PaaS
SaaS
Serverless
~~~

For each layer, mark:

~~~text
Provider
Customer
Shared / Depends
~~~

## 3. IaaS Mental Model

Typical customer responsibility includes more of:

- guest OS
- middleware/runtime
- application
- data
- workload configuration
- identity configuration

Provider operates more of the physical/platform foundation.

Do not treat this as universal for every service.

## 4. PaaS Mental Model

The provider operates more runtime/platform layers.

The customer focuses more on:

- application
- data
- configuration
- identity
- application observability

## 5. SaaS Mental Model

The provider operates most technology layers.

The customer still owns or influences:

- user access
- data usage
- configuration
- integration
- governance
- business process

## 6. Serverless Mental Model

The provider abstracts more server lifecycle and scaling.

The customer still owns:

- code
- permissions
- dependencies
- configuration
- data handling
- cost behavior
- observability

## 7. Scenario Classification

Classify each statement:

1. "We must patch the guest OS."
2. "The provider patches the runtime."
3. "We configure user roles in the application."
4. "We must secure application secrets."
5. "The provider replaces failed physical hosts."
6. "We define function permissions."
7. "We decide data retention."
8. "We configure backup policy for our workload."

For each, write:

~~~text
Likely customer?
Likely provider?
Shared?
Depends on service?
~~~

## 8. Failure Scenario

Suppose a managed database is unavailable.

Ask:

- what does the provider own?
- what does the customer still own?
- who owns application retry behavior?
- who owns schema design?
- who owns access policy?
- who owns recovery requirements?

## 9. Security Connection

Managed service does not mean:

~~~text
No customer security responsibility
~~~

Identity, data, access, configuration, and application behavior still matter.

## 10. Architect Connection

Choosing a higher-level managed service trades:

~~~text
More abstraction / less operational work
for
Less low-level control / different cost and portability constraints
~~~

## Validation Checklist

- [ ] Built responsibility maps for all four service models
- [ ] Identified at least five responsibilities that remain with the customer in managed services
- [ ] Explained why responsibility boundaries depend on service type
- [ ] Explained why "managed = provider handles everything" is false
- [ ] Connected abstraction level to operational burden and control

## Teach-Back

Explain:

> "The more managed the service, the more responsibility shifts—but responsibility never disappears."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.

# D00-T007 Source Verification — DevOps Foundations

## Verification Goal

Verify the core claims in **00.07 — DevOps Foundations** against current DORA guidance, official CI/CD guidance, Google SRE material, CNCF platform-engineering guidance, and OWASP DevSecOps guidance.

## Verification Status

**Result:** Core claims verified with one important modernization.

**Evidence level:** E2 — supported by current research/program guidance and authoritative engineering references.

### Important 2026 Update

The historical four DORA delivery metrics have evolved.

Current DORA guidance uses **five software delivery performance metrics**:

### Throughput

- Change lead time
- Deployment frequency
- Failed deployment recovery time

### Instability

- Change fail rate
- Deployment rework rate

Therefore D00-T007 retains the historical four-key context for learner continuity but teaches the **current five-metric model** as the canonical 2026 view.

---

# Verified Claim Map

| Topic claim | Verification | Primary source |
|---|---|---|
| Delivery performance should be measured as a system rather than one activity | Verified | DORA |
| Smaller changes can improve both throughput and stability | Verified | DORA |
| Deployment frequency and change lead time are delivery-performance metrics | Verified | DORA |
| Historical MTTR/time-to-restore evolved into failed deployment recovery time | Verified | DORA 2026 metric history |
| Deployment rework rate is now the fifth DORA metric | Verified | DORA 2026 |
| CI/CD automates the software release lifecycle | Verified | AWS Prescriptive Guidance |
| Continuous delivery and continuous deployment differ at production promotion | Verified | AWS Prescriptive Guidance |
| Toil is manual/repetitive/automatable/tactical work with little enduring value | Verified | Google SRE |
| Blameless postmortems focus learning on systems/processes rather than personal blame | Verified | Google SRE |
| SRE and DevOps overlap; SRE can be treated as a concrete implementation of DevOps principles | Verified | Google SRE |
| Platform engineering can scale DevOps principles through internal platforms/self-service | Verified | CNCF TAG App Delivery |
| Shift-left security moves useful security checks earlier in the lifecycle | Verified | OWASP DevSecOps Guideline |

---

# Primary / Authoritative Sources

## 1. DORA — Software Delivery Performance Metrics

- https://dora.dev/guides/dora-metrics/
- https://dora.dev/insights/dora-metrics-history/
- https://dora.dev/insights/quickcheck-updates/

Supports:

- change lead time
- deployment frequency
- failed deployment recovery time
- change fail rate
- deployment rework rate
- throughput vs instability framing
- small-batch improvement guidance
- service/application-level measurement
- warning against optimizing a single metric

### Important correction

Historically, DORA used:

- deployment frequency
- lead time for changes
- change fail rate
- mean time to recover / time to restore service

Current DORA material explains that the recovery metric was renamed/redefined as **failed deployment recovery time**, and a fifth metric, **deployment rework rate**, was added.

The curriculum should therefore not present the older four metrics as the complete current model.

---

# 2. AWS — CI/CD Definitions

- https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-cicd-litmus/understanding-cicd.html

Supports:

- CI/CD as automation across the software release lifecycle
- source/build/test/staging/production pipeline stages
- continuous delivery vs continuous deployment distinction
- continuous delivery retaining an explicit production promotion decision
- continuous deployment allowing successful changes to flow through to production automatically

### Important nuance

A pipeline tool alone does not establish CI/CD maturity.

The engineering outcome depends on:

- integration frequency
- validation quality
- feedback speed
- reproducibility
- release safety
- recovery

---

# 3. Google SRE — Toil

- https://sre.google/sre-book/eliminating-toil/
- https://sre.google/workbook/eliminating-toil/

Supports the toil characteristics used in D00-T007:

- manual
- repetitive
- automatable
- tactical
- low/no enduring value
- tends to scale with service growth

### Important nuance

Not every manual task is toil.

Work requiring meaningful judgment or producing durable system improvement may not be toil.

---

# 4. Google SRE — Blameless Incident Learning

- https://sre.google/resources/practices-and-processes/incident-management-guide/
- https://sre.google/sre-book/postmortem-culture/
- https://sre.google/workbook/postmortem-culture/

Supports:

- learning from incidents
- blameless postmortems
- improving systems, procedures, training, detection, mitigation, and communication
- creating concrete follow-up actions

### Important nuance

Blameless does not mean absence of accountability.

It means the analysis should not stop at:

> "A person made a mistake."

The objective is durable system improvement.

---

# 5. Google SRE — DevOps vs SRE

- https://sre.google/workbook/how-sre-relates/
- https://sre.google/sre-book/introduction/
- https://cloud.google.com/blog/products/devops-sre/supercharge-your-devops-practice-with-sre-principles

Supports:

- DevOps as a broad set of principles/practices around lifecycle collaboration
- SRE as a more concrete reliability-focused discipline
- significant overlap between DevOps and SRE
- the useful mental model that SRE can implement DevOps objectives

### Important nuance

Do not teach:

> DevOps = SRE

or:

> SRE replaces DevOps

They overlap but are not identical.

---

# 6. CNCF — Platform Engineering

- https://glossary.cncf.io/platform-engineering/
- https://tag-app-delivery.cncf.io/wgs/platforms/glossary/
- https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/

Supports:

- platform engineering as building tools/processes/platform capabilities that empower developers
- self-service and reduced infrastructure complexity
- platform engineering as a way to scale DevOps principles
- platform teams treating developers/internal users as platform customers

### Important nuance

Platform engineering does not remove the need for:

- shared ownership
- production feedback
- team collaboration
- reliability responsibility

---

# 7. OWASP — Security in the Delivery Lifecycle

- https://owasp.org/projects/devsecops-guideline

Supports:

- security controls integrated into software delivery
- shift-left security culture
- identifying design flaws/vulnerabilities earlier
- continued security detection through the lifecycle

### Important nuance

Shift left should not mean:

> security happens only before production.

Runtime/production learning remains necessary.

---

# Verified Nuances / Corrections

## 1. DORA Is Now Five Metrics, Not Four

As of 2026, the current model is:

~~~text
Throughput
├── Change Lead Time
├── Deployment Frequency
└── Failed Deployment Recovery Time

Instability
├── Change Fail Rate
└── Deployment Rework Rate
~~~

Historical four-key terminology remains useful background, but should be labeled historical.

## 2. Recovery Metric Terminology Changed

The former MTTR/time-to-restore framing could include failures unrelated to deployments.

Current DORA uses **failed deployment recovery time** to focus specifically on recovery from failed production changes.

## 3. Speed and Stability Are Not Automatically Opposed

Current DORA guidance states that strong teams can perform well across both throughput and stability/instability dimensions.

Do not teach:

> faster delivery necessarily means lower reliability.

## 4. Metrics Are Signals, Not Targets to Game

DORA explicitly warns against turning one metric into a universal target.

Metrics should support continuous improvement for a specific application/service.

## 5. CI/CD Is More Than a Pipeline Product

Installing Jenkins, GitHub Actions, GitLab, or another tool does not itself produce continuous integration or continuous delivery.

The practices are defined by engineering behavior and outcomes.

## 6. Toil Is Not "Work I Dislike"

Manual or repetitive work only becomes toil when it has the relevant operational characteristics such as automatable, tactical, repetitive, and low enduring value.

## 7. Blameless Does Not Mean Consequence-Free

The goal is to improve systems and conditions instead of stopping analysis at individual blame.

## 8. SRE Can Implement DevOps Principles

This is a useful relationship model, not an identity equation.

## 9. Platform Engineering Can Scale DevOps

Platform engineering can provide reusable self-service/paved-road capabilities that make good delivery practices easier across many teams.

## 10. Shift Left and Shift Right Are Complementary

Earlier validation reduces preventable defects.

Production/runtime feedback reveals behavior that pre-production environments cannot fully reproduce.

---

# Evidence Decision

The following D00-T007 areas are now eligible for **DOC-VERIFIED** status:

- flow / delivery-system framing
- DORA software delivery performance metrics
- small-batch improvement framing
- CI/CD definitions
- continuous delivery vs continuous deployment distinction
- toil definition
- blameless incident learning
- DevOps vs SRE relationship
- DevOps vs platform engineering relationship
- security integration / shift-left framing

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require hands-on or structured exercises:

- map one feature from idea to production and feedback
- identify queues, WIP, handoffs, and bottlenecks
- compare one large batch with multiple smaller changes
- design a delivery feedback loop
- classify toil vs judgment work
- calculate/currently interpret delivery-performance metrics
- identify misleading metric optimization

These become the D00-T007 practical package.

# D00 Production / Senior / SRE / Architect Scenarios

## Maturity Lens

```text
Production Operator
→ Senior Engineer
→ SRE
→ Architect
```

Every major scenario should ask:

- What happened?
- Who is affected?
- What is the scope?
- What evidence exists?
- What is the safest mitigation?
- What is the root cause?
- How can recurrence be reduced?
- What reliability issue does this expose?
- Should the architecture change?
- What trade-off does that introduce?

## Scenario Families

D00 introduces availability, performance, capacity, configuration, change, dependency, state, security, observability, reliability and architecture scenarios.

Cross-level examples include application latency, dependency failure, traffic spike, single-instance failure, stateful-session failure, alert without user impact, user impact without alert, automation blast radius, name-resolution failure, expired credential, resource exhaustion and third-party degradation.

Full scenario assets live under [Scenarios](../../scenarios/README.md).

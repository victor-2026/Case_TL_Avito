# TDR — Tech Design Review

**Source:** [Avito Playbook](https://github.com/avito-tech/playbook/blob/master/tech_design_review.md)

TDR is Avito's standard format for any design decision. The Test Strategy solution (page 05) follows this format.

## Lifecycle

```
Problem → TDR Dashboard → Design Document → Review → Feedback → Refine → Implement
```

## Template

| Section | What it contains |
|---------|-----------------|
| **Problem** | Business/product problem being solved |
| **Description** | Proposed solution and how it addresses the problem |
| **Dependency Diagram** | Architecture — components and their relationships |
| **Trade-offs** | Compromises made, planned tech debt, when it will be resolved |
| **Alternatives** | Other approaches considered and why they were rejected |
| **FAQ** | Questions raised during design and answers |
| **Load** | RPM, replicas per DC, read/write ratio |
| **Resources** | Similar services, DB config, storage, GPU, specific needs |
| **Database Structure** | Schema design and storage approach |
| **Information Security** | Public API, personal data, threat model |
| **Metrics** | Business, product, technical metrics to measure success |

## Why TDR for Test Strategy

TDR is how Avito engineers communicate design decisions. Presenting the testing strategy in TDR format demonstrates:

1. **You know Avito's internal processes**
2. **You think like an Avito engineer** — structured, data-driven, risk-aware
3. **Your solution fits their culture** — not a generic test plan, but a design document
4. **You speak their language** — TDR, Unit, Cluster, E5, Zero Bug Policy, QS

## Adaptation for QA

In the [Test Strategy](05-test-strategy.md) page, each TDR section is adapted for quality:

| TDR Section | QA Adaptation |
|-------------|---------------|
| Problem | Quality problem being solved (financial risk, DS coverage, etc.) |
| Description | Testing architecture + governance model |
| Dependency Diagram | Components under test, test layers, CI/CD flow |
| Trade-offs | What won't be tested initially, tech debt in test automation |
| Alternatives | Why not just more manual QA / single E2E suite |
| Load | Test execution frequency, parallelism, CI capacity |
| Resources | Environments, test data, tools |
| Metrics | DORA, QS, coverage, defect leakage |

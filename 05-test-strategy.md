# TDR: Testing Strategy for MNZ Cluster

**Author:** Victor — Test Lead candidate
**Role:** Test Lead (MNZ) — E5+
**Cluster:** MNZ (Monetization + Ads + FinTech)

---

## Problem

### Business Problem

MNZ cluster generates Avito's core revenue through ad promotion, professional plans, auction mechanics, and CPL/CPA instruments. Financial risk is high — a single undetected bug in pricing, auction, or payment flow causes direct revenue loss and seller churn.

### Quality Problem

Current state:
- QA embedded in product units (E3–E4), reporting to Unit-Leaders
- No cluster-level quality governance — each unit tests in isolation
- DS/ML algorithms (auction efficiency, inventory efficiency, liquidity distribution) not covered by quality process
- Cross-unit integrations (e.g., payment → listing promotion → auction) have no end-to-end testing
- Metrics are unit-local — no cluster-wide quality visibility
- Zero Bug Policy and SLO enforced per unit, not per cluster

### Risks

| Risk | Impact | Current Coverage |
|------|--------|-----------------|
| Pricing bug in MNZ | Revenue loss, seller complaints | Unit tests only |
| ML regression in auction | Suboptimal ranking → lower liquidity | No QA coverage |
| Integration failure (Payment → Promotion) | Users pay but get no benefit | No E2E tests |
| Flaky release | CFR increases, MTTR blows up | No cluster-level quality gates |
| Crash in seller onboarding | Churn increase | Mobile QA in unit only |

---

## Description

### Solution Overview

A **three-layer testing architecture** with a **quality governance model** for the MNZ cluster.

### Layer 1 — Unit (existing, needs improvement)

Each product unit owns its testing:

| Activity | Owner | Tools |
|----------|-------|-------|
| Unit tests (Go) | Developers | Go testing, table-driven tests |
| API contract tests | QA (E3–E4) | Contract testing per service |
| UI regression | QA (E4) | Playwright, per-unit POMs |
| DS model validation | DS engineers | Precision/Recall, AUC, A/B tests |

**Improvement needed:** Add mutation testing requirement for critical services (payment, pricing, auction).

### Layer 2 — Cluster (NEW — Test Lead owns this)

Cross-unit quality coordination:

| Activity | Description | Frequency |
|----------|-------------|-----------|
| **Cross-unit integration tests** | End-to-end flows: payment → promotion → auction → listing | Every release |
| **DS quality audit** | Non-deterministic testing of ML models: property-based, drift detection, A/B validation | Weekly |
| **Release quality gates** | Pre-release checks: CFR trend, QS score, mutation pass rate | Per release train |
| **Cluster metrics dashboard** | DORA + QS + business metrics across all MNZ units | Real-time |
| **Incident RCA** | Cluster-level incident analysis — prevent recurrence across units | Per incident |
| **Risk map** | Risk register for the entire cluster — updated quarterly | Quarterly |

### Layer 3 — Platform (company-wide, collaborate)

Work with Tech Platform → Quality team:

| Activity | Collaboration |
|----------|--------------|
| Shared test infrastructure | Contribute to Resource Manager, test data factories |
| Performance testing | Engage platform team for load testing critical MNZ services |
| Security testing | Coordinate with security team for payment/personal data flows |
| Tooling improvements | Propose cluster-level needs to platform team |

### Governance Model

```
Test Lead (MNZ)
  ├── QA Unit A (E4) — reports functionally to Test Lead, administratively to Unit-Leader
  ├── QA Unit B (E4)
  ├── QA Unit C (E4)
  └── QA Unit D (E3+)
```

**Key principle:** QA engineers have a **solid line to Test Lead** for quality standards and a **dotted line to Unit-Leader** for daily work. This prevents the current problem of quality being a secondary concern.

### Zero Bug Policy Implementation

Per Avito's ZBP principle, every bug gets an immediate decision:

| Decision | Criteria |
|----------|----------|
| **Fix now** | Blocks revenue, user-facing crash, security issue |
| **Fix in queue** | Cosmetic, low-impact, workaround exists |
| **Never (close)** | Not a bug, will-not-fix, superseded |

**Cluster ZBP board** — visible across all MNZ units. Every unit's bug queue is transparent.

---

## Dependency Diagram

```
                     ┌─────────────────────────────────────┐
                     │         Cluster Metrics             │
                     │  DORA │ QS │ Defect Leakage │ SLO    │
                     └───────────────┬─────────────────────┘
                                     │
         ┌───────────────────────────┼───────────────────────────┐
         │                           │                           │
    ┌────┴────┐              ┌───────┴───────┐           ┌──────┴──────┐
    │ Unit A  │              │   Unit B      │           │   Unit C    │
    │ (MNZ)   │              │   (ADV)       │           │   (SX)      │
    └────┬────┘              └───────┬───────┘           └──────┬──────┘
         │                           │                          │
    ┌────┴───────────────────────────┴──────────────────────────┴────┐
    │              Cross-Unit Integration Tests                      │
    │   Payment → Promotion → Auction → Listing (Playwright E2E)     │
    └────────────────────────────────────────────────────────────────┘
                                     │
         ┌───────────────────────────┼───────────────────────────┐
         │                           │                           │
    ┌────┴────┐              ┌───────┴───────┐           ┌──────┴──────┐
    │ DS      │              │   Platform    │           │   CI/CD     │
    │ Audit   │              │   Quality     │           │   Gates     │
    └─────────┘              └───────────────┘           └─────────────┘
```

---

## Trade-offs

| Trade-off | Decision | Rationale | Tech Debt | Resolution |
|-----------|----------|-----------|-----------|------------|
| Manual exploratory testing | Keep for critical flows only | Automation covers 90% | 10% manual | Q3: add session-based testing |
| Performance testing | Start with k6 + platform team | No dedicated perf QA | Full perf framework | Q4: hire or train |
| Security testing | Coordinate with security team | Not core competence | In-depth pen testing | Continuous: bug bounty |
| Mobile testing | Existing unit QA + Crash Budget | No dedicated mobile QA | Cross-platform coverage | Q2: mobile QA hire |
| DS model testing | Property-based + A/B first | Gold dataset later | Gold dataset creation | Q3: build golden dataset |
| Test data management | Shared factories | No isolated per-unit data | Data conflicts | Q2: test data service |

---

## Alternatives Considered

| Alternative | Rejected Because |
|-------------|-----------------|
| **Centralized QA team** | Loses domain context — unit QA knows their product best |
| **Single E2E test suite** | Too slow (30min+), blocks DF, hard to maintain across 200+ teams |
| **Outsource DS testing** | DS models need domain expertise — must be internal |
| **No Test Lead, keep per-unit QA** | Current state — cluster risks remain unaddressed |
| **Buy test management tool** | Allure TestOps already proven in pilot — no need to buy |
| **Build custom test framework** | Playwright + k6 + Go testing are sufficient — no new framework needed |

---

## FAQ

### Q: How does the Test Lead enforce quality standards if QA reports to Unit-Leaders?

**A:** Solid line to Test Lead for quality standards, dotted line to Unit-Leader for daily work. The Test Lead sets the testing standard, defines metrics, and evaluates QA performance on quality criteria. The Unit-Leader handles sprint planning and product priorities.

### Q: How do you test DS models that are non-deterministic?

**A:** Four-layer approach: (1) Property-based tests on model invariants, (2) A/B experiments with statistical significance gates, (3) Drift detection — model metrics monitored in production, (4) Golden dataset for regression testing (developed in Q3).

### Q: Won't adding quality gates slow down 200–250 daily releases?

**A:** Quality gates are not CI bottlenecks. Each gate takes < 2 minutes: contract tests (~30s) + mutation sample (~30s) + QS check (~10s). The heavy suite runs in parallel as a nightly. The gate only blocks if CFR trend is rising or QS drops below threshold.

### Q: How do you measure Test Lead success in first 90 days?

| Phase | Goal | Metric |
|-------|------|--------|
| Month 1 | Audit current state | Complete risk map for all MNZ units |
| Month 2 | Establish cluster metrics | DORA dashboard live for all units |
| Month 3 | First cross-unit integration tests | 3 critical E2E flows covered |

---

## Load

| Activity | Frequency | Execution Time | Parallelism |
|----------|-----------|---------------|-------------|
| Unit tests (per unit) | Per commit | < 5 min | CI parallel |
| API contract tests | Per PR | < 2 min | CI parallel |
| Cross-unit integration | Per release train | < 15 min | 4× parallel |
| DS model audit | Weekly | < 30 min | Sequential |
| Full regression | Nightly | < 30 min | 8× parallel |
| Mutation testing | Per release | < 10 min (sampled) | CI parallel |

---

## Resources

### Team

| Role | Count | Source |
|------|-------|--------|
| Test Lead | 1 | This hire |
| QA Engineer (E4) | 3–4 | Existing units, re-aligned |
| QA Engineer (E3+) | 1–2 | Existing units, re-aligned |

### Environments

| Environment | Purpose | Configuration |
|-------------|---------|---------------|
| Dev | Unit testing, contract tests | Shared Kubernetes namespace |
| Staging | Cross-unit integration tests | Full MNZ cluster + mock payment |
| Prod-like | Performance testing | 10% of prod capacity |

### Tools

| Tool | Purpose | Status |
|------|---------|--------|
| Playwright | E2E, cross-unit integration | Existing in some units |
| Go testing | Unit, table-driven tests | Existing |
| k6 | Performance, load testing | Available |
| TeamCity | CI | Existing |
| Allure TestOps | Test reporting, metrics | Piloted |
| Grafana | DORA dashboard, SLO tracking | Existing |
| VictoriaMetrics | Metrics storage | Existing |

---

## Information Security

| Concern | Mitigation |
|---------|------------|
| Test data contains personal info | Synthetic data generators — no production data in test environments |
| Payment flows under test | Mock payment gateway — real gateway only in prod with limited test cards |
| API tokens in tests | Vault-based secrets — TeamCity injects via environment variables |
| Threat model | Coordinate with security team for new services |

---

## Metrics

### Business

- **Revenue impact:** No regression in monetization flows after release
- **Liquidity Rate:** DS model changes do not degrade listing sell-through
- **Seller Churn:** Onboarding and payment flow quality gates prevent churn-inducing bugs

### Product

- **Adoption Rate:** Quality gates enable faster rollout of new features
- **Conversion Rate:** Payment flow regression tests catch conversion-killing bugs before release
- **Self-Serve Rate:** UI smoke tests prevent onboarding errors

### Technical

| Metric | Current | Target |
|--------|---------|--------|
| CFR | Unknown | < 10% |
| MTTR | Unknown | < 1 hour |
| QS | Per unit (varies) | > 4.0 (cluster) |
| API Coverage (critical) | Unknown | > 90% |
| Mutation Score | 0% | > 80% |
| Flaky Test Rate | Unknown | < 1% |
| Defect Leakage | Unknown | < 3% |
| Test Suite Time | Unknown | < 30 min |

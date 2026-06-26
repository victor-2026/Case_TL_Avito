# Case TL Avito: Test Strategy for MNZ Cluster

**Роль:** Test Lead (MNZ — кластер Монетизации)
**Уровень:** E5+ / M2–M3
**Кластер:** MNZ (Монетизация) + ADV (Реклама) + SX (Финтех)

---

## Pages

| # | Page | What |
|---|------|------|
| 1 | [Case Context](01-case-context.md) | Role, cluster, expectations, level |
| 2 | [TDR Format](02-tdr-format.md) | Why the solution uses TDR — Avito's design review standard |
| 3 | [Metrics Framework](03-metrics.md) | Business, Product, Technical metrics — three-layer measurement |
| 4 | [Glossary](04-glossary.md) | All acronyms — brief |
| 5 | [Test Strategy (TDR)](05-test-strategy.md) | **Core deliverable** — full TDR for MNZ testing |

---

## TL;DR

**Problem:** MNZ cluster (Monetization + Ads + FinTech) operates at Avito's scale — 2700+ engineers, 200+ teams, 200–250 releases/day, 96000 RPS. Financial risks are high. QA is currently embedded in product units (E3–E4 level) with no cluster-level testing strategy.

**Solution (TDR):** A three-layer testing architecture + quality governance model for MNZ:

1. **Layer 1 — Unit**: unit-level testing (existing E3–E4 QA, Go/Python unit tests, API contract tests)
2. **Layer 2 — Cluster**: cross-unit integration, DS/ML quality, release governance, metrics (Test Lead owns this layer)
3. **Layer 3 — Platform**: company-wide tools (Tech Platform → Quality), non-functional testing, shared infrastructure

**Key metrics:** CFR < 10%, QS > 4.0, Mutation Score > 80%, Defect Leakage < 3%

---

## How to Use This Case

1. Start with [Case Context](01-case-context.md) to understand the role
2. Read [TDR Format](02-tdr-format.md) — this is how Avito engineers think
3. Read [Test Strategy](05-test-strategy.md) — the core deliverable
4. Use [Glossary](04-glossary.md) and [Metrics](03-metrics.md) as reference

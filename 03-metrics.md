# Metrics Framework

**Source:** [Avito TDR](https://github.com/avito-tech/playbook/blob/master/tech_design_review.md) — Metrics section

Three layers of metrics. Every TDR must list all three.

---

## Business

Measure money and platform efficiency.

| Metric | Description | Test Lead Impact |
|--------|-------------|------------------|
| **Revenue** | Monetization revenue | Indirect — bugs in payment flows = lost revenue |
| **ARPU** | Average Revenue Per User | Indirect — data correctness |
| **Liquidity Rate** | Listing sell-through speed | DS quality — undetected regression drops liquidity |
| **Inventory Fill Rate** | % of ad placements filled | Ad ranking bugs → fill rate drop |
| **Auction Revenue** | Revenue from ad auctions | Testing auction algorithms before release |
| **Seller Churn** | % sellers leaving paid services | Onboarding bugs → churn increase |

---

## Product

Measure user behavior and feature value.

| Metric | Description | Test Lead Impact |
|--------|-------------|------------------|
| **Adoption Rate** | % users adopting new feature | Bugs block adoption |
| **Conversion Rate** | Free → paid conversion | Payment flow errors kill conversion |
| **NPS (Seller)** | Net Promoter Score | Quality issues → negative NPS |
| **Retention D1/D7/D30** | User return rate | Bugs cause churn |
| **Self-Serve Rate** | % users who set up without support | UI errors → support ticket flood |
| **TTV** | Time-to-Value (first paid placement) | Onboarding friction |

---

## Technical

Direct Test Lead ownership.

### DORA

| Metric | Elite Target | Your Role |
|--------|-------------|-----------|
| **DF** — Deployment Frequency | Multiple/day | Quality gates must not slow DF |
| **LT** — Lead Time for Changes | < 1 hour | Auto-tests must not be CI bottleneck |
| **MTTR** — Mean Time to Restore | < 1 hour | RCA, regression tests, post-mortem |
| **CFR** — Change Failure Rate | 0–15% | **Primary metric** — coverage + gates drive CFR down |

### Quality Score (QS)

| Component | Weight | Description |
|-----------|--------|-------------|
| Incidents | ~30% | Count and severity |
| SLA Response | ~15% | How fast team responds to bugs |
| SLA Fix | ~15% | How fast team fixes bugs |
| Crash Budget (Mobile) | ~20% | iOS/Android crash rate |
| Coverage / Automation | ~20% | Test coverage |

**Scoring:** 0 / 0.5 / 1 per metric. Max 5.

**Your target:** QS > 4.0

### Test Metrics

| Metric | Target |
|--------|--------|
| API coverage (critical paths) | > 90% |
| Mutation Score | > 80% |
| Flaky Test Rate | < 1% |
| Full suite execution | < 30 min |
| Defect Leakage | < 3% |

### SLO

| Metric | Example for MNZ |
|--------|----------------|
| Availability | 99.9% |
| p95 Latency | < 200ms |
| Error Budget | 0.1% time (= 8.7h/year) |

---

## Quick Reference

```
Business: Revenue, ARPU, Liquidity, Fill Rate, Auction Revenue, Churn
Product:  Adoption, Conversion, NPS, Retention, Self-Serve, TTV
Technical: DORA (DF/LT/MTTR/CFR), QS, Coverage, Mutation Score, Flaky Rate
```

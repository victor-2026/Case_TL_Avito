# Case TL Avito: Test Strategy for MNZ Cluster

**Роль:** Test Lead (MNZ — кластер Монетизации)
**Уровень:** E5+ / M2–M3
**Кластер:** MNZ (Монетизация) + ADV (Реклама) + SX (Финтех)

---

## Страницы

| # | Страница | О чём |
|---|----------|-------|
| 1 | [Case Context](01-case-context.md) | Роль, кластер, ожидания, уровень |
| 2 | [TDR Format](02-tdr-format.md) | Почему решение в формате TDR — стандарт Avito для design review |
| 3 | [Metrics Framework](03-metrics.md) | Бизнес, продуктовые, технические метрики — трёхуровневая система |
| 4 | [Glossary](04-glossary.md) | Все акронимы — кратко |
| 5 | [Test Strategy (TDR)](05-test-strategy.md) | **Главный ответ** — полный TDR для тестирования MNZ |

---

## TL;DR

**Проблема:** Кластер MNZ (Монетизация + Реклама + Финтех) работает в масштабе Avito — 2700+ инженеров, 200+ команд, 200–250 релизов/день, 96000 RPS. Финансовые риски высоки. QA встроено в продуктовые юниты (уровень E3–E4), кластерной стратегии тестирования нет.

**Решение (TDR):** Трёхслойная архитектура тестирования + модель quality governance для MNZ:

1. **Layer 1 — Unit**: тестирование на уровне юнитов (существующие QA E3–E4, Go/Python unit-тесты, API contract тесты)
2. **Layer 2 — Cluster**: кросс-юнитная интеграция, качество DS/ML, release governance, метрики (этот слой владеет Test Lead)
3. **Layer 3 — Platform**: общеплатформенные инструменты (Tech Platform → Quality), нефункциональное тестирование, общая инфраструктура

**Ключевые метрики:** CFR < 10%, QS > 4.0, Mutation Score > 80%, Defect Leakage < 3%

---

## Как использовать этот кейс

1. Начните с [Case Context](01-case-context.md) — контекст роли
2. Прочитайте [TDR Format](02-tdr-format.md) — как мыслят инженеры Avito
3. Перейдите к [Test Strategy](05-test-strategy.md) — основной документ
4. Используйте [Glossary](04-glossary.md) и [Metrics](03-metrics.md) как справочник

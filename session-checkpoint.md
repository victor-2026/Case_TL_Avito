# Session Checkpoint — Case_TL_Avito

**Дата:** 2026-06-28
**Сессия:** Работа над кейсом Avito Test Lead MNZ (Session 61+, продолжение)

---

## Что сделано

### Структура репозитория
- Полная перестройка: `00`–`01`–`02`–`03`–`04`–`99`
- `raw/` — источник правды (101-facts, переименован, не редактируется)
- `wiki/` — 19 подстраниц playbook Avito
- Удалены: `01-case-context.md`, `02-tdr-format.md`, `04-glossary.md`, `05-test-strategy.md`

### Файлы ответа на кейс
| Файл | Содержание |
|------|-----------|
| `00-glossary.md` | Все термины, сверено с `/raw/Основные термины.md`. Добавлены TMG, DX, OKR |
| `01-case-full-text.md` | Точный текст кейса из PDF + registry fact/fiction |
| `02-starting.md` | **Q1:** Исследование — 3 гипотезы по команде 1, классификация багов команды 2, соседнее соглашение с командой 3 |
| `03-metrics.md` | **Q2:** Phase 1 Diagnostic (8 метрик по 3 командам) + Phase 2 Tracking (6 целей на квартал) + TMM Level 2 обязательный baseline |
| `04-actions.md` | **Q3:** 90-day plan с SMART целями: Research (wk1-2) → Quick Wins (wk3-6) → Foundation (wk7-13) |
| `99-additional metrics.md` | Справочно: Business/Product/Technical метрики, DORA (industry reference), покрытие 50-80% (из Соседского соглашения) |

### Исправления по фактам
- ZBP: 3 → 4 варианта (+ «превращаем в задачу»)
- SPT: «Service Performance Team» → «Support Project — проект в Jira»
- SLA → SLO в таблице QS (SLO — внутренняя цель, SLA — юридический контракт)
- API coverage >90% → 50-80% (из Соседского соглашения)
- TMM Level 2: не справочная метрика, а обязательный baseline с квартальным аудитом
- DORA значения MTTR/LT/DF помечены как industry reference, не из источников Avito

### Понимание роли
- Test Lead = M-grade, кластер MNZ
- В кейсе — конкретная проблемная ситуация в одном из юнитов кластера
- Использовать только факты из `raw/`, PDF кейса, playbook (по согласованию)
- Ответ — презентация на 3 вопроса, не TDR/стратегия

---

## Pipeline / Активные заявки
- **NextDay AI (Jul 2)** — единственное активное интервью
- **Avito** — отклик без подтверждения
- **Logifuture** — 🔴 Rejected (postmortem в catalog)

---

## Файл сессии
`/Users/victor/Private/Case_TL_Avito/session-checkpoint.md`

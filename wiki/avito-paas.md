# Платформа разработки Авито (PaaS)

**Источник:** [avito-tech/playbook/avito-paas.md](https://github.com/avito-tech/playbook/blob/master/avito-paas.md)

## Что такое PaaS в Avito

Внутренняя платформа разработки, которая предоставляет:

- **CI/CD** — сборка, тестирование, деплой
- **Feature flags** — точечное включение функциональности
- **Service mesh** — управление трафиком
- **Мониторинг и алерты** — Grafana + Prometheus
- **Логирование** — централизованный сбор логов
- **Test environments** — изолированные окружения для тестирования

## Инструменты PaaS

| Категория | Инструмент |
|-----------|-----------|
| CI/CD | GitLab CI / TeamCity |
| Feature flags | Feature Toggle сервис |
| Monitoring | Grafana + Prometheus |
| Logs | ELK / Loki |
| Service mesh | Istio / собственные решения |
| Test env | Kubernetes namespaces |

## Применение к кейсу

- PaaS даёт инфраструктуру для тестов: запуск в CI, feature flags для A/B тестирования
- Мониторинг (Grafana) — уже есть, нужно только настроить дашборды качества
- Test environments — можно попросить окружение для QA команды 2

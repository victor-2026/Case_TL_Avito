# Инженерные практики Avito

**Источник:** [avito-tech/playbook/avito-developer-practice.md](https://github.com/avito-tech/playbook/blob/master/avito-developer-practice.md)

## TBD (Trunk-Based Development)

- Все изменения мержатся в master/trunk
- Feature flags для незаконченных фич
- Короткие ветки (дни, не недели)

## Code Review

- Каждый PR проходит ревью
- Авто-проверки: линтер, тесты, coverage
- Нельзя мержить без аппрува

## CI/CD

- Авто-сборка на каждый коммит
- Авто-тесты в CI
- Деплой после зелёного билда
- Canary / blue-green деплой

## Тестирование

- Пирамида тестов: много unit → меньше API → мало UI
- Тест — первая документация
- Coverage как ориентир, не цель
- Стабильность тестов важнее количества

## Performance и нагрузка

- Performance тесты на критичные сценарии
- Load testing перед релизами с высоким риском
- Профилирование в production (perforator)

## Мониторинг и алерты

- Дашборды для каждого сервиса
- SLI/SLO алерты
- On-call ротация

## Применение к кейсу

- TBD + feature flags = можно катить часто, но с контролем качества
- Code review тестов — базовое требование для dev команды 1 (без QA)
- Coverage — оценить текущее состояние обеих команд
- Performance тесты — если баги команды 2 связаны с производительностью

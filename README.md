# Notification Platform — ДЗ4

Архитектурное проектирование централизованной платформы уведомлений онлайн-банка.

## Материалы

- [Функциональные и нефункциональные требования, ASR и риски](docs/requirements.md)
- [RFC: гарантированная доставка и кросс-канальный failover](docs/RFC.md)
- [C4 варианта A](diagrams/c4-option-a.puml)
- [Основной сценарий варианта A](diagrams/sequence-option-a-main.puml)
- [Failover-сценарий варианта A](diagrams/sequence-option-a-failover.puml)
- [C4 варианта B](diagrams/c4-option-b.puml)
- [Основной сценарий варианта B](diagrams/sequence-option-b-main.puml)
- [Failover-сценарий варианта B](diagrams/sequence-option-b-failover.puml)

## Краткий результат

Рассмотрены два варианта механизма гарантированной доставки:

1. собственный оркестратор на Kafka и PostgreSQL;
2. durable workflow на Temporal.

Выбран первый вариант. Он лучше подходит для ожидаемой нагрузки, позволяет независимо масштабировать каналы и опирается на привычный для банка стек. Гарантия строится на Transactional Outbox, обработке at-least-once, идемпотентности и конечном автомате доставки.

## Диаграммы

Файлы имеют формат PlantUML. Для C4 используется библиотека C4-PlantUML через `includeurl`, поэтому при первом рендере нужен интернет. Удобнее всего открыть их расширением PlantUML в IDE.

Пример рендера одной диаграммы через Kroki:

```bash
mkdir -p out
curl -sS -H 'Content-Type: text/plain' \
  --data-binary @diagrams/c4-option-a.puml \
  https://kroki.io/plantuml/svg > out/c4-option-a.svg
```

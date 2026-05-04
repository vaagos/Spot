# Spot — Documentation

Техническая документация продукта **Spot** — мобильного приложения с авторскими маршрутами по городам России.

Документация ведётся в подходе **Docs as Code**: исходники в Markdown лежат в репозитории, изменения проходят через pull request.

## Структура документации

```
docs/
├── intro.md                        — Карточка сервиса
├── overview/                       — Концепция и границы проекта
│   ├── problem.md
│   ├── audience-and-stakeholders.md
│   ├── business-goals.md
│   ├── product-description.md
│   ├── risks.md
│   └── constraints.md
├── requirements/                   — Требования
│   ├── functional.md               — Use Cases
│   ├── non-functional.md           — НФТ по 10 категориям
│   └── gathering.md                — RACI и вопросы для интервью
├── architecture/                   — Архитектура (шаблон)
│   └── overview.md                 — Диаграммы C1/C2
├── scenarios/                      — Сценарии (шаблон)
│   ├── registration.md
│   └── route-walkthrough.md
├── processes/                      — Моделирование процессов
│   └── bpmn.md                     — BPMN + DMN
├── api/                            — API
│   └── api-reference.md            — OpenAPI 3.0
├── db/                             — Модель данных
│   ├── storage.md                  — Сущности и выбор технологий
│   └── erd.md                      — ERD (3 уровня)
├── async/                          — Асинхронное взаимодействие
│   └── rating-events.md            — Kafka + Avro
├── platform/                       — Платформизация
│   └── strategy.md                 — Монетизация и B2B2C
└── layouts/                        — Макеты
    └── screens.md                  — UI-макеты + эндпоинты
```

## Просмотр

Все Markdown-файлы читаются прямо в интерфейсе GitHub. Изображения подключены через относительные пути и отображаются в превью.

Стартовая страница — [`docs/intro.md`](docs/intro.md).

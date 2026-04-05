# Индекс инженерной документации

## Назначение

Этот файл — entry point для долгоживущей engineering documentation в `docs/`.

Используй этот слой для architecture, principles, ADRs, contracts и других durable engineering decisions. Не считай временные planning или execution artifacts каноническими, если они конфликтуют с этим слоем.

## Стратегия чтения

1. Начинай с `docs/principles.md` для project values и baseline principles.
2. Переходи в релевантную documentation area ниже, а не читай все дерево целиком.
3. Открывай focused documents только когда они реально нужны текущей задаче.

## Основные documentation areas

- `docs/principles.md` - project values и high-level principles.
- `docs/methodology-layer/` - engineering documentation для слоя Project Methodology Runtime.
- `docs/contracts/` - contract layer и machine-readable boundary artifacts.
- `docs/adr/` - принятые architectural decisions и долгоживущая history решений.
- `docs/terms/` - canonical terminology maps и term definitions.
- `docs/specification/` - целевой SoT-слой для формальных спецификаций, когда в нем появляются действительно канонические specification artifacts.

## Временные legacy-разделы внутри `docs/`

Сейчас границы `docs/` уже уточнены, и временные operational artifacts выводятся из этого слоя:

- `docs/idea/` больше не должен использоваться как каталог для idea-stage artifacts; они должны жить в `operational_scope/ideas/`.
- `docs/plans/` больше не должен использоваться как каталог для planning artifacts; они должны жить в `operational_scope/plans/`.
- `docs/specification/` не должен содержать discussion drafts; такие файлы должны жить в `operational_scope/discussion/`, пока не станут каноническими спецификациями.

## Важные границы

- `docs/` — engineering Source of Truth.
- `docs/` не должен использоваться как временный execution tracker.
- Если plan меняет architecture или contracts, принятый результат должен быть отражен в `docs/` до начала реализации.
- Если `idea`, `plan` или `discussion` artifact не стал каноническим engineering document, он должен жить в `operational_scope/`, а не в `docs/`.

## Entry points по слоям

- `docs/methodology-layer/overview.md` — entry point только для этого документационного слоя, а не для всего `docs/`.
- `docs/contracts/README.md` — entry point для contract-layer policy и navigation.

## Связанные Entry points

- `AGENTS.md` для repository-wide порядка загрузки контекста.
- `project/index.md` для durable project context.
- `operational_scope/index.md` для временного execution-layer context.

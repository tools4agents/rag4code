# Индекс контекста проекта

## Назначение

Этот файл — entry point для durable project context layer.

Используй `project/`, чтобы понять repository boundaries, technical assumptions, migration state и top-level navigation. Этот слой не является engineering Source of Truth для архитектуры.

## Порядок чтения

1. `project/overview.md` для краткого описания проекта и его целей.
2. `project/gitContext.md` для repository ownership, nested repositories и git boundaries.
3. `project/techContext.md` для technical baseline и environment assumptions.
4. `project/repository-map.md` для top-level navigation по областям репозитория.
5. `project/context-migration.md` для текущей миграции от legacy `.kilocode` к новой layered model.

## Границы слоя

- Используй `project/` для durable repository context.
- Используй `docs/` для architecture, contracts, ADRs и других engineering Source of Truth artifacts.
- Используй `operational_scope/` для временных plans, tasks, research и execution status.

## Связанные Entry points

- `AGENTS.md` для repository-wide порядка загрузки контекста.
- `docs/index.md` для navigation по engineering documentation.
- `operational_scope/index.md` для индекса execution-layer.

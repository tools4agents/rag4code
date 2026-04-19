# Индекс контекста проекта

## Назначение

Этот файл — entry point для durable project context layer проекта `<project-slug>`.

Используй `project/`, чтобы понять назначение репозитория, git boundaries, technical baseline, secret handling и repository-local loading order.

Этот слой не является engineering Source of Truth для архитектуры.

## Порядок чтения

1. `project/overview.md`
2. `project/gitContext.md`
3. `project/techContext.md`
4. `project/secretsContext.md`
5. `project/entry-points.md`
6. optional `project/codeStyle.md`
7. optional `project/repository-map.md`
8. optional `project/context-migration.md`

## Границы слоя

- Используй `project/` для durable repository context.
- Используй `docs/` для engineering SoT.
- Используй `operational_scope/` для временного execution context.

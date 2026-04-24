# Индекс контекста проекта

## Назначение

Этот файл — entry point для durable project context layer проекта `<project-slug>`.

Используй `project/`, чтобы понять назначение репозитория, git boundaries, technical baseline, secret handling и где находится repository-local routing contract.

Этот слой не является engineering Source of Truth для архитектуры.

## Состав слоя

- `project/overview.md` — назначение проекта и ограничения этого context layer.
- `project/gitContext.md` — repository ownership, git boundaries и рабочие правила для git-операций.
- `project/techContext.md` — technical baseline проекта.
- `project/secretsContext.md` — secret handling baseline и local files policy.
- `project/entry-points.md` — routing/loading contract и ownership split между context layers.
- optional `project/codeStyle.md` — repository-local code style guidance.
- optional `project/repository-map.md` — карта репозитория, если она реально полезна.
- optional `project/context-migration.md` — migration notes для context layer, если они нужны.

Детальный порядок входа в контекст и ownership split между layers см. в `project/entry-points.md`.

## Границы слоя

- Используй `project/` для durable repository context.
- Используй `docs/` для engineering SoT.
- Используй `operational_scope/` для временного execution context.
- Не дублируй routing contract из `project/entry-points.md` в этом индексе.

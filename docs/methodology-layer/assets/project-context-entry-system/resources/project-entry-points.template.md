# Entry Points

## Назначение

Этот файл фиксирует concrete project-local loading order и ownership split между `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и target-specific layers.

## Порядок чтения контекста

1. `AGENTS.md` как top-level router artifact.
2. `project/index.md` как durable context entry.
3. `project/gitContext.md` для repository ownership и git boundaries.
4. `project/techContext.md` для technical baseline.
5. `project/secretsContext.md` для secret handling и local files policy.
6. optional `project/codeStyle.md`.
7. optional `project/repository-map.md`.
8. optional `project/context-migration.md`.
9. `docs/index.md` для engineering Source of Truth.
10. `operational_scope/task-map.md` только когда нужен execution context.

Если временный operational artifact конфликтует с `docs/`, следуй `docs/`.

## Ownership Model

### `AGENTS.md`

`AGENTS.md` владеет только router-level guidance.

### `project/`

`project/` владеет durable context.

### `docs/`

`docs/` владеет engineering SoT.

### `operational_scope/`

`operational_scope/` владеет execution context.

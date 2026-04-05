# Индекс слоя Operational Scope

## Назначение

Этот файл — entry point для временного execution layer текущей итерации.

`operational_scope/` предназначен для plans, tasks, research, discussion artifacts, task map и другого short-lived delivery context. Это не engineering Source of Truth.

## Статус

Этот слой вводится во время миграции с legacy layout `tasks_descriptions/` и временных operational artifacts, которые раньше лежали в `docs/`.

Пока миграция не завершена, часть execution context все еще живет вне `operational_scope/`, но `ideas/`, `plans/`, `research/`, `discussion/` и `tasks/` уже перенесены в этот слой.

## Целевое содержимое

- `operational_scope/task-map.md` для индекса задач.
- `operational_scope/tasks/` для execution task files.
- `operational_scope/plans/` для planning artifacts.
- `operational_scope/ideas/` для idea-stage artifacts.
- `operational_scope/research/` для research artifacts.
- `operational_scope/discussion/` для временных discussion documents.

## Правила

- Используй этот слой для временного execution context.
- Не используй этот слой как долгоживущий Source of Truth для архитектуры.
- Если execution меняет architecture или contracts, сначала обновляй `docs/`.

## Примечание о миграции

- После текущего этапа миграции основные operational artifacts уже перенесены в `operational_scope/`.
- `tasks_descriptions/` остается как legacy layout до отдельного cleanup шага.
- Эта директория постепенно станет primary entry point для operational context.

## Связанные Entry points

- `AGENTS.md` для repository-wide порядка загрузки контекста.
- `project/index.md` для durable project context.
- `docs/index.md` для navigation по engineering Source of Truth.

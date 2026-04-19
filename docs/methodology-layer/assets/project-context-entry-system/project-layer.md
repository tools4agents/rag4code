# Project Layer

## Назначение

Этот документ фиксирует роль `project/` как durable context layer внутри [`project-context-entry-system`](./project-context-entry-system.md).

## Что должно жить в `project/`

`Project/` должен содержать durable repository context:

- overview проекта;
- git boundaries;
- technical baseline;
- secrets handling baseline;
- loading-order detail;
- optional code style, repository map и migration notes.

## Что не должно жить в `project/`

- engineering architecture canon;
- task execution status;
- temporary spike findings;
- target-specific runtime config internals.

## Baseline principle

`Project/` адаптирует работу агента под конкретный проект, но не подменяет `docs/` и не дублирует `AGENTS.md`.

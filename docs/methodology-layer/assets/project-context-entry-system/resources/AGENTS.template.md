# <Project Name>

## О проекте

`<project-slug>` — <short project description>.

## Как читать контекст

Используй такой порядок чтения:

1. `project/index.md` для durable project context.
2. `docs/index.md` для engineering Source of Truth.
3. `operational_scope/task-map.md` для текущего execution context.
4. relevant file из `operational_scope/tasks/`, если работа идет по конкретной задаче.

Если временный operational artifact конфликтует с `docs/`, следуй `docs/`.

## Правила Source of Truth

- `project/` — durable repository context.
- `docs/` — engineering Source of Truth.
- `operational_scope/` — execution layer.
- Не воспринимай временные operational artifacts как долгоживущий архитектурный канон.

## Ключевые entry points

- `project/index.md`
- `docs/index.md`
- `operational_scope/task-map.md`

## Рабочий язык

- Документацию и project-local context пиши на русском языке.
- Код, identifiers, docstrings, code comments и commit messages пиши на английском языке.

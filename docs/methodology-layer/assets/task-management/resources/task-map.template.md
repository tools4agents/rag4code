# Task Map

> Status: Active  
> Scope: execution index for `<project-or-scope>`  
> Role: канонический индекс задач текущей итерации

## Назначение

Этот файл фиксирует поэтапный execution plan для `<project-or-scope>`.

Он нужен, чтобы:

- держать work-in-progress в явной форме;
- не распылять фокус на весь проект сразу;
- двигаться по связным задачам в порядке их зависимости;
- упрощать handoff между агентами и сессиями.

## Этапы

| Stage | Название | Цель | Статус |
| --- | --- | --- | --- |
| Stage 1 | `<Stage 1 name>` | <What this stage should stabilize> | pending |
| Stage 2 | `<Stage 2 name>` | <What this stage should materialize> | pending |
| Stage 3 | `<Stage 3 name>` | <What this stage should implement> | pending |

Если проекту нужен flat `task-map`, этот блок может быть упрощен или опущен.

## Stage 1 — `<Stage 1 name>`

| Task ID | Задача | Назначение | Статус |
| --- | --- | --- | --- |
| T1.1 | `<Task 1>` | <Expected output of the task> | pending |
| T1.2 | `<Task 2>` | <Expected output of the task> | pending |
| T1.3 | `<Task 3>` | <Expected output of the task> | pending |

## Stage 2 — `<Stage 2 name>`

| Task ID | Задача | Назначение | Статус |
| --- | --- | --- | --- |
| T2.1 | `<Task 1>` | <Expected output of the task> | pending |
| T2.2 | `<Task 2>` | <Expected output of the task> | pending |

## Stage 3 — `<Stage 3 name>`

| Task ID | Задача | Назначение | Статус |
| --- | --- | --- | --- |
| T3.1 | `<Task 1>` | <Expected output of the task> | pending |
| T3.2 | `<Task 2>` | <Expected output of the task> | pending |

## Текущий фокус

- Active stage: `<Stage N>`
- Active task candidate: `<Task ID and name>`
- Decision rule: <What must be agreed or stabilized before the next task opens>

## Execution policy

- Сначала стабилизируется upstream layer, затем открывается downstream work.
- Не materialize-ить большой пакет зависимых артефактов до review предыдущего шага.
- После завершения каждой задачи обновлять этот индекс и при необходимости создавать отдельный task file в `operational_scope/tasks/`.
- Если задача становится слишком широкой, разделять ее на более узкие sequential tasks.

## Как использовать template

- Используй этот template как стартовую форму для stage-aware `task-map`.
- Убирай лишние stages, если проект меньше и flat list удобнее.
- Не превращай `task-map` в длинный narrative plan: детали исполнения живут в task files.
- Архитектурный канон должен жить в `docs/`, а `task-map` должен оставаться execution index.

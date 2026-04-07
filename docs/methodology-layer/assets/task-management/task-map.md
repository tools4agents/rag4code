# Task Map

> Status: Draft  
> Scope: concrete `task-management-system asset` под названием `task-map`  
> Role: Source of Truth для baseline task storage, task index и execution tracking model

## Назначение

Этот документ фиксирует первый concrete [`task-management-system asset`](../../../terms/project/terms/task-management-system-asset.md): `task-map`.

Он задает минимальную систему хранения, индексации и управления [`task artifacts`](../../../terms/project/terms/task-artifact.md) внутри проекта.

## Что задает `task-map`

`Task-map` отвечает на вопросы:

- где живут task-oriented operational artifacts;
- какой файл считается task index;
- как фиксируется execution context;
- как задачи связываются с engineering SoT и при необходимости с отдельными supporting artifacts.

## Baseline layout

Для первой итерации `task-map` использует такой baseline layout:

```text
operational_scope/
  tasks/
  task-map.md
```

## Роли элементов layout

- `operational_scope/task-map.md` — канонический индекс task-layer;
- `operational_scope/tasks/` — исполнимые [`task artifacts`](../../../terms/project/terms/task-artifact.md).

Другие каталоги внутри `operational_scope/` могут существовать, но они не определяются этим asset и не считаются его обязательной частью.

## Что считается task index

Для `task-map` каноническим индексом task-layer считается `operational_scope/task-map.md`.

Этот файл должен давать краткую карту задач:

- название;
- статус;
- ссылку на task file.

Индекс нужен для quick navigation и focus management, а не для повторного пересказа содержимого task files.

## Связь с execution tracking

Каждый [`task artifact`](../../../terms/project/terms/task-artifact.md) должен хранить минимальный execution context.

Для первой итерации baseline включает:

- контекст;
- цель;
- scope;
- шаги реализации;
- `Definition of Done`;
- `Execution Status`.

## Связь с supporting artifacts

Обычно задачи в этой системе опираются прежде всего на [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md).

В отдельных случаях задача может также ссылаться на:

- [`plan artifacts`](../../../terms/project/terms/plan-artifact.md);
- [`research artifacts`](../../../terms/project/terms/research-artifact.md);
- [`spike reports`](../../../terms/project/terms/spike-report.md).

Но такие связи являются опциональными и не определяют базовую структуру `task-map`.

## Связь с knowledge lifecycle

`Task-map` не задает сам lifecycle знания в проекте.

Он предполагает, что project already uses какой-то [`knowledge-lifecycle asset`](../../../terms/project/terms/knowledge-lifecycle-asset.md), например `document-driven-development`.

То есть `task-map` управляет только task-oriented operational storage, а knowledge lifecycle asset задает движение знания между слоями.

## Связь с terms management

`Task-map` не задает glossary system.

Если в проекте есть [`terms-management-system asset`](../../../terms/project/terms/terms-management-system-asset.md), task artifacts должны использовать его terminology baseline, но не подменять собой term definitions.

## Связь с task-management skills

`Task-map` является естественной основой для skills вроде:

- `task-setter`;
- `task-handoff-writer`;
- `active-task-setter` или его будущего аналога;
- других task-oriented operational skills.

Эти skills должны опираться на `task-map` как на task-layer baseline.

## Что этот документ не делает

Этот документ не описывает:

- process semantics конкретной methodology;
- critic/reviewer workflow как process model;
- lifecycle знания между `Operational Documentation Layer`, `Engineering Documentation SoT` и `Release Documentation Layer`;
- release publishing pipeline.

## Связь с другими документами

Этот документ нужно читать вместе с:

- [`asset-taxonomy-and-composition-model.md`](../../asset-taxonomy-and-composition-model.md);
- [`documentation-lifecycle-layers.md`](../knowledge-lifecycle/documentation-lifecycle-layers.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- `task-map` является concrete `task-management-system asset`.
- `operational_scope/task-map.md` является каноническим task index для этой системы.
- `operational_scope/tasks/` является baseline storage location для [`task artifacts`](../../../terms/project/terms/task-artifact.md).
- task-oriented operational artifacts должны жить в task-layer, а не в `docs/`.
- task system не должна подменять knowledge lifecycle model.
- task artifacts обычно опираются на [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md).
- ссылки на plans, research и spike reports являются опциональными supporting links, а не частью обязательного layout этого asset.

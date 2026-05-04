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
- как в task index фиксируются этапы разработки и sequential tasks внутри этапов;
- как задачи связываются с engineering SoT и при необходимости с отдельными supporting artifacts.

## Baseline layout

Для первой итерации `task-map` использует такой baseline layout:

```text
operational_scope/
  tasks/
  task-map.md
```

Scope-aware layout расширяет этот baseline и следует path rules из [`operational-artifact-path-rules.md`](./resources/operational-artifact-path-rules.md):

```text
operational_scope/
  task-map.md
  inputs/
  tasks/
    task-map.md
    execution/
    research/
    deep-research/
    spikes/
  research/
  deep-research/
  spikes/
  initiatives/
    <initiative-slug>/
      tasks/
        task-map.md
        execution/
        research/
        deep-research/
        spikes/
      research/
      deep-research/
      spikes/
```

## Роли элементов layout

- `operational_scope/task-map.md` — канонический индекс task-layer; в scope-aware режиме это central navigation index для task scopes;
- `operational_scope/tasks/` — baseline storage location для исполнимых [`task artifacts`](../../../terms/project/terms/task-artifact.md);
- `operational_scope/tasks/task-map.md` — task index для unscoped tasks;
- `operational_scope/initiatives/<initiative-slug>/tasks/task-map.md` — task index внутри initiative workspace;
- `operational_scope/initiatives/<initiative-slug>/tasks/<task-type>/` — initiative-scoped task artifacts.

Другие каталоги внутри `operational_scope/` могут существовать, но они не определяются этим asset и не считаются его обязательной частью.

## Что считается task index

Для `task-map` каноническим индексом task-layer считается `operational_scope/task-map.md`.

В scope-aware режиме этот файл является центральным индексом task scopes, а не flat list всех задач.

Центральный индекс должен давать краткую карту scopes:

- scope slug;
- scope type;
- статус;
- ссылку на scope task index;
- связанную initiative, если она есть.

В flat режиме этот файл может давать краткую карту задач:

- название;
- статус;
- ссылку на task file.

Индекс нужен для quick navigation и focus management, а не для повторного пересказа содержимого task files.

## Scope-aware task maps

`Task-map` должен поддерживать scope-aware модель, когда task artifacts группируются по initiative workspace или unscoped task area.

Detailed path rules live in [`operational-artifact-path-rules.md`](./resources/operational-artifact-path-rules.md).

### Scope identity

Scope определяется так:

```text
initiative work:
  scope = <initiative-slug>
  task map = operational_scope/initiatives/<initiative-slug>/tasks/task-map.md

unscoped work:
  scope = unscoped
  task map = operational_scope/tasks/task-map.md
```

Все work items, связанные с initiative, используют initiative workspace as namespace.

Все work items без конкретной initiative используют unscoped task area.

### Task types inside task map

Task map может содержать секции по task types:

```text
execution tasks
research tasks
deep-research tasks
spike tasks
```

### Evidence tasks and outputs

Evidence task может быть создан из разных мест SDLC workflow, когда нужно уменьшить неопределенность.

Evidence task фиксирует:

- какую uncertainty нужно уменьшить;
- что нужно проверить или исследовать;
- какой evidence ожидается;
- куда evidence должен вернуться в SDLC context.

Evidence output влияет на дальнейшее движение SDLC workflow, но task-management layer не принимает route/product/system/architecture decisions сам.

Task artifacts and evidence outputs use different paths:

```text
task artifact:
  .../tasks/<task-type>/<task-slug>.md

evidence output:
  .../<evidence-type>/<evidence-slug>/
```

## Stage-aware task maps

`Task-map` может быть не только flat list задач, но и stage-aware execution index.

Такой формат особенно полезен, когда:

- работа идет в несколько крупных [`project stage`](../../../terms/project/terms/project-stage.md);
- между задачами есть dependency order;
- важно не открывать downstream work до stabilizing upstream result;
- над проектом работают разные агенты или сессии, которым нужен явный execution route.

### Что такое stage-aware task map

В stage-aware варианте `operational_scope/task-map.md` может явно содержать:

- таблицу этапов;
- по одной компактной таблице задач на каждый этап;
- секцию `Current focus`;
- короткую `Execution policy`.

### Recommended minimal stage model

Для software-delivery проектов полезен baseline вида:

1. `Documentation SoT`
2. `Project Structure`
3. `Implementation`
4. optional `Verification / Integration`

Этот набор не является жестким универсальным стандартом.

Но сам паттерн staged decomposition считается полезной частью `task-map`, если он помогает удерживать фокус и dependency order.

### Почему stages полезны

Stage-aware decomposition нужна, чтобы:

- не смешивать SoT design, filesystem materialization и кодовую реализацию в одном проходе;
- видеть, какой слой уже достаточно зрел для перехода дальше;
- уменьшать каскадные переделки downstream artifacts после review upstream layer;
- упрощать handoff между агентами и сессиями.

### Sequential tasks inside stage

Даже внутри одного этапа задачи рекомендуется упорядочивать по dependency order.

Например, внутри `Documentation SoT` сначала может идти:

1. documentation skeleton;
2. architecture overview set;
3. runtime/package traceability;
4. contracts;
5. terms;
6. testing docs.

Это помогает применять small-batch execution вместо широкого прохода по всему проекту сразу.

### Small-batch rule

Если используется stage-aware `task-map`, рекомендуется такой invariant:

- следующий крупный task не открывается, пока предыдущий достаточно не stabilized;
- не нужно materialize-ить большой пакет downstream artifacts до review upstream result;
- отдельный task file появляется тогда, когда задача уже имеет bounded scope и понятный expected output.

### Flat vs staged

Оба формата допустимы:

- flat `task-map` — когда delivery scope мал и стадийность не дает особой пользы;
- staged `task-map` — когда работа multi-step, multi-session или multi-agent.

`Task-management-system asset` должен поддерживать оба режима, а не навязывать только один.

## Связь с execution tracking

Каждый [`task artifact`](../../../terms/project/terms/task-artifact.md) должен хранить минимальный execution context.

Для первой итерации baseline включает:

- контекст;
- цель;
- scope;
- шаги реализации;
- `Definition of Done`;
- `Execution Status`.

Если проект использует stage-aware `task-map`, execution context может дополнительно включать:

- `Active stage`;
- `Active task candidate`;
- короткое `Decision rule` для перехода к следующему task;
- stage-level status.

## Связь с SDLC workflow

`Task-map` не заменяет SDLC workflow и не определяет, когда именно work item должен стать задачей.

В новой SDLC модели:

```text
input artifacts
  -> Initiative Workspace Preparation / downstream design and evidence workflows
  -> Execution Planning & Task Decomposition
  -> execution tasks
  -> Task Implementation
```

`execution tasks` обычно появляются как результат `Execution Planning & Task Decomposition` для конкретной initiative.

`trivial-direct` не создает initiative workspace, но все равно получает task-level traceability через unscoped task area and lightweight Execution Planning.

`Research`, `Deep Research` and `Spike` могут создавать `evidence tasks` из разных мест SDLC, если нужно уменьшить неопределенность до продолжения design или execution flow.

## Связь с supporting artifacts

Обычно задачи в этой системе опираются прежде всего на [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md).

В отдельных случаях задача может также ссылаться на:

- [`plan artifacts`](../../../terms/project/terms/plan-artifact.md);
- [`research artifacts`](../../../terms/project/terms/research-artifact.md);
- [`spike reports`](../../../terms/project/terms/spike-report.md).

Но такие связи являются опциональными и не определяют базовую структуру `task-map`.

Idea, plan, research and spike artifacts являются supporting/source artifacts. Они не образуют обязательный универсальный pipeline `idea -> plan -> taskset -> task` внутри этого asset.

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
- `task-materializer`;
- `taskset-materializer`;
- `idea-capture`;
- `plan-capture`;
- `deep-research-task-setter`;
- `spike-experiment-task-setter`;
- других task-oriented operational skills.

Эти skills должны опираться на `task-map` как на task-layer baseline.

## Template and reuse

Для bootstrap нового `operational_scope/task-map.md` можно использовать reusable template:

- [`task-map.template.md`](./resources/task-map.template.md)

Template не задает обязательный process model, но дает:

- согласованную структуру для scope-aware and stage-aware task maps;
- единообразную форму таблиц этапов и задач;
- reusable starting point для новых проектов.

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
- [`operational-artifact-path-rules.md`](./resources/operational-artifact-path-rules.md);
- [`task-map.template.md`](./resources/task-map.template.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- `task-map` является concrete `task-management-system asset`.
- `operational_scope/task-map.md` является каноническим task index для этой системы and may act as central navigation index for task scopes.
- `operational_scope/tasks/` является baseline storage location для [`task artifacts`](../../../terms/project/terms/task-artifact.md).
- Scope-aware task maps group tasks by initiative workspace or unscoped task area.
- Initiative task artifacts live under `operational_scope/initiatives/<initiative-slug>/tasks/<task-type>/`.
- Unscoped task artifacts live under `operational_scope/tasks/<task-type>/`.
- Evidence output artifacts live outside `tasks/`: under `operational_scope/initiatives/<initiative-slug>/<evidence-type>/<evidence-slug>/` or `operational_scope/<evidence-type>/<evidence-slug>/`.
- Detailed path rules are defined in [`operational-artifact-path-rules.md`](./resources/operational-artifact-path-rules.md).
- task index может быть как flat, так и stage-aware, если это помогает execution continuity.
- task-oriented operational artifacts должны жить в task-layer, а не в `docs/`.
- task system не должна подменять knowledge lifecycle model.
- task artifacts обычно опираются на [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md).
- stage-aware task map должен помогать управлять dependency order, focus и handoff между сессиями.
- ссылки на plans, research и spike reports являются опциональными supporting links, а не частью обязательного layout этого asset.

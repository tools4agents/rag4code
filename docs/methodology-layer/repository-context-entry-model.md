# Repository Context Entry Model for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая модель входных точек repository context, порядка загрузки контекста и ownership boundaries для project-scoped agent work  
> Role: Source of Truth для системы входных точек и загрузки контекста проекта как отдельного слоя structure + navigation + ownership

## 1. Назначение документа

Этот документ фиксирует [`repository-context-entry-model`](../terms/project/terms/repository-context-entry-model.md) для `Project Methodology Runtime`.

Его задача - описать:
- какие entry points должен иметь проект для человека и агента;
- в каком порядке эти entry points читаются;
- как между ними распределяется ответственность;
- как работает [`nested-repo-context-switching`](../terms/project/terms/nested-repo-context-switching.md);
- как отделяется navigation contract от [`Engineering Documentation SoT`](../terms/project/terms/engineering-documentation-sot.md), execution layer и Kilo runtime artifacts.

Этот документ не описывает:
- heuristic discovery и classification project roots;
- artifact taxonomy во всех деталях;
- process semantics `workflow`, `workflow-step`, `step-vacancy` и `agent-role`;
- contract policy;
- adapter implementation details.

## 2. Почему это отдельный focused spec

Этот bounded context нельзя смешивать с [`project-discovery.md`](project-discovery.md).

`Project Discovery` отвечает на вопросы:
- какие project roots существуют;
- какие из них являются `root-project`, `nested-project`, `external-project-reference` или `service-managed-root`;
- как эти решения подтверждаются и сохраняются.

`Repository context entry model` отвечает на другой класс вопросов:
- как агент входит в уже выбранный project context;
- какие файлы считаются canonical entry points этого context;
- как читать проект по слоям без смешения ownership;
- когда нужно переключаться на локальный context autonomous nested project.

То есть здесь речь идет не про discovery, а про систему входных точек и загрузки контекста проекта.

Этот focused spec опирается на принципы из [`principles.md`](principles.md), прежде всего на:
- `lazy loading` и `progressive disclosure`;
- `explicit over implicit`;
- `separate artifacts instead of hidden mixing`;
- удобство для человека и агента.

## 3. Что задает `repository-context-entry-model`

`Repository-context-entry-model` задает три вещи одновременно:
- `structure` - какие entry-point artifacts и directories должны существовать;
- `navigation` - в каком порядке они читаются;
- `ownership` - какой файл или слой чем владеет и что не должен дублировать.

Главный invariant такой:
- агент не должен читать весь repository подряд;
- проект должен давать короткий и explainable маршрут загрузки контекста;
- этот маршрут должен быть одинаково понятен человеку и агенту.

Этот invariant прямо следует из [`principles.md`](principles.md):
- `lazy loading` и `progressive disclosure` требуют читать контекст по слоям, а не монолитно;
- `explicit over implicit` требует явного loading order и ownership split;
- `separate artifacts instead of hidden mixing` требует не смешивать router, durable context, engineering SoT, execution layer и Kilo runtime layer.

## 4. Базовая модель entry points

Для первой итерации фиксируется следующая baseline model.

### 4.1 `AGENTS.md`

`AGENTS.md` - это top-level router artifact.

Он отвечает за:
- краткое объяснение, что это за проект;
- верхнеуровневый порядок чтения;
- переключение в autonomous nested repo, если task scope уходит туда;
- links на основные entry points.

`AGENTS.md` не должен:
- дублировать весь durable context из `project/`;
- дублировать архитектурный канон из `docs/`;
- дублировать execution details из `operational_scope/`;
- превращаться в длинный rules pack.

### 4.2 `project/index.md`

[`project/index.md`](../../project/index.md) - это durable context entry.

Он отвечает за:
- карту project-level context artifacts;
- links на repository boundaries, tech baseline и migration notes;
- объяснение границы между `project/`, `docs/` и `operational_scope/`.

### 4.3 `project/entry-points.md`

`project/entry-points.md` - это focused spec project-local loading order.

Он отвечает за:
- подробную модель entry points внутри конкретного проекта;
- порядок чтения relevant files;
- ownership split между `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и `.kilo/`;
- локальные правила `nested repo context switching`, если они есть в этом проекте.

### 4.4 `project/gitContext.md`

[`project/gitContext.md`](../../project/gitContext.md) отвечает только за repository ownership, git boundaries и nested git behavior.

### 4.5 `project/techContext.md`

[`project/techContext.md`](../../project/techContext.md) отвечает только за technical baseline и environment assumptions.

### 4.6 `project/codeStyle.md`

`project/codeStyle.md` отвечает только за coding style и project-specific authoring conventions для кода.

Этот файл относится к durable project context, а не к engineering architecture SoT.

### 4.7 `docs/index.md`

[`docs/index.md`](../../docs/index.md) - это entry point в [`Engineering Documentation SoT`](../terms/project/terms/engineering-documentation-sot.md).

Он отвечает за:
- navigation по engineering documentation;
- links на архитектурные и contract entry points;
- separation между канонической документацией и временными operational artifacts.

### 4.8 `operational_scope/index.md`

[`operational_scope/index.md`](../../operational_scope/index.md) - это entry point в [`Operational Documentation Layer`](../terms/project/terms/operational-documentation-layer.md).

Он отвечает за:
- navigation по task, plan, research, discussion и related operational artifacts;
- links на `task-map.md` и supporting execution directories;
- объяснение, что этот слой не является engineering SoT.

### 4.9 `.kilo/`

`.kilo/` - это Kilo-specific runtime/config layer выбранного проекта.

Он отвечает за:
- executable rules;
- project-local commands;
- agent artifacts;
- other Kilo-facing config artifacts, если они materialized для текущего проекта.

## 5. Рекомендуемый порядок загрузки контекста

Для первой итерации принимается такой baseline loading order:

1. Прочитать `AGENTS.md` как router artifact.
2. Проверить, не уходит ли task scope в autonomous [`nested-project`](../terms/project/terms_map.md).
3. Если scope остается в текущем project root, прочитать `project/index.md`.
4. Затем прочитать `project/entry-points.md`, если он есть.
5. Перейти в [`docs/index.md`](../../docs/index.md) для [`Engineering Documentation SoT`](../terms/project/terms/engineering-documentation-sot.md).
6. Открывать [`operational_scope/index.md`](../../operational_scope/index.md) только когда нужен execution context.
7. Открывать `.kilo/` artifacts только когда нужен Kilo-specific runtime/config behavior.

Главный invariant:
- context loading идет от router и durable navigation к SoT и затем к execution/runtime layers, а не наоборот.

## 6. Ownership model между entry points

Чтобы избежать drift и дублирования, каждый entry-point artifact имеет узкую ответственность.

### 6.1 Router ownership

`AGENTS.md` владеет только:
- кратким repository-wide route;
- high-level scope guidance;
- rule of switching to local context другого autonomous project.

### 6.2 Durable context ownership

`Project/` владеет только:
- repository boundaries;
- technical baseline;
- loading order модели;
- project-specific durable guidance, которая не является архитектурным каноном.

### 6.3 Engineering SoT ownership

`Docs/` владеет только:
- архитектурой;
- contracts;
- terminology;
- ADR и другими long-lived engineering decisions.

### 6.4 Execution-layer ownership

`Operational_scope/` владеет только:
- tasks;
- plans;
- research;
- discussion;
- other temporary execution artifacts.

### 6.5 Agent-system runtime ownership

`.kilo/` владеет только:
- Kilo-facing rules and runtime artifacts;
- command and agent projections;
- other target-specific config artifacts для текущего agent system.

## 7. [`nested-repo-context-switching`](../terms/project/terms/nested-repo-context-switching.md)

Для [`repository-context-entry-model`](../terms/project/terms/repository-context-entry-model.md) фиксируется обязательная поддержка [`nested-repo-context-switching`](../terms/project/terms/nested-repo-context-switching.md).

Это означает:
- если внутри текущего repository есть autonomous [`nested-project`](../terms/project/terms_map.md) со своим `AGENTS.md`, агент должен переключиться на его local context, когда task scope уходит туда;
- parent project не должен навязывать nested project свой `project/`, `docs/`, `operational_scope/` или `.kilo/` canon;
- parent context может использоваться только как outer navigation, пока task scope не вошел в autonomous nested project;
- fallback inheritance допустим только для отсутствующего слоя, а не для override существующего local canon.

Следствие:
- [`project/gitContext.md`](../../project/gitContext.md) должен явно фиксировать такие nested projects и их boundaries;
- `AGENTS.md` должен вести к relevant entry points, но не быть owner файла для boundary details;
- `project/entry-points.md` должен объяснять local switching policy для человека и агента.

## 8. Связь с layered documentation model

`Repository-context-entry-model` не заменяет [`documentation-lifecycle-layers.md`](assets/knowledge-lifecycle/documentation-lifecycle-layers.md).

Связь между ними такая:
- [`documentation-lifecycle-layers.md`](assets/knowledge-lifecycle/documentation-lifecycle-layers.md) задает, где рождается и канонизируется знание;
- [`repository-context-entry-model`](../terms/project/terms/repository-context-entry-model.md) задает, как агент находит правильные entry points в уже выбранном проекте.

То есть lifecycle отвечает за движение знания между слоями, а context entry model - за навигацию по этим слоям.

## 9. Связь с project-level Kilo artifacts

Этот документ признает, что project может иметь Kilo-facing artifacts вроде:
- `AGENTS.md`;
- `project/` context files;
- `.kilo/rules/`;
- `.kilo/agent/`;
- `.kilo/command/`;
- `kilo.json`.

Но он не описывает детально, какие из них являются source artifacts, какие - project-owned config, а какие - runtime materialization outputs.

Эта тема принадлежит отдельному focused spec [`agent-system-assets-and-materialization-boundaries.md`](agent-system-assets-and-materialization-boundaries.md).

## 10. Связь с `project-context-entry-system asset`

На текущем этапе [`repository-context-entry-model`](../terms/project/terms/repository-context-entry-model.md) и [`project-context-entry-system asset`](../terms/project/terms/project-context-entry-system-asset.md) считаются смежными, но разными уровнями описания.

### Focused spec

Этот документ остается focused specification и отвечает на вопросы:

- какая модель entry points считается канонической;
- как устроены `structure + navigation + ownership`;
- какие invariants должен соблюдать project context loading.

### Asset type

`Project-context-entry-system asset` отвечает на другой вопрос:

- как упаковать эту модель как reusable system of files, templates и authoring rules для инициализации новых проектов.

То есть:

- focused spec задает semantic model;
- asset type задает reusable packaging and materialization baseline.

Concrete reusable implementation этого asset type фиксируется в:

- [`assets/project-context-entry-system/index.md`](assets/project-context-entry-system/index.md)

Следствие:

- этот документ не должен растворяться в template catalog;
- asset documentation не должна подменять semantic model focused spec.

## 11. Что этот документ не должен делать

Этот документ не должен:
- дублировать discovery classification model;
- превращаться в contract policy;
- дублировать architecture overview;
- дублировать task system layout во всех деталях;
- описывать внутренний Kilo adapter implementation manual.

Если в него начинают попадать filesystem heuristics для `.git`-scan, full runtime adapter schemas или process semantics workflow execution, это означает нарушение boundaries.

## 12. Связь с другими каноническими документами

Этот документ нужно читать вместе с:
- [`overview.md`](overview.md);
- [`project-discovery.md`](project-discovery.md);
- [`documentation-lifecycle-layers.md`](assets/knowledge-lifecycle/documentation-lifecycle-layers.md);
- [`task-map.md`](assets/task-management/task-map.md);
- [`terms-map.md`](assets/terms-management/terms-map.md);
- [`interfaces-and-storage.md`](interfaces-and-storage.md);
- [`layered-sot-and-materialization-model.md`](layered-sot-and-materialization-model.md).

## 13. Canonical invariants

- [`repository-context-entry-model`](../terms/project/terms/repository-context-entry-model.md) задает систему входных точек и загрузки контекста проекта как `structure + navigation + ownership`.
- [`repository-context-entry-model`](../terms/project/terms/repository-context-entry-model.md) не равен `project-discovery`.
- `AGENTS.md` является router artifact, а не полной replacement model для всех context layers.
- `project/` является durable context layer, а не engineering SoT.
- `docs/` является engineering SoT.
- `operational_scope/` является execution layer, а не architectural canon.
- `.kilo/` является target agent-system runtime/config layer, а не полным semantic owner layer проекта.
- autonomous [`nested-project`](../terms/project/terms_map.md) со своим `AGENTS.md` должен переключать агента на local context для своего scope.
- reusable packaging этой модели фиксируется через `project-context-entry-system asset`.

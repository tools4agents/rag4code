# Asset Taxonomy and Composition Model for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая модель типов assets, composition packs и их свободной композиции в `Project Methodology Runtime`  
> Role: Source of Truth для asset taxonomy поверх `HyperGraph Asset Catalog SoT`

## Назначение

Этот документ фиксирует, какие виды assets HyperGraph считает first-class reusable units и как из них собираются совместимые compositions.

Он нужен, чтобы:

- отделить asset types друг от друга;
- не смешивать operating model, task system, terms system и methodology;
- зафиксировать свободную композицию assets без жесткого hardcoded dependency tree;
- дать базу для будущего package management внутри `HyperGraph Asset Catalog SoT`.

## Базовый принцип

HyperGraph управляет не одной фиксированной методологией, а экосистемой совместимых assets.

Assets могут:

- использоваться по отдельности;
- рекомендоваться друг с другом;
- включаться в composition packs;
- заменяться альтернативными реализациями того же asset type.

## Базовые asset types

В этом документе важно различать:

- `asset type` — класс reusable assets;
- `concrete asset` — конкретная реализация этого asset type;
- `composition pack` — совместимая сборка нескольких concrete assets.

### `knowledge-lifecycle asset`

Задает модель жизненного цикла знания в проекте.

Этот тип asset отвечает на вопросы:

- где рождается новое знание;
- где оно канонизируется;
- где оно публикуется для внешнего потребления.

### `task-management-system asset`

Задает систему хранения, индексации и управления задачами.

Этот тип asset отвечает на вопросы:

- где живут task artifacts;
- как устроен task index;
- как фиксируются status, handoff, focus и execution context.

### `terms-management-system asset`

Задает систему хранения и раскрытия терминов.

Этот тип asset отвечает на вопросы:

- где живут `terms_map.md` и detail pages;
- как организован lazy loading терминов;
- как glossary используется в инженерной и operational documentation.

### `research-management-system asset`

Задает систему хранения, индексации, branching и traceability для research documentation.

Этот тип asset отвечает на вопросы:
- где живет research index;
- как topic раскладывается на branches и iterations;
- как research artifacts поддерживают handoff и continuation;
- как findings и evidence связываются с upstream questions и synthesis.

### `testing-system asset`

Задает систему хранения, индексации и traceability для testing documentation и links к test implementation.

Этот тип asset отвечает на вопросы:
- где живет test index;
- как устроены suite pages;
- как задается baseline test traceability chain;
- как documentation связана с code-level test implementation.

### `traceability-system asset`

Задает систему markdown-first traceability для регистрации graph-ready entities, edges and traces с возможной derived graph projection.

Этот тип asset отвечает на вопросы:

- где находятся entry points для traceability navigation;
- как устроены entity registries для graph vertices;
- как описываются atomic relationships между entities;
- как описываются curated trace chains поверх atomic edges;
- как markdown/code Source of Truth соотносится с derived graph database and MCP query layer.

`traceability-system asset` задает generic mechanics traceability и не должен владеть SDLC-specific entity families. Например, он может описывать pattern `entity registry -> edges map -> trace map`, но не обязан знать, что конкретная методология связывает Product Design, System Design, Architecture Design, Test Design, tasks and code.

### `workflow asset`

Задает reusable [`workflow`](../terms/project/terms/workflow.md) как самостоятельную process entity.

Этот тип asset отвечает на вопросы:

- какую bounded process goal решает workflow;
- какие [`workflow-step`](../terms/project/terms/workflow-step.md), gate-like steps или nested workflows входят в процесс;
- какие roles, rules, skills or supporting assets нужны для выполнения workflow;
- как workflow package может быть installed and reused в разных methodology compositions.

`workflow asset` не равен [`workflow-pack`](../terms/project/terms/workflow-pack.md): `workflow` — semantic process entity, а `workflow-pack` — packaging boundary для source artifacts этого workflow.

Примеры возможных standalone workflow assets:

- research workflow;
- spike experiment workflow;
- review workflow;
- documentation sync workflow;
- opportunity exploration workflow.

### `methodology-workflow asset`

Задает главный SDLC / delivery workflow методологии как специализированный workflow верхнего уровня.

В текущей терминологии HyperGraph этот concept исторически называется `methodology workflow`. Название `methodology-workflow asset` используется здесь как taxonomy-level label; отдельная работа по переименованию SDLC workflow terminology может быть выполнена позже.

Этот тип asset отвечает на вопросы:

- какой top-level development process рекомендует методология;
- какие stages, process workflows and cross-cutting workflows входят в SDLC graph;
- какие transition points, returns, consolidation/freeze workflows and downstream routes являются частью delivery model;
- какие supporting subsystem assets нужны методологии: task management, testing system, traceability system, terms management and others.

`methodology-workflow asset` может ссылаться на standalone `workflow assets` как на nested или supporting workflows, но не должен поглощать generic mechanics этих assets.

### `methodology asset`

Задает process model разработки.

Этот тип asset отвечает на вопросы:

- какой workflow или набор workflows рекомендуются;
- какие роли, rules и skills нужны по этапам;
- какие review, critique и planning loops являются частью методологии.

`methodology asset` может включать или рекомендовать один `methodology-workflow asset`, набор supporting `workflow assets` и совместимые subsystem assets. Он не обязан владеть всеми subsystem conventions напрямую.

### `rules pack`

Содержит набор reusable правил и policy artifacts.

### `skills pack`

Содержит набор reusable skills, которые могут использоваться человеком и агентом.

### `agent-role pack`

Содержит reusable [`agent-role`](../terms/project/terms/agent-role.md) и связанные `agent-system`-specific assets.

### `reference pack`

Содержит external reference knowledge про конкретную `agent-system` или другую внешнюю систему.

## Composition pack

`Composition pack` — это publishable совместимый набор assets, который разработчик может подключить как готовый методологический стек.

Composition pack может включать:

- один `knowledge-lifecycle asset`;
- один `task-management-system asset`;
- один `terms-management-system asset`;
- один `research-management-system asset`;
- один `testing-system asset`;
- один `traceability-system asset`, если composition требует graph-ready traceability;
- один `methodology-workflow asset`, если composition задает top-level SDLC/delivery workflow;
- один или несколько supporting `workflow assets`;
- один или несколько `methodology assets`;
- `rules packs`;
- `skills packs`;
- `agent-role packs`;
- `reference packs`.

## Свободная композиция вместо жестких зависимостей

Asset taxonomy не требует, чтобы каждый asset type жестко зависел от всех остальных.

Вместо этого HyperGraph должен поддерживать более свободную модель связей:

- `requires`;
- `compatible_with`;
- `recommended_with`;
- `included_in_composition`.

Это позволяет:

- использовать asset отдельно;
- менять один subsystem asset без полной замены methodology stack;
- публиковать альтернативные compositions;
- заменять task system, terms system или rules pack независимо от methodology.

## Первый concrete composition example

На текущем этапе пример composition удобно показывать в табличной форме.

| Asset type | Concrete asset | Роль в composition |
| --- | --- | --- |
| `knowledge-lifecycle asset` | `document-driven-development` | Задает lifecycle знания через documentation layers. |
| `task-management-system asset` | [`task-map.md`](assets/task-management/task-map.md) | Задает систему хранения, индексации и управления задачами. |
| `terms-management-system asset` | [`terms-map.md`](assets/terms-management/terms-map.md) | Задает систему хранения и progressive disclosure терминов. |
| `research-management-system asset` | [`research-tree.md`](assets/research-management/research-tree.md) | Задает tree-shaped research storage, branch navigation и research traceability. |
| `testing-system asset` | [`test-map.md`](assets/testing-system/test-map.md) | Задает систему хранения test documentation, suite navigation и baseline traceability. |
| `traceability-system asset` | [`index.md`](assets/traceability/index.md) | Задает markdown-first entity registries, edge maps, trace maps and derived graph projection conventions. |
| `methodology-workflow asset` | `Adaptive Waterfall for Agents workflow` | Задает top-level SDLC graph, stages, process workflows, return paths and consolidation/freeze points. |
| `workflow asset` | `supporting workflows` | Задает reusable bounded workflows, которые могут подключаться к methodology workflow или использоваться standalone. |
| `methodology asset` | `waterfall` | Задает process model разработки. |
| `rules pack` | `project-selected rules` | Подключает набор policy и operating rules. |
| `skills pack` | `project-selected skills` | Подключает набор reusable skills для работы с выбранной stack. |

Такой `composition pack` можно воспринимать как готовую methodology stack для разработки ПО.

## Что этот документ не делает

Этот документ не описывает:

- детальные process semantics [`workflow`](../terms/project/terms/workflow.md) и [`workflow-step`](../terms/project/terms/workflow-step.md);
- детальный storage layout каждого asset type;
- package manifest format для Agent Asset Manager;
- project-local installed asset inventory format;
- runtime materialization policy;
- version resolution algorithm.

## Связь с другими документами

Этот документ нужно читать вместе с:

- [`overview.md`](overview.md);
- [`layered-sot-and-materialization-model.md`](layered-sot-and-materialization-model.md);
- [`artifact-model.md`](artifact-model.md);
- [`documentation-lifecycle-layers.md`](assets/knowledge-lifecycle/documentation-lifecycle-layers.md).

## Canonical invariants

- HyperGraph управляет экосистемой composable assets, а не одной жестко зашитой методологией.
- `knowledge-lifecycle asset`, `task-management-system asset`, `terms-management-system asset`, `research-management-system asset`, `testing-system asset`, `traceability-system asset`, `workflow asset`, `methodology-workflow asset` и `methodology asset` являются разными asset types.
- composition pack может включать совместимый набор assets разных типов.
- task system и terms system не обязаны быть зашиты внутрь methodology asset.
- research-management system не обязана быть зашита внутрь methodology asset.
- testing system не обязана быть зашита внутрь methodology asset.
- traceability system не обязана быть зашита внутрь methodology asset или methodology-workflow asset.
- methodology asset может использовать существующие lifecycle, task-management, terms-management, research-management, testing, traceability and workflow assets, не владея ими.

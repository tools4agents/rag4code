# Agent-System Assets and Materialization Boundaries for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая спецификация границ между reusable source assets, project-owned context-entry artifacts и `agent-system` materialization targets  
> Role: Source of Truth для распределения Kilo-facing artifacts между `AGENTS.md`, `project/`, `.kilo/` и related layers без смешения source ownership

## 1. Назначение документа

Этот документ фиксирует boundaries между reusable assets и project-scoped artifacts для target `agent-system`.

Его задача - описать:
- какие artifacts остаются в reusable source layer;
- какие artifacts принадлежат project-owned context layer;
- какие artifacts являются `agent-system` runtime materialization targets;
- как это отражается на Kilo-specific filesystem layout;
- что не должно ошибочно считаться `rule`, `agent-role` или runtime output.

Этот документ не описывает:
- полную artifact taxonomy;
- process semantics workflow and roles;
- detailed interface contracts;
- heuristic project discovery;
- Kilo adapter implementation details.

## 2. Почему нужен отдельный boundary spec

В `Project Methodology Runtime` уже различаются:
- `agent-system`-agnostic assets;
- `agent-system`-specific assets;
- `agent-system materialization`.

Но этого distinction недостаточно, когда нужно materialize конкретный project-scoped runtime для Kilo.

Нужно отдельно зафиксировать:
- что именно попадает в `AGENTS.md` и `project/`;
- что уходит в `.kilo/rules/`, `.kilo/agent/`, `.kilo/command/` и `kilo.json`;
- что остается reusable source asset и не должно напрямую materialize как project file;
- где проходит граница между project-owned context и target runtime layer.

## 3. Базовое различение трех слоев

Для этого focused spec фиксируются три разных слоя.

### 3.1 Reusable source asset layer

Это слой reusable assets внутри HyperGraph catalog.

Сюда входят:
- `rules packs`;
- `skills packs`;
- `agent-role packs`;
- `reference packs`;
- `agent-system`-agnostic and `agent-system`-specific source artifacts.

Этот слой не зависит от одного конкретного проекта и не должен растворяться в project-local layout.

### 3.2 Project-owned context-entry layer

Это слой project-local artifacts, которые помогают человеку и агенту войти в корректный project context.

Сюда относятся:
- `AGENTS.md`;
- `project/index.md`;
- `project/entry-points.md`;
- `project/gitContext.md`;
- `project/techContext.md`;
- `project/codeStyle.md`.

Этот слой является project-owned guidance/config layer, а не reusable asset catalog и не runtime output.

### 3.3 Agent-system runtime/materialization layer

Это environment-facing layer, который реально потребляет target `agent-system`.

Для Kilo сюда относятся project-local artifacts вроде:
- `.kilo/rules/`;
- `.kilo/agent/`;
- `.kilo/command/`;
- `kilo.json`;
- другие Kilo-facing files, если они введены policy выбранного проекта.

Этот слой должен считаться materialization target, а не главным semantic owner layer.

## 4. Что относится к Kilo-specific project baseline

Для текущего baseline важно признать, что Kilo-facing project surface состоит из двух разных project-local групп.

### 4.1 Project-owned context-entry artifacts

Kilo читает их как часть project context, но они не являются `.kilo/` runtime directory.

Сюда относятся:
- `AGENTS.md`;
- `project/`.

Они отвечают за:
- routing;
- durable context;
- loading order;
- ownership split;
- nested context switching.

### 4.2 Kilo runtime/config artifacts

Это уже `.kilo/` and adjacent Kilo-facing layer.

Сюда относятся:
- `.kilo/rules/`;
- `.kilo/agent/`;
- `.kilo/command/`;
- `kilo.json`.

Они отвечают за:
- executable rules;
- agent projections;
- reusable commands/workflows в representation target system;
- runtime-facing Kilo configuration.

Главный invariant:
- не все Kilo-facing project files являются `.kilo/` files;
- `AGENTS.md` и `project/` образуют отдельный project-owned context-entry layer.

## 5. Что materialize в какие target locations

### 5.1 Rules packs

`Rules pack` materialize в Kilo-facing rule layer:
- project-local `rules` -> `.kilo/rules/`;
- global developer-level rules -> global Kilo config layer вне project repo.

Но governance, loading order и project navigation не должны без необходимости размываться в `.kilo/rules/`, если они принадлежат `AGENTS.md` или `project/`.

### 5.2 Agent-role packs

`Agent-role pack` materialize в Kilo-facing agent layer:
- `.kilo/agent/` для project-scoped agent artifacts.

При этом нужно сохранять distinction между:
- abstract reusable role semantics;
- `agent-system`-specific source asset для Kilo;
- project-local materialized agent artifact.

### 5.3 Workflow or command-like assets

Artifacts, которые для target system представляются как executable multi-step procedures, materialize в:
- `.kilo/command/`.

Важно:
- abstract `workflow` и Kilo command representation не равны друг другу;
- command layer является target-specific projection поверх broader process model.

### 5.4 Skills packs

`Skills pack` не обязан автоматически materialize в project-local Kilo filesystem layout.

Если target `agent-system` не имеет stable project-local representation для skills, то skills остаются:
- reusable source assets;
- or indirectly referenced by role, rule или command artifacts.

Следствие для текущего baseline:
- не нужно насильно придумывать project-local skill directory, пока target model не стабилизирован.

### 5.5 Project context entry artifacts

Artifacts вроде `AGENTS.md` и `project/*.md` не должны трактоваться как `rules pack materialization`.

Они образуют специальный project-owned context-entry layer:
- он Kilo-facing по факту consumption;
- но по смыслу это не `rule-doc`, не `agent-role pack` и не runtime command projection.

## 6. Что должно жить в `AGENTS.md`

`AGENTS.md` должен materialize или authorиться как router artifact.

Он должен содержать:
- краткий routing contract;
- high-level loading order;
- links на project-local entry points;
- instructions for `nested repo context switching`.

Он не должен содержать:
- полный engineering SoT;
- полный durable context проекта;
- большой rules corpus;
- task storage model во всех деталях.

## 7. Что должно жить в `project/`

`Project/` должен materialize или authorиться как durable context-entry layer.

Он должен содержать:
- repository boundaries;
- technical baseline;
- loading-order model;
- code style;
- migration notes and repository map, если они нужны.

Он не должен:
- подменять `docs/` как engineering SoT;
- подменять `operational_scope/` как execution layer;
- подменять `.kilo/rules/` как executable policy layer.

## 8. Что должно жить в `.kilo/rules/`

`.kilo/rules/` должен materialize или authorиться как executable policy layer.

Сюда относятся:
- project-local governance overlays;
- git behavior rules;
- task execution rules;
- documentation behavior rules;
- code execution guardrails and similar operational policies.

Но сюда не должны попадать:
- repository map;
- full tech context;
- glossary system;
- architecture canon;
- broad explanation of entry points, если для этого есть `project/entry-points.md`.

## 9. Что должно жить в `.kilo/agent/`

`.kilo/agent/` должен materialize или authorиться как Kilo-specific agent artifact layer.

Сюда относятся:
- target-specific agent artifacts для выбранных reusable roles;
- system prompts и local agent definitions в representation target system.

Но сюда не должны стекаться:
- reusable abstract role semantics как единственный source layer;
- generic process semantics workflow;
- project-wide navigation guidance.

## 10. Что должно жить в `.kilo/command/`

`.kilo/command/` должен materialize или authorиться как Kilo-specific command layer.

Сюда относятся:
- reusable command projections;
- multi-step procedures в shape, который понимает Kilo.

Но сюда не должны без необходимости попадать:
- все workflow проекта целиком;
- task storage model;
- project boundaries and SoT policy.

## 11. `kilo.json`

`Kilo.json` должен трактоваться как target-specific config artifact.

Он отвечает за:
- selection of Kilo runtime behavior, где это поддерживает target system;
- project-local configuration hooks для Kilo.

Он не должен трактоваться как:
- замена `AGENTS.md`;
- замена `project/` context layer;
- semantic owner layer reusable methodology assets.

## 12. Связь с global vs project config

Этот документ признает distinction между:
- `Global Agent-System Config SoT`;
- `Project Agent-System Config SoT`.

Следствие для Kilo:
- общие cross-project defaults должны жить в global Kilo layer;
- project repo должен хранить только project-specific context and runtime artifacts;
- reusable assets не должны копироваться в каждый project без необходимости.

## 13. Связь с `repository-context-entry-model`

Этот документ и [`Repository Context Entry Model for Project Methodology Runtime`](repository-context-entry-model.md) описывают смежные, но разные bounded contexts.

`Repository-context-entry-model` отвечает на вопросы:
- как агент входит в project context;
- какие файлы читать в каком порядке;
- как распределяется ownership между entry points.

Этот документ отвечает на вопросы:
- какие Kilo-facing artifacts являются source-like project guidance;
- какие являются runtime materialization targets;
- какие reusable packs materialize в какие Kilo layers.

## 14. Что пока не нужно поднимать в отдельный asset type

Этот документ не вводит новый asset type.

Он фиксирует boundaries между уже существующими классами:
- reusable packs;
- project-owned context-entry artifacts;
- agent-system-specific runtime materialization targets.

Если позже появятся alternative reusable systems для распределения artifacts между `AGENTS.md`, `project/`, `.kilo/` and other target layers, тогда можно обсуждать отдельный subsystem asset.

На текущем этапе достаточно focused spec.

## 15. Что этот документ не должен делать

Этот документ не должен:
- дублировать artifact model полностью;
- дублировать discovery policy;
- превращаться в Kilo adapter implementation manual;
- задавать glossary system;
- дублировать engineering architecture canon.

Если сюда начинают попадать low-level parser rules или полный list of fields для Kilo internal config, это означает нарушение boundaries.

## 16. Связь с другими каноническими документами

Этот документ нужно читать вместе с:
- [`Project Methodology Runtime Overview`](overview.md);
- [`Artifact Model for Project Methodology Runtime`](artifact-model.md);
- [`Layered SoT and Materialization Model for Project Methodology Runtime`](layered-sot-and-materialization-model.md);
- [`Interfaces and Storage for Project Methodology Runtime`](interfaces-and-storage.md);
- [`Repository Context Entry Model for Project Methodology Runtime`](repository-context-entry-model.md);
- [`agent-system-specific asset`](../terms/project/terms/agent-system-specific-asset.md);
- [`agent-system materialization`](../terms/project/terms/agent-system-materialization.md).

## 17. Canonical invariants

- reusable source assets, project-owned context-entry artifacts и runtime materialization targets являются разными слоями.
- `AGENTS.md` и `project/` образуют special project-owned context-entry layer и не должны автоматически считаться `rules pack materialization`.
- `.kilo/rules/`, `.kilo/agent/`, `.kilo/command/` и `kilo.json` относятся к Kilo-facing runtime/config layer.
- `rules pack`, `agent-role pack` и command-like projections materialize в разные target layers и не должны semantic collapse в один filesystem bucket.
- abstract `workflow` не равен Kilo command projection.
- abstract reusable role semantics не равны `.kilo/agent/` artifacts.
- `skills pack` не обязан materialize в project-local Kilo layout, пока не зафиксирована stable target representation.
- global Kilo config и project-local Kilo artifacts должны оставаться разными config layers.

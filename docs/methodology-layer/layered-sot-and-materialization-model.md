# Layered SoT and Materialization Model for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая модель слоев Source of Truth, resolved states и materialization states для `Project Methodology Runtime`  
> Role: Source of Truth для ownership model между внутренним каноном HyperGraph, конфигурацией `agent-system` и производными runtime states

## 1. Назначение документа

Этот документ фиксирует layered model для `Project Methodology Runtime`.

Он нужен, чтобы явно разделить:

- внутренний канон HyperGraph;
- reusable asset catalog;
- глобальную и project-specific конфигурацию выбранной [`agent-system`](../terms/project/terms/agent-system.md);
- производные resolved states;
- производные runtime materialization states.

Этот документ не описывает:

- process semantics [`workflow`](../terms/project/terms/workflow.md), [`workflow-step`](../terms/project/terms/workflow-step.md), [`step-vacancy`](../terms/project/terms/step-vacancy.md) и [`agent-role`](../terms/project/terms/agent-role.md);
- artifact taxonomy во всех деталях;
- graph DB layer, который связывает документацию, код и runtime через отдельный derived graph.

## 2. Canonical layers и derived states

В этой модели нужно жестко различать:

- canonical Source of Truth layers;
- derived resolved states;
- derived runtime materialization states.

`Source of Truth` владеет каноническим смыслом и конфигурацией.

Resolved state и materialization state:

- вычисляются из канонических слоев;
- могут быть rebuilt;
- не должны считаться semantic owner layer.

## 3. Canonical Source of Truth layers

Для первой итерации фиксируются четыре канонических слоя.

### 3.1 `HyperGraph Docs SoT`

Этот слой владеет:

- domain model HyperGraph;
- терминологией и glossary;
- сущностями и их границами;
- governance rules;
- layering rules;
- naming conventions.

Практически это соответствует `docs/` внутри HyperGraph repository.

### 3.2 `HyperGraph Asset Catalog SoT`

Этот слой владеет reusable assets, которые HyperGraph может устанавливать, резолвить и materialize.

Сюда входят:

- methodology packs;
- role packs;
- skill packs;
- rules packs;
- reference packs;
- другие reusable source artifacts для работы по определенной методологии разработки ПО.

На первой итерации этот catalog может существовать как набор nested git repositories внутри `assets/`.

### 3.3 `Global Agent-System Config SoT`

Этот слой хранит глобальные настройки выбранной [`agent-system`](../terms/project/terms/agent-system.md) для всех проектов конкретного разработчика.

Сюда относятся:

- global defaults;
- global profiles;
- global activation preferences;
- global config, не привязанный к одному проекту.

### 3.4 `Project Agent-System Config SoT`

Этот слой хранит project-specific конфигурацию выбранной [`primary-agent-system`](../terms/project/terms/primary-agent-system.md).

Сюда относятся:

- project-specific selection and overrides;
- project-level bindings;
- project-specific activation rules;
- portable config для materialization внутри конкретного проекта.

## 4. Derived states

Поверх канонических слоев строятся четыре производных состояния.

### 4.1 `Service-global Resolved State`

Это производное состояние, в котором сервис хранит результат разрешения глобальной конфигурации.

По смыслу этот слой ближе к `lock`-state, чем к authoring config.

### 4.2 `Global Runtime Materialization State`

Это производное состояние, в котором уже materialized глобальные runtime artifacts для выбранной `agent-system`.

### 4.3 `Service-project Resolved State`

Это производное состояние, в котором сервис хранит результат разрешения project config вместе с reusable assets и global defaults.

Этот слой также ближе к `lock`-state, чем к каноническому project config.

### 4.4 `Project Runtime Materialization State`

Это производное состояние, в котором уже materialized project runtime artifacts для выбранной `agent-system`.

Именно этот слой реально потребляет target environment внутри проекта.

## 5. Resolution order

Порядок разрешения должен быть таким:

1. `HyperGraph Docs SoT` задает domain and governance constraints.
2. `HyperGraph Asset Catalog SoT` задает доступные reusable assets.
3. `Global Agent-System Config SoT` задает global defaults.
4. `Project Agent-System Config SoT` задает project-specific selection и overrides.
5. Сервис строит `Service-global Resolved State` и `Service-project Resolved State`.
6. На их основе materialize `Global Runtime Materialization State` и `Project Runtime Materialization State`.

## 6. Relationship between internal canon and agent-system layers

HyperGraph сам по себе не является только runtime adapter.

Он одновременно:

- владеет собственным domain/governance canon;
- владеет reusable asset catalog;
- управляет конфигурацией для конкретной `agent-system`;
- строит resolved state;
- materialize runtime artifacts для target environment.

Следствие:

- `docs/` и `assets/` являются внутренним каноном HyperGraph;
- global/project `agent-system` configs являются managed config layers;
- runtime materialization не должна считаться частью канона HyperGraph.

## 7. Project and developer isolation

Для одного и того же проекта разные разработчики могут использовать разные `agent-system`.

Поэтому:

- проект не должен считаться навсегда привязанным к одной `agent-system`;
- у каждого developer context может быть собственная active [`primary-agent-system`](../terms/project/terms/primary-agent-system.md);
- developer-local runtime settings не должны без необходимости засорять основной project repo.

## 8. Packaging and distribution implications

Эта модель не требует одного конкретного механизма distribution.

На первой итерации reusable assets могут жить как nested git repositories inside `assets/`.

В дальнейшем asset catalog может развиться в более формальную package model, включая обычные Python packages и dependency resolution через package manager.

Но независимо от механизма distribution должны сохраняться те же semantic layers:

- canonical asset source;
- resolved state;
- materialized runtime state.

## 9. Что находится вне scope этого документа

Graph layer, который связывает документацию, код, tasks, contracts и runtime через graph DB, не считается частью этого focused spec.

На текущем этапе это отдельный следующий слой, который будет использовать результаты `Project Methodology Runtime`, но не должен смешиваться с базовой SoT/materialization model.

## 10. Связь с другими каноническими документами

Этот документ нужно читать вместе с:

- [`Project Methodology Runtime Overview`](overview.md);
- [`Principles for Project Methodology Runtime`](principles.md);
- [`Artifact Model for Project Methodology Runtime`](artifact-model.md);
- [`Workflow and Roles for Project Methodology Runtime`](workflow-and-roles.md);
- [`Interfaces and Storage for Project Methodology Runtime`](interfaces-and-storage.md);
- [`Naming Conventions for Project Methodology Runtime`](naming-conventions.md).

## 11. Canonical invariants

Для первой итерации считаются обязательными следующие invariants:

- `HyperGraph Docs SoT` и `HyperGraph Asset Catalog SoT` являются внутренним каноном HyperGraph;
- global и project `agent-system` configs являются отдельными canonical config layers;
- resolved states являются derived и rebuildable;
- runtime materialization states являются derived и rebuildable;
- runtime-facing artifacts не должны считаться Source of Truth;
- project не должен считаться навсегда привязанным к одной `agent-system`;
- graph DB layer не должен смешиваться с базовой SoT/materialization model этого документа.

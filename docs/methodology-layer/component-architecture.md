# Component Architecture for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая component-level архитектура первой итерации `Project Methodology Runtime`  
> Role: Source of Truth для состава компонентов, их ответственности и основных взаимодействий

## Назначение

Этот документ фиксирует component architecture первой пробной итерации `Project Methodology Runtime`.

Он нужен, чтобы:

- определить минимальный состав компонентов системы;
- развести их ответственности и границы реализации;
- подготовить основу для C4/C3-диаграмм и первой PoC;
- зафиксировать путь materialization под Kilo без ухода в code-level design.

## Граница системы

В первой итерации `Project Methodology Runtime` рассматривается как один HyperGraph subsystem, который:

- реализует поведение, заданное `HyperGraph Docs SoT`, и читает `HyperGraph Asset Catalog SoT`;
- читает `Global Agent-System Config SoT` и `Project Agent-System Config SoT`;
- строит resolved state;
- materialize runtime для выбранной [`primary-agent-system`](../terms/project/terms/primary-agent-system.md);
- дает navigation and control interfaces через MCP и Web UI.

## Компоненты первой итерации

### 1. `Asset Catalog Reader`

Отвечает за чтение reusable assets из `assets/` и извлечение их metadata, identities и references.

### 2. `Project Config Reader`

Отвечает за чтение project-scoped config и project-local selections для выбранной `agent-system`.

### 3. `Global Config Reader`

Отвечает за чтение global config для выбранной `agent-system`.

### 4. `Discovery and Classification Engine`

Отвечает за `manual-hybrid discovery`, classification project roots и подготовку входа для дальнейшего indexing/resolution.

### 5. `Asset Resolver`

Отвечает за выбор concrete assets и compatible compositions на основе:

- asset catalog;
- global config;
- project config;
- selected `agent-system`.

### 6. `Resolved State Builder`

Отвечает за сборку:

- `Service-global Resolved State`;
- `Service-project Resolved State`.

### 7. `Runtime Materializer`

Отвечает за materialization runtime-facing artifacts для target `agent-system`.

На первой итерации именно он создает `Project Runtime Materialization State` для Kilo.

### 8. `Traceability Indexer`

Отвечает за подготовку derived navigation structures и provenance references для MCP/Web UI.

Полный graph layer в первой итерации еще не считается завершенным bounded context, но navigation index нужен уже сейчас.

### 9. `MCP Interface`

Дает агенту navigation, lookup и controlled operations поверх file-first SoT и resolved state.

### 10. `Web UI Interface`

Дает разработчику graph-and-config-first view, sync/materialization actions и explainability.

## Основные взаимодействия

Базовый поток первой итерации такой:

1. `Asset Catalog Reader`, `Global Config Reader` и `Project Config Reader` читают входные слои.
2. `Discovery and Classification Engine` определяет project scope.
3. `Asset Resolver` выбирает compatible assets и compositions.
4. `Resolved State Builder` строит service-level resolved state.
5. `Runtime Materializer` materialize runtime под target `agent-system`.
6. `Traceability Indexer` подготавливает navigation/explainability layer.
7. `MCP Interface` и `Web UI Interface` дают доступ к результату.

## Минимальные implementation boundaries для первой PoC

Для первой PoC достаточно реализовать минимальный вертикальный срез:

- чтение `assets/`;
- чтение project config с `primary_agent_system = kilo`;
- базовый `Asset Resolver` для composition из `document-driven-development`, `task-map`, `terms-map` и минимального Kilo-compatible role asset;
- `Resolved State Builder` для project-level resolution;
- `Runtime Materializer` для Kilo;
- минимальный MCP-facing lookup для проверки результата.

## Kilo materialization path первой итерации

Для первой итерации path под Kilo такой:

- source layers задают reusable assets и config;
- `Asset Resolver` выбирает Kilo-compatible assets;
- `Resolved State Builder` фиксирует итоговую composition для проекта;
- `Runtime Materializer` раскладывает Kilo-facing runtime artifacts в project-scoped runtime;
- результат должен быть rebuildable из SoT и config layers.

## Что пока вне scope

В этот документ пока не входят:

- code-level class design;
- package manager implementation;
- full graph DB architecture;
- release publishing pipeline;
- детальные MCP contracts.

## Связь с другими документами

- [`Project Methodology Runtime Overview`](overview.md)
- [`Layered SoT and Materialization Model for Project Methodology Runtime`](layered-sot-and-materialization-model.md)
- [`Interfaces and Storage for Project Methodology Runtime`](interfaces-and-storage.md)
- [`Project Discovery for Project Methodology Runtime`](project-discovery.md)
- [`Asset Taxonomy and Composition Model for Project Methodology Runtime`](asset-taxonomy-and-composition-model.md)

## Canonical invariants

- component architecture первой итерации должна оставаться file-first;
- runtime не должен читать `HyperGraph Docs SoT` напрямую; `HyperGraph Docs SoT` задает реализацию и архитектурные границы, а не runtime input channel;
- resolver и materializer не должны становиться semantic owner layers;
- runtime materialization должна быть rebuildable;
- Kilo path первой итерации должен быть узким vertical slice, а не полной multi-agent implementation;
- MCP и Web UI используют одни и те же canonical and resolved layers, а не собственные competing sources of truth.

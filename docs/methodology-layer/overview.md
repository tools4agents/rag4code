# Project Methodology Runtime Overview

> Status: Draft  
> Scope: общий обзор слоя `Project Methodology Runtime`  
> Role: входная точка для человека и агента перед чтением специализированных спецификаций

## 1. Зачем нужен этот слой

`Project Methodology Runtime` — это слой HyperGraph, который управляет методологическими артефактами проекта как отдельным предметным доменом.

В контексте этого проекта методология нужна не просто как набор текстовых правил, а как формализованная модель разработки ПО вместе с командой ИИ-агентов.

Ее задача — зафиксировать:
- центральный `methodology workflow` проекта;
- reusable `agent-role` как профиль исполнителя;
- `step-vacancy` как назначение роли на конкретный шаг workflow;
- подмножества `rules`, `skills` и `MCP tools`, назначаемые ролям;
- связанные `workflow`, которые могут использоваться внутри проекта как локальные многошаговые протоколы;
- project-level выбор methodology, profiles, discovery decisions и `primary_agent_system`.

Сам слой связывает между собой:
- канонические `markdown` и `yaml` artifacts;
- project-level methodology intent;
- environment-facing runtime projection для agent system;
- derived graph representation для navigation, provenance и traceability.

Слой нужен, чтобы methodology проекта была:
- переносимой;
- воспроизводимой;
- навигируемой;
- пригодной и для человека, и для агента;
- не завязанной на machine-specific storage paths.

## 2. Что слой должен уметь

На уровне архитектуры этот слой должен:
- хранить и резолвить `Project Portable Intent`;
- работать с `Central methodology catalog` как с переиспользуемым источником methodology artifacts;
- хранить reusable role packs с core `agent-role` и adapter projections;
- задавать и поддерживать `methodology workflow` проекта;
- связывать шаги `methodology workflow` с `step-vacancy`, а через них — с `agent-role`, rules, skills и `MCP tools`;
- хранить внутри methodology описания отдельных `workflow`, используемых как рабочие многошаговые протоколы;
- materialize `project-scoped runtime` для конкретной agent environment, выбранной через `primary_agent_system`;
- строить `graph projection` в ArcadeDB как derived state;
- поддерживать `manual-hybrid discovery` для project boundaries;
- обнаруживать drift между desired state и materialized runtime state;
- выполнять `reconcile`, если projection или runtime вышли из согласованного состояния.

## 3. Основные инварианты

Для этого слоя зафиксированы следующие архитектурные инварианты:

### 3.1 File-first Source of Truth

`Source of Truth` для methodology artifacts — это `markdown` и `yaml` files.

Database не является каноническим источником. Она хранит derived representation, пригодную для navigation, traceability и explainability.

### 3.2 Project portability

Проект хранит только `portable references` и не должен зависеть от machine-specific absolute paths.

Это значит, что project metadata может хранить:
- `methodology_id`;
- `version_ref`;
- `artifact_id`;
- `profile_id`;
- `role_id`;
- `primary_agent_system`;
- project-relative discovery decisions.

Но project metadata не должна хранить physical path до `Central methodology catalog` или service-local operational storage.

### 3.3 Runtime как projection

Environment-facing runtime должен рассматриваться как `Runtime Materialization State`, а не как канонический source layer.

Для Kilo Code это означает, что файлы в `.kilocode/` и смежные runtime artifacts — это materialized projection, которую можно rebuild.

### 3.4 Unified project-scoped runtime

Для агента runtime должен быть единым `project-scoped runtime`.

Различие между global и project уровнями полезно на уровне source layering, но agent-facing consumption должен видеть один согласованный local layer.

### 3.5 Explicit discovery policy

`Project Discovery` не должен быть скрытой эвристикой.

Для первой итерации используется `manual-hybrid discovery`:
- сервис ищет candidates;
- разработчик подтверждает final classification;
- результат сохраняется как project-owned decision;
- автоматического rediscovery без явного запроса нет.

## 4. Границы слоя

Этот слой отвечает за:
- methodology artifacts;
- roles, role packs, rules, skills и related metadata;
- workflow assignment layer через `step-vacancy`;
- project selection и activation policy;
- выбор `primary_agent_system` и adapter projection policy;
- discovery classification для project boundaries;
- runtime materialization;
- graph projection;
- drift detection и `reconcile`.

Этот слой не должен смешивать в одном документе:
- архитектурный обзор;
- терминологический glossary;
- focused domain specs;
- implementation contracts.

Поэтому документация слоя разделена на несколько уровней.

## 5. Карта документации слоя

### 5.1 Терминология

- `docs/terms/common/terms_map.md` — каноническая карта общих терминов
- `docs/terms/project/terms_map.md` — каноническая карта project-specific терминов

### 5.2 Обзор слоя

- этот файл — `docs/methodology-layer/overview.md`
- `docs/methodology-layer/principles.md` — производные архитектурные принципы и patterns решений именно для этого слоя

### 5.3 Focused specs

- `docs/methodology-layer/artifact-model.md` — `MethodologyArtifact`, `MethodologyArtifactType`, baseline types, artifact families и role packs как packaging boundary
- `docs/methodology-layer/workflow-and-roles.md` — `agent-role`, `workflow`, `workflow-step`, `step-vacancy` и process semantics workflow assignment
- `docs/methodology-layer/component-architecture.md` — component-level архитектура первой итерации, boundaries и основной materialization flow
- `docs/methodology-layer/asset-taxonomy-and-composition-model.md` — asset types, composition packs и свободная композиция reusable assets
- `docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md` — concrete `knowledge-lifecycle asset` `document-driven-development` и его three-layer documentation flow
- `docs/methodology-layer/assets/task-management/task-map.md` — concrete `task-management-system asset` `task-map` и baseline task storage model
- `docs/methodology-layer/assets/terms-management/terms-map.md` — concrete `terms-management-system asset` `terms-map` и scoped terminology maps
- `docs/methodology-layer/assets/research-management/research-tree.md` — concrete `research-management-system asset` `research-tree` и baseline tree-shaped research storage model
- `docs/methodology-layer/assets/research-management/research-branches.md` — structure topic roots, branch dossiers и branch portfolio navigation
- `docs/methodology-layer/assets/research-management/research-traceability.md` — identifier families, traceability chain и grep-friendly metadata placement для research tree
- `docs/methodology-layer/assets/testing-system/test-map.md` — concrete `testing-system asset` `test-map` и baseline testing documentation model
- `docs/methodology-layer/assets/testing-system/test-suites.md` — suite page structure, implementation roots и search-boundary conventions
- `docs/methodology-layer/assets/testing-system/test-case-traceability.md` — identifier families, traceability chain и code-level metadata placement
- `docs/methodology-layer/repository-context-entry-model.md` — system of project context entry points, loading order, ownership boundaries и `nested repo context switching`
- `docs/methodology-layer/agent-system-assets-and-materialization-boundaries.md` — boundaries между reusable source assets, project-owned context-entry artifacts и target `agent-system` materialization layers
- `docs/methodology-layer/layered-sot-and-materialization-model.md` — canonical SoT layers, resolved states и runtime materialization model
- `docs/methodology-layer/interfaces-and-storage.md` — interface model, storage boundaries, portability и runtime projection policy
- `docs/methodology-layer/project-discovery.md` — `manual-hybrid discovery`, classification policy и минимальный graph contract
- `docs/methodology-layer/naming-conventions.md` — naming rules для glossary terms, pack layout, Python identifiers и `agent-system`-related namespaces

### 5.4 Patterns

- `docs/methodology-layer/patterns/index.md` — index reusable design patterns для этого слоя
- `docs/methodology-layer/patterns/reviewable-automation-pattern.md` — collaboration loop между ИИ-агентом и deterministic algorithm/tool по схеме `plan -> review -> apply -> verify`

### 5.5 Contracts

- `docs/contracts/` — отдельный слой контрактов

Контракты должны описывать конкретные schemas, MCP operations, sync lifecycle и другие implementation-facing boundaries, но не дублировать архитектурные объяснения из overview и focused specs.

## 6. Рекомендуемый маршрут чтения

Для человека и агента рекомендуется одинаковый маршрут чтения:

1. прочитать `docs/methodology-layer/overview.md`;
2. открыть `docs/terms/common/terms_map.md` и `docs/terms/project/terms_map.md`, если встречаются незнакомые или нагруженные термины;
3. перейти только в релевантный focused spec;
4. открыть конкретный contract в `docs/contracts/` только когда нужна implementation detail.

Это и есть целевой `lazy loading` и `progressive disclosure` подход для слоя methodology runtime.

## 7. Как распределяется ответственность между документами

Чтобы избежать дублирования, каждый документ имеет собственную ответственность:

- `overview.md` объясняет зачем слой существует, какие у него инварианты и как устроена карта документации;
- `artifact-model.md` отвечает только за meta-model artifacts, baseline types, artifact families и role packs как packaging boundary;
- `workflow-and-roles.md` отвечает только за process semantics `agent-role`, `workflow`, `workflow-step`, `step-vacancy` и workflow assignment layer;
- `component-architecture.md` отвечает только за состав компонентов системы, их boundaries и основной runtime flow первой итерации;
- `asset-taxonomy-and-composition-model.md` отвечает только за типы reusable assets, composition packs и модель свободной композиции;
- `assets/knowledge-lifecycle/documentation-lifecycle-layers.md` отвечает только за concrete `knowledge-lifecycle asset` `document-driven-development`;
- `assets/task-management/task-map.md` отвечает только за concrete `task-management-system asset` `task-map`;
- `assets/terms-management/terms-map.md` отвечает только за concrete `terms-management-system asset` `terms-map`;
- `assets/research-management/research-tree.md` отвечает только за concrete `research-management-system asset` `research-tree` и baseline research index model;
- `assets/research-management/research-branches.md` отвечает только за structure topic roots, branch pages и portfolio navigation внутри research tree;
- `assets/research-management/research-traceability.md` отвечает только за identifier conventions, target traceability chain и grep-friendly metadata placement для research tree;
- `assets/testing-system/test-map.md` отвечает только за concrete `testing-system asset` `test-map` и baseline test index model;
- `assets/testing-system/test-suites.md` отвечает только за suite page structure, implementation roots и search-boundary conventions;
- `assets/testing-system/test-case-traceability.md` отвечает только за identifier conventions, target traceability chain и code-level metadata placement;
- `repository-context-entry-model.md` отвечает только за system of project context entry points, loading order, structure + navigation + ownership и `nested repo context switching`;
- `agent-system-assets-and-materialization-boundaries.md` отвечает только за boundaries между reusable assets, project-owned context-entry artifacts и target `agent-system` materialization layers;
- `layered-sot-and-materialization-model.md` отвечает только за ownership model между внутренним каноном HyperGraph, `agent-system` config layers и derived runtime states;
- `interfaces-and-storage.md` отвечает только за interfaces, `Source of Truth`, portability и storage boundary;
- `project-discovery.md` отвечает только за discovery policy, classification model и минимальный graph contract;
- `naming-conventions.md` отвечает только за naming rules для human-facing terms, filesystem layout и Python-facing identifiers;
- `patterns/index.md` отвечает только за navigation по reusable patterns этого слоя;
- `patterns/reviewable-automation-pattern.md` отвечает только за reusable collaboration pattern между ИИ-агентом и deterministic algorithm/tool;
- `docs/contracts/` отвечает только за explicit contracts.

Если определение повторяется в нескольких местах, источником истины становятся `docs/terms/common/terms_map.md` и `docs/terms/project/terms_map.md`, а остальные документы должны ссылаться на них, а не копировать полное объяснение.

## 8. Что должно исчезнуть после миграции из planning docs

После миграции из старых planning documents должны исчезнуть:
- крупные повторяющиеся блоки про `Source of Truth`;
- дублирование объяснений про Web UI и MCP в нескольких файлах;
- повторяющиеся формулировки про `Central methodology catalog`;
- конкурирующие описания `manual-hybrid discovery`;
- смешение `agent-role`, `step-vacancy` и workflow step semantics в одном определении;
- повторяющиеся объяснения про `project-scoped runtime` и adapter projections;
- смешение архитектурного обзора и contract-level деталей в одном документе.

## 9. Связь с общей архитектурой проекта

Этот слой не существует изолированно. Он продолжает идеи из:
- `operational_scope/ideas/project-first-model-and-storage.md`;
- `operational_scope/ideas/HyperGraph_vision.md`;
- `operational_scope/ideas/integrated_knowledge_graph_schema.md`;
- `docs/adr/0001-arcadedb-as-unified-storage-for-mvp.md`.

Но эти документы задают более широкий контекст. Каноническое описание именно слоя `Project Methodology Runtime` должно жить в `docs/methodology-layer/`.

## 10. Целевое состояние документации слоя

После миграции documentation package для этого слоя должен стать:
- компактным на входе;
- многоуровневым;
- пригодным для lazy navigation;
- удобным для человека;
- удобным для агента;
- свободным от конкурирующих planning versions.

Этот файл является канонической входной точкой в documentation package слоя `Project Methodology Runtime`.

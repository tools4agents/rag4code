# Artifact Model for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая meta-model спецификация для artifacts слоя `Project Methodology Runtime`  
> Role: Source of Truth для `MethodologyArtifact`, `MethodologyArtifactType`, baseline artifact families и packaging boundaries

## 1. Назначение документа

Этот документ фиксирует каноническую модель артефактов для слоя `Project Methodology Runtime`.

Его задача — описать:
- какие базовые сущности используются для modeling methodology artifacts;
- как различаются artifact instance и artifact type;
- какие baseline artifact families считаются обязательными для первой итерации;
- как устроены reusable artifact families и packaging boundaries;
- какие invariants должна сохранять система при расширении vocabulary artifacts.

Этот документ не описывает:
- process semantics `workflow`, `workflow-step`, `step-vacancy` и `agent-role` как участников workflow execution;
- storage boundaries и runtime states;
- discovery policy;
- contract policy;
- adapter-specific materialization details.

Для этих тем источниками истины являются отдельные focused specs слоя.

## 2. Почему нужен отдельный artifact model

`Project Methodology Runtime` не должен быть жестко привязан к короткому списку специальных сущностей вроде `ADR`, `Rule`, `Skill` или `Mode`.

Вместо этого слой должен поддерживать extensible model, где:
- есть общая сущность artifact;
- есть конфигурируемое описание artifact type;
- разные methodology могут добавлять новые families и specializations без переписывания core domain.

Это дает:
- extensibility без постоянного изменения core model;
- единый vocabulary для graph traceability;
- предсказуемые authoring conventions;
- явные boundaries между semantic artifact, projection artifact и support artifact.

## 3. Core meta-model

### 3.1 `MethodologyArtifact`

`MethodologyArtifact` — это конкретный artifact instance внутри methodology catalog, project intent или related documentation layer.

Минимально artifact должен позволять ответить на вопросы:
- что это за artifact;
- к какому type он относится;
- где он лежит относительно своего logical root;
- каков его текущий lifecycle status;
- из какого source layer он происходит;
- как он связан с другими artifacts.

Рекомендуемый минимальный набор полей:
- `artifact_id`
- `artifact_type_id`
- `title`
- `status`
- `format`
- `rel_path`
- `source_layer`
- `version_ref`
- `content_hash`
- `template_ref`
- `metadata`

### 3.2 `MethodologyArtifactType`

`MethodologyArtifactType` — это конфигурируемое описание семейства artifacts.

Именно `MethodologyArtifactType` определяет:
- semantic category artifact;
- ожидаемый storage format;
- default authoring conventions;
- graph semantics;
- validation expectations;
- high-level render policy.

Рекомендуемый минимальный набор полей:
- `artifact_type_id`
- `name`
- `description`
- `storage_format`
- `default_roots`
- `template_schema`
- `graph_binding`
- `render_policy`
- `validation_policy`
- `layering_policy`

### 3.3 Artifact instance vs artifact type

Нужно жестко различать два уровня:

- `MethodologyArtifactType` отвечает на вопрос, что это за family of artifacts и по каким правилам она живет;
- `MethodologyArtifact` отвечает на вопрос, какой конкретный artifact существует в catalog, project layer или documentation package.

Следствие:
- новые artifacts не должны требовать обязательного расширения core classes;
- новые types могут вводиться как configuration-level vocabulary;
- граф, валидация и templates должны опираться на type model, а не на hardcoded list of kinds.

## 4. Что обязан описывать `MethodologyArtifactType`

Каждый artifact type должен описывать по меньшей мере пять измерений.

### 4.1 Semantic category

Type должен фиксировать, что именно представляет artifact family.

Типичные примеры semantic categories:
- narrative methodology artifact;
- glossary artifact;
- rule artifact;
- skill artifact;
- role artifact;
- workflow artifact;
- contract artifact;
- decision artifact;
- test-related artifact.

### 4.2 Storage format expectation

На первой итерации достаточно поддерживать file-first baseline:
- `markdown`
- `yaml`

Этого хватает для:
- human-readable documentation;
- reusable packs;
- project-portable configuration;
- machine-readable schemas и projections.

### 4.3 Authoring contract

Type должен задавать минимальные expectations к authoring:
- recommended frontmatter или metadata fields;
- expected sections;
- optional sections;
- identifier convention;
- traceability convention.

Задача type model — описывать не только хранение, но и shape authoring expectations.

### 4.4 Graph semantics

Type должен задавать, как artifact family входит в derived graph.

Это включает:
- возможные vertex labels;
- допустимые edge families;
- preferred traceability identifiers;
- минимальные navigation expectations.

Artifact model не обязан описывать все будущие graph contracts по каждому subtype, но должен фиксировать, что graph semantics являются property artifact type, а не ad hoc знанием конкретного документа.

### 4.5 Render policy

Type должен задавать high-level policy materialization:
- artifact только индексируется;
- artifact используется как source without direct materialization;
- artifact materializes как самостоятельный runtime artifact;
- artifact materializes через adapter transformation;
- artifact участвует в aggregation pipeline.

При этом детальные runtime concerns не принадлежат этому документу. Здесь фиксируется только сам факт, что render policy является частью type model.

## 5. Baseline artifact types первой итерации

На первой итерации фиксируются четыре baseline artifact types.

### 5.1 `methodology-doc`

Используется для narrative documentation слоя методологии.

Сюда относятся:
- overview documents;
- principles documents;
- focused specs;
- canonical process explanations;
- другие project methodology docs, не являющиеся glossary, contract или rule artifact.

### 5.2 `rule-doc`

Используется для описания правил, governance constraints и operating conventions.

Сюда относятся:
- project rules;
- workflow rules;
- quality or process guardrails;
- policy-like documentation artifacts.

### 5.3 `skill-doc`

Используется для reusable skill artifacts.

Сюда относятся:
- skill definitions;
- trigger and protocol descriptions;
- input and output expectations;
- related usage guidance.

### 5.4 `agent-role`

Используется для reusable role artifacts.

Важно:
- `agent-role` является baseline artifact type;
- это не равно конкретному runtime mode;
- adapter-specific projection не подменяет core role artifact;
- semantic usage роли внутри workflow описывается вне этого документа.

Artifact model фиксирует `agent-role` как artifact family и baseline type, но не заменяет process-level спецификацию роли.

## 6. Допустимые расширения vocabulary

Поверх baseline types методология может вводить новые `MethodologyArtifactType` без изменения core model.

Типичные кандидаты на extension:
- `adr`
- `term`
- `contract`
- `test-suite`
- `workflow-step`
- `workflow-overview`
- `acceptance-criteria`
- `quality-gate`
- `definition-pack`
- `projection-profile`

Это означает, что конкретная methodology может собирать свой artifact vocabulary как конфигурационную надстройку над общей meta-model.

## 7. Artifact families и ownership boundaries

Artifact model владеет не отдельными workflow semantics, а artifact families как структурными единицами documentation and runtime ecosystem.

В рамках этого документа важно зафиксировать следующие artifact families:
- methodology documentation artifacts;
- rule artifacts;
- skill artifacts;
- role artifacts;
- workflow artifacts как family of artifacts;
- contract artifacts;
- support artifacts вроде notes, mappings и related metadata.

Ownership этого документа распространяется на:
- vocabulary artifact families;
- distinction между core artifact и support artifact;
- distinction между reusable artifact и project-specific instance;
- packaging boundary для reusable artifact families.

## 8. Reusable artifacts и project-specific instances

Нужно различать:
- reusable artifact, который может жить в catalog и переноситься между проектами;
- project-specific binding, override или selection;
- runtime-facing projection, который является derived representation.

Следствие:
- reusable semantics не должны растворяться в project-local naming;
- project-level decisions должны ссылаться на reusable artifacts, а не копировать их без необходимости;
- runtime artifacts не должны считаться каноническим источником смысла.

## 9. `role pack` как artifact family и packaging boundary

В этом документе фиксируется ownership для `role pack` как artifact family.

`Role pack` — это packaging boundary, которая объединяет связанные artifacts одной reusable role unit.

Внутри `role pack` могут существовать:
- core role artifact;
- adapter-specific projection artifacts;
- human-readable docs;
- support metadata.

Это не должно автоматически распространяться на все reusable packs.

Для `agent-system`-agnostic packs baseline другой:
- они используются как общий reusable source layer для всех `agent-system`;
- они не должны содержать внутри себя `agent-system`-specific assets;
- system-specific assets должны выделяться в отдельную artifact family или separate pack structure.

Важно:
- packaging boundary не отменяет semantic boundary;
- core role artifact и projection artifact остаются разными artifacts;
- physical proximity файлов не должна трактоваться как semantic collapse.

Этот документ владеет:
- понятием `role pack` как artifact family;
- pack structure на уровне artifact model;
- местом core role artifact и sibling projection artifacts внутри pack.

Но этот документ не описывает process semantics использования роли в workflow. Это responsibility другого focused spec.

## 10. High-level graph implications

Artifact model должен быть совместим с graph-backed traceability.

Это означает:
- artifact family должна иметь устойчивую identity model;
- type model должна поддерживать predictable navigation;
- связи между artifact instance и artifact type должны быть recoverable;
- reusable artifacts, packs и projections должны быть различимы в derived graph.

При этом точные graph contracts для отдельных bounded contexts могут быть формализованы позже в contract layer или в других focused specs.

## 11. Что этот документ принципиально не делает

Этот документ не должен:
- описывать `workflow -> workflow-step -> step-vacancy -> agent-role` как process semantics;
- определять storage states вроде `Catalog Source of Truth` и `Runtime Materialization State`;
- описывать Web UI или MCP interfaces;
- задавать discovery policy;
- дублировать contract policy из `docs/contracts/README.md`.

Если этот документ начинает описывать runtime layers, project discovery или handoff semantics workflow, это означает нарушение boundaries.

## 12. Связь с другими каноническими документами

Этот документ нужно читать вместе с:
- `docs/methodology-layer/overview.md` как обзором слоя;
- `docs/methodology-layer/principles.md` как набором guiding principles;
- `docs/methodology-layer/workflow-and-roles.md` как process-level spec;
- `docs/methodology-layer/interfaces-and-storage.md` как storage and interface boundary spec;
- `docs/methodology-layer/project-discovery.md` как discovery policy spec;
- `docs/contracts/README.md` как contract policy layer.

## 13. Canonical invariants

Для первой итерации migration baseline считаются обязательными следующие invariants:
- artifact model строится через `MethodologyArtifact` и `MethodologyArtifactType`, а не через жесткий список hardcoded kinds;
- baseline artifact types включают как минимум `methodology-doc`, `rule-doc`, `skill-doc` и `agent-role`;
- reusable artifact families должны оставаться отличимыми от project-specific bindings и runtime projections;
- `role pack` является artifact-oriented packaging boundary;
- canonical pack structure и artifact family semantics не должны определяться process-level документом;
- contract policy не принадлежит artifact model;
- runtime details и storage states не принадлежат artifact model.

## 14. Целевое назначение для миграции legacy docs

При миграции legacy planning package этот документ должен стать канонической точкой сборки для:
- meta-model artifacts;
- baseline artifact types;
- extensible type vocabulary;
- reusable artifact families;
- role pack как packaging boundary.

После завершения миграции именно этот файл должен заменить прежние legacy explanations про artifact model и связанные временные planning formulations.

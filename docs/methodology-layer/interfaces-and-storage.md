# Interfaces and Storage for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая спецификация interface boundaries, storage layers и runtime projection policy для `Project Methodology Runtime`  
> Role: Source of Truth для interface model, portability rules и границ между source, project intent, service-local state и runtime materialization

## 1. Назначение документа

Этот документ фиксирует границы взаимодействия и хранения для слоя `Project Methodology Runtime`.

Его задача — описать:
- какие interfaces предоставляет слой;
- где проходит граница между каноническими artifacts, project intent и runtime state;
- как обеспечивается portability проекта;
- как работает adapter projection policy;
- как связаны file-first authoring, graph navigation и runtime materialization.

Этот документ не описывает:
- artifact meta-model и pack structure;
- process semantics `workflow`, `workflow-step`, `step-vacancy` и `agent-role`;
- discovery classification rules;
- детальную contract policy.

## 2. Interface model

`Project Methodology Runtime` проектируется как file-first слой с несколькими интерфейсами поверх одного и того же semantic baseline.

На первой итерации фиксируются три основных interface families:
- MCP interface для агента;
- Web UI для разработчика;
- file-based workflow как базовый способ authoring и versioning.

Важный invariant:
- ни MCP, ни Web UI не должны становиться конкурирующим Source of Truth;
- канонический source layer остается file-based.

## 3. File-first workflow как базовый Source of Truth

Каноническим Source of Truth для methodology artifacts являются files.

На первой итерации это означает:
- markdown используется для human-readable specification and methodology artifacts;
- yaml используется для portable config и machine-readable support artifacts;
- runtime-facing artifacts считаются projections, а не каноническим слоем смысла.

Сервис должен:
- читать canonical files;
- индексировать их;
- строить derived graph representation;
- materialize runtime projections;
- помогать с audit и reconcile.

Но сервис не должен подменять собой базовую файловую работу разработчика.

## 4. MCP interface

### 4.1 Назначение MCP

MCP interface нужен агенту для navigation, traceability и explainability внутри project methodology graph.

Агент через MCP должен уметь:
- понимать свою активную роль или связанный role context;
- находить artifacts по identifier;
- получать путь к source artifact;
- видеть связанные rules, skills, contracts, ADR, tests и project references;
- перемещаться по graph relationships между artifacts;
- по запросу разработчика инициировать controlled updates methodology artifacts.

### 4.2 Что важно на первой итерации

На первой итерации MCP важен прежде всего как navigation and traceability interface.

Write operations допустимы, но не должны становиться главным сценарием. Приоритет — explainable graph navigation и безопасная работа поверх file-first SoT.

## 5. Web UI

### 5.1 Основная роль Web UI

Web UI нужен разработчику-человеку для:
- graph navigation;
- project configuration;
- запуска sync, audit и materialization;
- понимания provenance и runtime state;
- получения path к нужному artifact file.

### 5.2 Что Web UI не обязан делать на первой итерации

Web UI не обязан:
- быть полноценным markdown editor;
- заменять IDE;
- хранить уникальное знание, которого нет в files;
- становиться primary environment for versioning.

Иначе слой начнет дублировать file-based workflow вместо усиления его через navigation and configuration.

## 6. Four-layer storage model

Для этого слоя фиксируется модель из четырех состояний.

### 6.1 `Catalog Source of Truth`

Это reusable source layer.

Он содержит:
- reusable methodology artifacts;
- reusable role artifacts и projection artifacts;
- reusable rules, skills, terms и related source files;
- reusable packs и support docs;
- source material, пригодный для git-backed versioning.

Ключевые свойства:
- это canonical source layer для reusable artifacts;
- слой не зависит от конкретного проекта;
- project не хранит machine-specific path до этого catalog.

### 6.2 `Project Portable Intent`

Это переносимый слой project-owned решений.

Он содержит:
- selected methodology references;
- version references;
- project-level bindings;
- selected roles, profiles или packs;
- project-specific overrides, если они допускаются policy;
- `primary_agent_system`;
- portable discovery decisions и related references.

Ключевые свойства:
- хранится в project scope;
- должен оставаться machine-independent;
- хранит references и intent, а не physical resolution service storage.

### 6.3 `Service-local Runtime State`

Это internal operational representation сервиса.

Он содержит:
- resolved runtime records;
- cache и local indices;
- job metadata;
- sync snapshots;
- diagnostics;
- derived intermediate state, который нужен для materialization и explainability.

Ключевые свойства:
- слой не portable;
- это не part of project-owned metadata;
- его можно rebuild из source layers и project intent, если service state утрачен.

### 6.4 `Runtime Materialization State`

Это environment-facing runtime projection.

Для конкретной agent system этот слой содержит:
- materialized runtime files;
- rendered instructions или config artifacts;
- adapter-facing structures, которые реально потребляет выбранная environment.

Ключевые свойства:
- это projection, а не Source of Truth;
- этот слой rebuildable;
- shape artifacts зависит от adapter implementation.

## 7. Project portability

### 7.1 Главный invariant portability

Проект должен хранить только portable intent и stable references.

Проект не должен хранить:
- machine-specific absolute paths;
- direct paths до central catalog;
- service-local filesystem internals;
- adapter-internal operational paths.

### 7.2 Что допустимо хранить в project-level metadata

Допустимые reference-level fields:
- `methodology_id`
- `version_ref`
- `artifact_id`
- `artifact_type_id`
- `role_id`
- `profile_id`
- `binding_id`
- `primary_agent_system`
- project-relative discovery and classification references

### 7.3 Почему это важно

Такой подход позволяет:
- переносить проект между машинами;
- materialize runtime для одной и той же методологии в разных environments;
- не смешивать logical selection и physical storage.

## 8. Central catalog и service-local storage

### 8.1 Central methodology catalog

`Central methodology catalog` живет во внутреннем storage сервиса и управляется service settings.

Это означает:
- default location может задаваться настройками сервиса;
- физический path до catalog — concern сервиса, а не проекта;
- project работает через stable references, а не через direct catalog path.

### 8.2 Internal service storage

У сервиса должно быть собственное internal storage для:
- central catalog;
- runtime records;
- jobs metadata;
- cache;
- indices;
- diagnostics and snapshots.

Этот storage не должен протекать в project metadata как обязательная часть portability model.

## 9. Adapter projection policy

### 9.1 Общий принцип

Каждая target agent system подключается через adapter boundary.

Это означает:
- reusable source artifacts не должны хранить runtime-specific file layout как core knowledge;
- project выбирает execution target через `primary_agent_system`;
- service-resolver выбирает нужную projection для этого target;
- runtime materialization создает environment-facing representation выбранного adapter.

### 9.2 Что это значит для проектного слоя

Project layer не должен:
- считать runtime artifacts каноническим source layer;
- хранить полный materialized snapshot как смысловую модель проекта;
- смешивать role semantics и adapter-specific representation.

### 9.3 Unified project-scoped runtime

Для выбранной agent system runtime должен materialize как единый project-scoped local layer.

Следствие:
- distinction global vs project полезна в source layering;
- но agent-facing runtime должен быть согласованным локальным слоем проекта;
- adapter отвечает за сборку этого unified local runtime.

## 10. `primary_agent_system`

`Primary_agent_system` — это project-level selector, который говорит сервису, какой adapter projection materialize как основной runtime target.

В этом документе важно зафиксировать только следующее:
- поле принадлежит `Project Portable Intent`;
- его смысл — выбрать target execution environment;
- оно не подменяет собой reusable role semantics;
- оно должно работать через stable adapter identity, а не через эвристику по наличию runtime files.

Подробный process смысл использования роли при разных systems не принадлежит этому документу.

## 11. Role pack storage location rules

Этот документ не описывает canonical pack structure, но фиксирует storage-level правила для reusable packs.

На storage boundary важно следующее:
- reusable role packs живут в source-oriented reusable layer, а не в runtime materialization;
- project intent ссылается на pack или role references, но не обязан копировать pack целиком;
- service-local runtime state может хранить resolved role bundle;
- runtime materialization создает environment-facing output, а не reusable pack structure.

То есть `role pack` как reusable source unit остается в source-oriented layer, а не растворяется в project config или runtime directories.

## 12. Contract layer boundary

`Docs/contracts/README.md` остается единственным Source of Truth для contract policy.

Следовательно, этот документ:
- не дублирует contract vocabulary;
- не дублирует rules of authoring для contracts;
- не пересказывает machine-readable schema policy.

Здесь допустимо фиксировать только то, как contract layer связан с:
- storage boundaries;
- runtime state;
- navigation;
- repository pointers;
- traceability.

## 13. Traceability and navigation implications

Storage and interface model должны поддерживать traceability между:
- документацией;
- ADR;
- contracts;
- кодом;
- тестами;
- project references;
- runtime projections.

Для этого:
- canonical files должны иметь stable identity;
- MCP и Web UI должны уметь приводить пользователя или агента к source artifact path;
- derived graph должен сохранять provenance и relationship context;
- runtime materialization должна быть explainable через source references.

## 14. Что этот документ не должен делать

Этот документ не должен:
- описывать artifact type taxonomy;
- описывать process semantics workflow and roles;
- определять discovery classification statuses;
- дублировать contract policy;
- превращаться в adapter implementation manual.

Если в документ начинают попадать подробные type families, role semantics или discovery heuristics, это означает нарушение boundaries.

## 15. Связь с другими каноническими документами

Этот документ нужно читать вместе с:
- `docs/methodology-layer/overview.md` как обзором слоя;
- `docs/methodology-layer/principles.md` как набором guiding principles;
- `docs/methodology-layer/artifact-model.md` как artifact-oriented spec;
- `docs/methodology-layer/workflow-and-roles.md` как process-level spec;
- `docs/methodology-layer/project-discovery.md` как discovery policy spec;
- `docs/contracts/README.md` как contract boundary layer.

## 16. Canonical invariants

Для первой итерации migration baseline считаются обязательными следующие invariants:
- file-first workflow остается canonical Source of Truth;
- project хранит portable intent, а не machine-specific storage paths;
- `Catalog Source of Truth`, `Project Portable Intent`, `Service-local Runtime State` и `Runtime Materialization State` являются разными слоями;
- runtime materialization считается rebuildable projection;
- `primary_agent_system` принадлежит project-level intent и выбирает adapter target;
- contract policy не дублируется вне `docs/contracts/README.md`;
- MCP и Web UI усиливают navigation and configuration, но не подменяют file-based SoT.

## 17. Целевое назначение для миграции legacy docs

При миграции legacy planning package этот документ должен стать канонической точкой сборки для:
- interface model;
- four-layer storage model;
- project portability rules;
- central catalog boundary;
- adapter projection policy;
- unified project-scoped runtime semantics.

После завершения миграции именно этот файл должен заменить временные planning explanations про interfaces, storage boundaries и runtime projection policy, которые сейчас размазаны по legacy planning docs.
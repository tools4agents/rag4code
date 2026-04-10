# Workflow and Roles for Project Methodology Runtime

> Status: Draft  
> Scope: каноническая process-level спецификация для `workflow`, `workflow-step`, `step-vacancy` и `agent-role` в слое `Project Methodology Runtime`  
> Role: Source of Truth для process semantics, role reuse и workflow assignment layer

## 1. Назначение документа

Этот документ фиксирует process layer для `Project Methodology Runtime`.

Его задача — описать:
- как в методологии понимаются `workflow` и `workflow-step`;
- как `step-vacancy` связывает шаг процесса с reusable ролью;
- как понимается `agent-role` как профиль исполнителя;
- как сохраняется разделение между reusable role semantics и workflow assignment;
- как человек и агент должны навигировать process layer без смешения с storage, runtime и contract policy.

Этот документ не описывает:
- artifact meta-model и pack structure;
- storage boundaries и runtime states;
- discovery policy;
- detailed contract schemas или contract policy;
- adapter-specific materialization details.

## 2. Почему нужен отдельный process layer

`Project Methodology Runtime` рассматривает разработку как работу человека и ИИ-агентов по согласованному process map.

Чтобы этот процесс был reusable, explainable и traceable, нужно различать несколько разных сущностей:
- `workflow` как карту процесса;
- `workflow-step` как подробное описание конкретного шага;
- `step-vacancy` как позицию на шаге;
- `agent-role` как reusable профиль исполнителя.

Если смешать эти сущности в одном описании, система теряет:
- ясность ролей и границ ответственности;
- переиспользование ролей между workflow;
- навигацию от общего процесса к конкретному действию;
- возможность заменять role bindings без переписывания role semantics.

## 3. Core process entities

### 3.1 `workflow`

`Workflow` — это процессная карта, которая описывает полезную последовательность шагов для достижения результата.

На process layer `workflow` отвечает за:
- цель процесса;
- порядок шагов;
- обзорную навигацию по процессу;
- optional high-level inputs и outputs процесса.

`Workflow` должен оставаться компактной картой, а не превращаться в перегруженный монолит.

При этом важно различать:
- `workflow` как semantic process entity;
- `workflow-pack` как packaging boundary, внутри которой workflow authoring-ся и хранится.

### 3.2 `workflow-step`

`Workflow-step` — это semantic execution unit и подробное описание одного конкретного шага workflow.

На process layer `workflow-step` отвечает за:
- входы шага;
- действие шага;
- ожидаемые выходы;
- `DoD` шага;
- критерии провала или условия возврата;
- ссылку на связанную `step-vacancy`;
- связи с reusable `skills`, если шаг опирается на них.

`Workflow-step` описывает работу шага, а не reusable семантику исполнителя.

При этом важно различать:
- `workflow-step` как semantic step entity;
- `workflow-step-pack` как packaging boundary, внутри которой step authoring-ся и хранится вместе с support materials.

### 3.3 `step-vacancy`

`Step-vacancy` — это позиция на конкретном шаге конкретного workflow.

Она нужна, чтобы отделить:
- описание работы шага;
- назначение роли на шаг;
- reusable semantics самой роли.

`Step-vacancy` отвечает за assignment layer:
- какая роль требуется или допустима для шага;
- какая позиция должна быть закрыта в контексте шага;
- как workflow связывает step execution с reusable role profile.

### 3.4 `agent-role`

`Agent-role` — это reusable профиль исполнителя.

Роль описывает:
- системное поведение и образ мышления;
- доступные `rules`, `skills` и `MCP tools`;
- optional `when_to_use` как guidance hint;
- optional file access restrictions или близкую policy abstraction.

`Agent-role` не равен:
- конкретной `LLM model`;
- конкретному шагу workflow;
- конкретному runtime mode;
- конкретному adapter projection.

## 4. One-way process model

Для process layer фиксируется однонаправленная связь:
- `workflow -> workflow-step -> step-vacancy -> agent-role`

Это означает:
- `workflow` определяет карту процесса;
- каждый `workflow-step` раскрывает отдельный шаг;
- `step-vacancy` связывает шаг с подходящей ролью;
- `agent-role` не содержит знания о конкретных шагах, в которых он используется.

Такое направление зависимости сохраняет reusable nature роли и не делает process layer циклическим.

Для execution baseline дополнительно фиксируется:
- агенту обычно назначают выполнение конкретного `workflow-step`;
- один агент может последовательно выполнить несколько шагов, если это допускает process policy;
- весь workflow не должен рассматриваться как одна непрозрачная инструкция для единственного запуска целиком.

## 5. Что значит reusable role semantics

`Agent-role` должен проектироваться как reusable entity по умолчанию.

Это означает:
- одна и та же роль может использоваться в разных workflow;
- одна и та же роль может использоваться в нескольких шагах одного workflow;
- одна и та же роль может переноситься между проектами;
- workflow assignment не должен переписывать базовую role semantics.

Следствие:
- workflow выбирает роль для шага;
- роль не диктует, в каких шагах ее обязаны использовать;
- project methodology может менять workflow bindings без разрушения reusable role profile.

## 6. Разделение между role semantics и workflow assignment

В process layer нужно жестко различать два уровня.

### 6.1 Reusable role layer

Это уровень `agent-role`.

Он отвечает за:
- профиль исполнителя;
- guidance и behavioral semantics;
- доступные capabilities;
- reusable identity роли.

### 6.2 Assignment layer

Это уровень `step-vacancy`.

Он отвечает за:
- назначение роли на конкретный шаг;
- связь process map с reusable role;
- возможность менять исполнителя шага без изменения самой role semantics.

### 6.3 Execution description layer

Это уровень `workflow-step`.

Он отвечает за:
- описание самой работы шага;
- входы, выходы, `DoD` и failure criteria;
- ссылку на позицию шага через `step-vacancy`.

Именно это разделение позволяет избежать смешения:
- кто выполняет работу;
- где именно он назначен;
- что именно нужно сделать на шаге.

## 7. `when_to_use` как explainability hint

Для `agent-role` сохраняется важный invariant:
- `when_to_use` полезен как reusable guidance hint;
- это поле не заменяет workflow assignment;
- это поле не указывает конкретный шаг workflow;
- это поле помогает человеку и агенту понять, зачем роль существует и в каких типах задач она полезна.

Поэтому:
- `when_to_use` принадлежит role semantics;
- `step-vacancy` принадлежит assignment layer;
- workflow по-прежнему остается главным местом, где определяется применение роли в процессе.

## 8. Связь core role и adapter projection

На process layer важно признавать distinction между:
- core `agent-role`;
- `agent-system`-specific asset этой роли.

При этом:
- reusable role semantics принадлежат core role artifact;
- `agent-system`-specific asset не подменяет role semantics;
- process layer может учитывать, что у роли есть совместимый asset для выбранной `agent-system`;
- но этот документ не описывает storage, layout или runtime materialization artifacts.

Нужный invariant такой:
- workflow использует role semantics, а не runtime-specific file layout;
- execution environment может потребовать `agent-system`-specific asset, но это не меняет process model.

## 9. `role pack` как reusable source unit

Process layer признает, что `agent-role` может поставляться через `role pack` как reusable source unit.

На process layer важно признавать, что `role-pack` является специальным reusable packaging pattern для роли:

- он может объединять core role artifact;
- он может включать `agent-system`-specific assets для этой роли;
- он не должен трактоваться как универсальный шаблон для всех reusable packs.

Но этот документ не владеет:
- canonical pack structure;
- physical layout pack;
- packaging boundary как artifact model.

В этом документе фиксируется только process-level invariant:
- role pack — допустимый способ поставки reusable role;
- semantic usage роли внутри workflow не определяет и не переопределяет packaging conventions;
- pack structure задается artifact-oriented документацией, а не process semantics.

## 10. `primary-agent-system` в process layer

`Primary-agent-system` на process layer допускается только как process awareness concept.

Это означает:
- process layer может учитывать, какая `agent-system` активна для текущего developer context в проекте;
- role usage может зависеть от наличия совместимого `agent-system`-specific asset для этой system;
- сам выбор `primary-agent-system` не меняет reusable role semantics.

Важно различать:

- `primary-agent-system` как human-facing term;
- `primary_agent_system` как field-like selector в project configuration.

Process layer признает только semantic смысл этого selector:

- у конкретного разработчика в конкретном проекте обычно есть одна active `agent-system` в момент работы;
- при этом сам проект не должен считаться навсегда привязанным к одной agent system;
- разные разработчики могут использовать разные `agent-system` для одного и того же проекта.

Важное ограничение:
- этот документ не фиксирует storage, selector schema или runtime resolution pipeline для `primary_agent_system`;
- эти аспекты принадлежат storage and interfaces layer.

## 11. Что пока не формализуется как отдельный bounded context

На текущей итерации не создается отдельный focused spec для `workflow contracts`.

Причины:
- `workflow` и `workflow-step` уже не считаются markdown-only сущностями: это semantic entities, которые обычно authoring-ся через `workflow-pack` и `workflow-step-pack`;
- при этом handoff contracts между шагами пока не стабилизированы как самостоятельная formal model с жестким API;
- current priority — traceability между documentation, ADR, contracts, code, tests и project references, а не отдельная formal contract model между workflow steps.

Следствие:
- process layer описывает workflow semantics;
- contract policy остается в `docs/contracts/README.md`;
- если позже появится устойчивая model для step input and output contracts или `workflow -> contract -> test` traceability как отдельного слоя, тогда можно выделить отдельный focused spec.

## 12. Minimal canonical expectations

Для первой итерации process layer должен поддерживать следующие expectations.

### 12.1 Для `workflow`

Минимально `workflow` должен описывать:
- зачем нужен процесс;
- последовательность шагов.

Если workflow authoring-ся через `workflow-pack`, pack должен содержать по меньшей мере канонический workflow overview и ссылки на шаги.

### 12.2 Для `workflow-step`

Минимально `workflow-step` должен описывать:
- входы шага;
- действие шага;
- связанную `step-vacancy`;
- выходы шага;
- `DoD`;
- criteria for failure or return.

Если step authoring-ся через `workflow-step-pack`, pack должен содержать по меньшей мере канонический step markdown и может содержать templates, checklists, examples, references и другие support artifacts.

### 12.3 Для `step-vacancy`

Минимально `step-vacancy` должен описывать:
- identity позиции;
- связь с конкретным шагом;
- required или allowed `agent-role`.

### 12.4 Для `agent-role`

Минимально `agent-role` должен задавать:
- stable role identity;
- name и description;
- system behavior baseline;
- reusable capability set;
- optional `when_to_use`.

## 13. Process layer и traceability

Process layer должен быть совместим с graph-backed traceability.

На уровне process semantics должны быть recoverable следующие связи:
- какой workflow содержит какие steps;
- какой step связан с какой vacancy;
- какая vacancy ссылается на какую role;
- какие результаты workflow относятся к какому process path.

При этом process layer не обязан сам описывать все implementation-facing traceability edges.
Он должен лишь сохранять понятную semantic structure, поверх которой можно строить графовую навигацию между:
- документацией;
- ADR;
- contracts;
- кодом;
- тестами;
- project references.

## 14. Что этот документ не должен делать

Этот документ не должен:
- превращаться в artifact catalog;
- описывать pack structure и physical layout;
- дублировать storage state model;
- описывать MCP и Web UI boundaries;
- дублировать contract policy;
- описывать discovery classification rules.

Если в этот документ начинают попадать storage paths, materialization directories, detailed projection schemas или discovery heuristics, это означает нарушение boundaries.

## 15. Связь с другими каноническими документами

Этот документ нужно читать вместе с:
- `docs/methodology-layer/overview.md` как обзором слоя;
- `docs/methodology-layer/principles.md` как набором guiding principles;
- `docs/methodology-layer/artifact-model.md` как artifact-oriented spec;
- `docs/methodology-layer/interfaces-and-storage.md` как boundary spec для interfaces и storage;
- `docs/methodology-layer/project-discovery.md` как discovery policy spec;
- `docs/terms/project/terms/agent-role.md`, `docs/terms/project/terms/workflow.md`, `docs/terms/project/terms/workflow-pack.md`, `docs/terms/project/terms/workflow-step.md`, `docs/terms/project/terms/workflow-step-pack.md`, `docs/terms/project/terms/step-vacancy.md`, `docs/terms/project/terms/agent-system.md`, `docs/terms/project/terms/primary-agent-system.md` и `docs/terms/project/terms/role-pack.md` как glossary layer.

## 16. Canonical invariants

Для первой итерации migration baseline считаются обязательными следующие invariants:
- `agent-role` — reusable role profile, а не шаг workflow и не runtime mode;
- `step-vacancy` — assignment layer, а не description of work;
- `workflow-step` — detailed step description, а не reusable role semantics;
- `workflow` — process map, а не хранилище всех деталей шага;
- `workflow` и `workflow-step` являются semantic entities, а не просто markdown files;
- `workflow-pack` и `workflow-step-pack` являются packaging boundaries, а не заменой process semantics;
- связь `workflow -> workflow-step -> step-vacancy -> agent-role` является однонаправленной;
- `when_to_use` усиливает explainability роли, но не заменяет workflow assignment;
- `workflow-step` может ссылаться на reusable `skills`, но не должен semantic-чески сливаться с ними;
- наличие `agent-system`-specific asset не меняет process semantics роли;
- `primary-agent-system` описывает active target environment для developer context, а не semantic ownership роли;
- process layer не владеет pack structure;
- process layer не владеет contract policy;
- process layer не владеет storage and runtime model.

## 17. Целевое назначение для миграции legacy docs

При миграции legacy planning package этот документ должен стать канонической точкой сборки для:
- role model;
- workflow model;
- assignment model через `step-vacancy`;
- distinction между reusable role semantics и process execution semantics;
- process-level invariants, которые сейчас размазаны между planning docs и discussion artifacts.

После завершения миграции именно этот файл должен заменить временные discussion and planning explanations про `agent-role`, `workflow`, `workflow-step` и `step-vacancy` как process layer.

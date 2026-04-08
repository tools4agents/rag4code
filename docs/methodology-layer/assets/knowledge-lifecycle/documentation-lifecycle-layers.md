# Documentation Lifecycle Layers

> Status: Draft  
> Scope: concrete `knowledge-lifecycle asset` под названием `document-driven-development`  
> Role: Source of Truth для трехслойной documentation flow model внутри проектов, которыми управляет HyperGraph

## Назначение

Этот документ фиксирует первый concrete [`knowledge-lifecycle asset`](../../../terms/project/terms/knowledge-lifecycle-asset.md): `document-driven-development`.

В этой модели знание в проекте ведется прежде всего через документацию, поэтому lifecycle знания выражается как lifecycle documentation layers.

## Три слоя

### [`Operational Documentation Layer`](../../../terms/project/terms/operational-documentation-layer.md)

Это временный operational слой, в котором рождается и уточняется новое знание.

Типичные artifacts этого слоя:

- [`ideas`](../../../terms/project/terms/idea-artifact.md);
- [`plans`](../../../terms/project/terms/plan-artifact.md);
- [`tasks`](../../../terms/project/terms/task-artifact.md);
- [`research`](../../../terms/project/terms/research-artifact.md);
- [`discussion`](../../../terms/project/terms/discussion-artifact.md);
- [`review`](../../../terms/project/terms/review-artifact.md);
- [`open questions`](../../../terms/project/terms/open-question.md);
- [`white spots`](../../../terms/project/terms/white-spot.md);
- [`spike reports`](../../../terms/project/terms/spike-report.md), если для проверки гипотезы потребовался небольшой кодовый эксперимент или PoC.

В текущем baseline этот слой соответствует `operational_scope/`.

### [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md)

Это канонический инженерный Source of Truth для проекта.

Он содержит:

- архитектуру;
- terms и glossary;
- контракты;
- долгоживущие technical decisions;
- другие инженерные документы, на которые должны опираться разработчики и агенты.

В текущем baseline этот слой соответствует `docs/`.

### [`Release Documentation Layer`](../../../terms/project/terms/release-documentation-layer.md)

Это release-ready документация для внешнего потребления.

Она предназначена для:

- пользователей;
- разработчиков-интеграторов;
- контрибьюторов;
- читателей опубликованной release documentation.

Этот слой может materialize в publishable docs system вроде Docusaurus.

## Правило переходов

Для `document-driven-development` фиксируется следующая базовая логика переходов:

1. новое знание рождается в [`Operational Documentation Layer`](../../../terms/project/terms/operational-documentation-layer.md);
2. канонизируется в [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md);
3. публикуется для внешнего потребления в [`Release Documentation Layer`](../../../terms/project/terms/release-documentation-layer.md).

## Что это значит practically

- если идея, исследование, review или `spike report` еще не стали каноническим engineering knowledge, они живут в [`Operational Documentation Layer`](../../../terms/project/terms/operational-documentation-layer.md);
- если решение принято и должно стать long-lived source of truth, оно поднимается в [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md);
- если знание нужно отдать конечным пользователям, интеграторам или контрибьюторам как release-facing docs, оно публикуется в [`Release Documentation Layer`](../../../terms/project/terms/release-documentation-layer.md).

## Связь с task management

Этот asset не задает детальную систему хранения задач.

Он задает только lifecycle knowledge/documentation.

Task storage, task index, handoff и focus management принадлежат отдельному [`task-management-system asset`](../../../terms/project/terms/task-management-system-asset.md).

## Связь с terms management

Этот asset не задает детальную glossary system.

Структура `terms_map.md`, detail pages и navigation по терминам принадлежат отдельному [`terms-management-system asset`](../../../terms/project/terms/terms-management-system-asset.md).

## Связь с research management

Этот asset не задает детальную систему хранения и трассировки исследований.

Research index, topic trees, branch dossiers и iteration traceability принадлежат отдельному [`research-management-system asset`](../../../terms/project/terms/research-management-system-asset.md).

## Связь с методологией

Этот asset не равен конкретной methodology.

Например, concrete [`methodology asset`](../../../terms/project/terms/methodology-asset.md) вроде `waterfall` может использовать `document-driven-development` как knowledge lifecycle baseline, но не владеет самим lifecycle model.

## Что этот документ не делает

Этот документ не описывает:

- конкретный `task-map.md` layout;
- конкретную term map structure;
- process semantics конкретной methodology;
- release publishing pipeline implementation.

## Связь с другими документами

Этот документ нужно читать вместе с:

- [`asset-taxonomy-and-composition-model.md`](../../asset-taxonomy-and-composition-model.md);
- [`layered-sot-and-materialization-model.md`](../../layered-sot-and-materialization-model.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- `document-driven-development` является concrete `knowledge-lifecycle asset`.
- `Operational Documentation Layer`, `Engineering Documentation SoT` и `Release Documentation Layer` являются разными documentation lifecycle layers.
- operational artifacts не должны считаться engineering SoT, пока знание не канонизировано.
- release documentation не должна подменять engineering SoT проекта.
- `task-management-system asset`, `terms-management-system asset` и `research-management-system asset` остаются отдельными subsystem assets.

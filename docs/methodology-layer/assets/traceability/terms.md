# Terms: Traceability System

> Status: Draft  
> Scope: локальная терминология для `traceability-system asset`  
> Role: общие определения для traceability docs, methodology profiles, skills and workflow steps

## Назначение

Этот файл фиксирует локальные термины [`traceability-system asset`](./index.md), чтобы traceability docs, methodology profiles, skills and workflow steps не смешивали semantic traceability model и technical graph projection.

Главная граница:

```text
Entity / Entity type / Entity instance = language of traceable things
Relationship / Relationship type / Relationship instance = language of traceable links
Trace chain / Trace chain instance = language of meaningful paths
Graph projection = derived technical representation, not Source of Truth
```

Technical mapping is allowed only in graph projection / implementation context:

```text
Entity instance -> graph vertex
Relationship instance -> graph edge
Trace chain instance -> curated graph path over Relationship instances
```

## Terms

### Traceability system

Reusable markdown-first система для регистрации project Entity instances, Relationship instances and meaningful Trace chain instances в Source of Truth files.

Она задает mechanics для Entity registries, Relationship registries, Trace maps, project catalogs и derived graph projection.

### Traceability fact

Конкретное source-authored утверждение, используемое для traceability.

Примеры:

- строка Entity instance в `entities-map.md`;
- строка Relationship instance в `relationships-map.md`;
- строка Trace chain instance в `trace-map.md`;
- строка catalog, defining Entity type or Relationship type.

### Entity

Понятие сущности в traceability model: project thing, которую agents and humans должны уметь находить and reference.

Примеры: requirement, user story, system behavior record, architecture component, ADR, test case.

### Entity type

Класс или family of Entity instances с общим meaning и ownership.

Примеры: `requirement`, `product-capability`, `user-story`, `architecture-component`, `test-case`.

Entity types принадлежат project traceability language. Concrete Entity instances live in Entity registries.

### Entity instance

Concrete Entity со stable identifier.

Примеры: `REQ-001`, `CAP-002`, `SCN-004`, `ADR-003`.

В graph projection context Entity instance может быть represented as graph vertex, но markdown/code SoT остается primary source.

### Entity Identifier family

Stable project-local identifier pattern, используемый для идентификации Entity instances.

Примеры: `REQ-`, `US-`, `SCN-`, `ADR-`, `TC-`.

Entity Identifier families должны быть stable, grep-friendly и documented в Entity type catalog, если они active or proposed.

### Identifier prefix

Prefix-часть Entity Identifier family.

Пример: `REQ-` в `REQ-001`.

Этот asset не freeze-ит global prefix grammar. Methodology profiles и projects определяют active prefixes.

### Entity type catalog

Project-level catalog для active or proposed Entity types, Entity Identifier families/patterns, domains и registry locations.

Recommended location:

```text
docs/traceability/entity-type-catalog.md
```

Entity type catalog сообщает агентам, что означает identifier family и где искать Entity instances.

### Entity registry

Domain-local registry конкретных Entity instances.

Typical location:

```text
docs/<domain>/entities-map.md
```

Примеры:

```text
docs/product/entities-map.md
docs/system_design/entities-map.md
docs/architecture/entities-map.md
docs/testing/entities-map.md
```

### Entity detail page

Optional page для concrete Entity instance, когда row в `entities-map.md` недостаточно.

Typical location:

```text
docs/<domain>/entities/<entity-id>.md
```

Detail pages поддерживают substantial behavior, rationale, examples, constraints, risks или many relationships. Они не заменяют Entity registry.

### Relationship

Понятие связи между Entity instances в traceability model.

Relationship describes meaningful directed or typed connection, e.g. one entity details, realizes, supports, constrains or verifies another entity.

### Relationship type

Semantic type of Relationship.

Примеры: `details`, `realizes`, `supports`, `constrains`, `verifies`, `implemented-by`, `depends-on`.

Relationship type — canonical semantic concept. В markdown table cell он может храниться as a string value/label, but `label` is only stored representation of the Relationship type value, not a separate semantic concept.

### Relationship type catalog

Project-level catalog для allowed, active or proposed Relationship types и их meanings.

Recommended location:

```text
docs/traceability/relationship-type-catalog.md
```

Catalog защищает `relationships-map.md` от ambiguous Relationship type values без shared meaning.

### Relationship instance

Concrete relationship fact между двумя Entity instances.

Recommended registry location:

```text
docs/traceability/relationships-map.md
```

Relationship instance имеет source Entity instance, Relationship type, target Entity instance, source reference, status and notes.

В graph projection context Relationship instance может быть represented as graph edge, но semantic traceability docs should use Relationship terminology by default.

### Relationship registry

Markdown registry для Relationship instances.

Canonical semantic filename:

```text
docs/traceability/relationships-map.md
```

`relationships-map.md` является Source of Truth для atomic Relationship instances. Technical graph edges are derived from these Relationship instances.

### Trace chain

Curated meaningful path over Relationships.

Example:

```text
REQ-001 -> CAP-002 -> SCN-004 -> AC-005
```

Trace chains помогают людям и агентам следовать important reasoning paths без повторной reconstruction из atomic Relationship instances.

Trace chain описывает саму последовательность и ее смысл. Если эта последовательность зарегистрирована в `trace-map.md` и получила stable `Trace ID`, она становится Trace chain instance.

### Trace chain instance

Concrete registered Trace chain with stable `Trace ID` in `trace-map.md`.

Пример:

| Trace ID | Chain | Meaning | Status | Notes |
| --- | --- | --- | --- | --- |
| TR-001 | `REQ-001 -> CAP-002 -> SCN-003 -> AC-004` | Core product acceptance path for onboarding. | draft | Built during Product Design. |

В этом примере:

- `REQ-001 -> CAP-002 -> SCN-003 -> AC-004` — Trace chain;
- `TR-001` — stable identifier конкретного Trace chain instance;
- вся row in `trace-map.md` — traceability fact about this Trace chain instance.

Trace chain instance нужен, когда на curated path нужно ссылаться из review, Design Baseline Consolidation, Test Design, tasks or handoff notes.

Примеры ссылок:

```text
Проверь semantic consistency for TR-001.
TR-001 lacks System Design interpretation.
Test Design should derive verification targets from TR-001.
```

Trace chain instance не заменяет Relationship instances. Его chain должен быть explainable через Relationship registry, если corresponding Relationship instances уже существуют.

### Trace Identifier family

Stable project-local identifier family for Trace chain instances.

Default family:

```text
TR-
```

Этот asset сейчас использует одну Trace Identifier family and does not define a `Trace chain type catalog`.

Причина: Trace chain instances are curated meaningful paths over Relationship instances. В отличие от Entity instances and Relationship instances, для Trace chain instances пока нет stable, reusable type families with distinct governance, lifecycle or routing semantics.

Если practical usage позже выявит устойчивые кластеры Trace chains с разными lifecycle, review, routing, ownership or downstream-consumption semantics, asset может ввести `Trace chain type` taxonomy через explicit design decision.

See: [`trace-chain-type-catalog-decision.md`](./adr/trace-chain-type-catalog-decision.md).

### Trace map / Trace chain registry

Markdown registry для Trace chain instances.

Recommended location:

```text
docs/traceability/trace-map.md
```

Trace chains должны быть explainable через Relationship instances in the Relationship registry.

### Trace seed

Early or partial traceability hint, который позже может стать Relationship instance or Trace chain instance.

Trace seeds полезны, когда relationship важен, но еще не все target Entity instances существуют, или когда another owning stage/domain должен validate the Relationship.

### Downstream handoff seed

Trace seed, предназначенный для another owning stage or domain.

Пример: Product Design может отметить, что product scenario должен стать input для System Design behavior, не inventing System Design Entity instance.

Downstream handoff seeds не являются final cross-domain Relationship instances, пока target Entity instances не существуют и owning stages or consolidation не validate them.

### Project traceability context

Thin project routing artifact, который сообщает агентам, где находятся active traceability entry points.

Recommended location:

```text
project/traceabilityContext.md
```

Он должен указывать на `docs/traceability/index.md` и не дублировать detailed catalogs.

### Graph projection

Derived graph database or MCP navigation layer, построенный из markdown/code Source of Truth.

Graph projection является rebuildable и не должен становиться canonical Source of Truth.

### Status

Lifecycle/readiness marker для traceability facts and traceability language elements, когда соответствующий file format supports status.

Status может применяться к:

- Entity type catalog rows;
- Relationship type catalog rows;
- Entity registry rows;
- Relationship registry rows;
- Trace map rows.

Generic traceability asset определяет status как concept и рекомендует status-bearing registries, но не владеет methodology-specific promotion rules.

Concrete status semantics and transitions задаются methodology traceability profiles. Для `Adaptive Waterfall for Agents` status rules живут в:

```text
assets/metodologes/waterfall/software-development-methodology/resources/traceability/status-semantics.md
```

## Usage rule

- Используй эти terms при authoring traceability docs, methodology profiles, skills and workflow steps.
- Используй `Relationship type`, not `Relationship label`, когда обсуждается traceability semantics.
- Если слово `label` появляется в implementation/storage context, оно означает only stored string representation of a Relationship type value.
- Не используй `Relationship instance`, technical graph `edge` и `Trace chain` как взаимозаменяемые понятия.
- Не используй `Entity type` и `Entity instance` как взаимозаменяемые понятия.
- Если term становится project-wide за пределами этого asset, promote it to `docs/terms/` according to the terms-management system.

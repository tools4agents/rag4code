# Traceability System

> Status: Draft  
> Scope: concrete `traceability-system asset` для markdown-first graph-ready traceability  
> Role: navigation entrypoint для generic traceability conventions, templates and derived graph projection model

## Назначение

`Traceability System` задает reusable asset для регистрации project Entity instances, Relationship instances and meaningful Trace chain instances в file-first Source of Truth.

Он нужен, чтобы человек и агент могли:

- находить сущности проекта по stable identifiers;
- видеть atomic Relationship instances между сущностями;
- читать meaningful Trace chains поверх Relationships;
- строить derived graph database projection без переноса Source of Truth в database;
- использовать MCP/graph tools как navigation accelerator, а не как canonical truth.

## Состав asset package

- [`traceability-system.md`](./traceability-system.md) — core model and boundaries.
- [`terms.md`](./terms.md) — local terminology for traceability docs, methodology profiles, skills and workflow steps.
- [`entity-registries.md`](./entity-registries.md) — registry pattern для Entity instances.
- [`relationship-and-trace-maps.md`](./relationship-and-trace-maps.md) — Relationship registry and Trace map model.
- [`graph-projection.md`](./graph-projection.md) — derived graph DB and MCP relationship.
- [`adr/`](./adr/) — asset-local design records for traceability-system decisions.
- [`resources/`](./resources/) — templates для project materialization.

Asset design records in `adr/` фиксируют локальные design decisions этого asset. Они похожи на ADR по смыслу, но относятся к design governance конкретного methodology asset, not to whole-system architecture.

## Baseline project materialization

Recommended default project shape:

```text
project/
  traceabilityContext.md

docs/traceability/
  index.md
  entity-type-catalog.md
  relationship-type-catalog.md
  relationships-map.md
  trace-map.md

docs/<domain>/
  entities-map.md
  entities/
    <entity-id>.md
```

`project/traceabilityContext.md` should remain a thin routing artifact. Detailed traceability catalogs live under `docs/traceability/` to preserve lazy loading and progressive disclosure.

Project-specific methodology or context may choose concrete domain locations, for example `docs/product/entities-map.md` or `docs/architecture/entities-map.md`.

## Boundary

### This asset does

- defines generic Entity registry, Relationship registry and Trace map conventions;
- defines markdown-first Source of Truth rule;
- provides templates for project-local materialization;
- explains how graph database can be derived from markdown/code sources.

### This asset does not

- does not own project facts;
- does not define SDLC-specific Entity families;
- does not decide product, architecture, system or testing semantics;
- does not define concrete graph DB schema or MCP API contract;
- does not replace methodology-specific traceability profiles.

## Related documents

- [`asset-taxonomy-and-composition-model.md`](../../asset-taxonomy-and-composition-model.md)
- [`agent-asset-manager.md`](../../agent-asset-manager.md)
- [`asset-environment-project-manager.md`](../../asset-environment-project-manager.md)
- [`documentation-lifecycle-layers.md`](../knowledge-lifecycle/documentation-lifecycle-layers.md)

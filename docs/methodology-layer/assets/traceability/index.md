# Traceability System

> Status: Draft  
> Scope: concrete `traceability-system asset` для markdown-first graph-ready traceability  
> Role: navigation entrypoint для generic traceability conventions, templates and derived graph projection model

## Назначение

`Traceability System` задает reusable asset для регистрации project entities, relationships and meaningful traces в file-first Source of Truth.

Он нужен, чтобы человек и агент могли:

- находить сущности проекта по stable identifiers;
- видеть atomic relationships между сущностями;
- читать meaningful trace chains поверх relationships;
- строить derived graph database projection без переноса Source of Truth в database;
- использовать MCP/graph tools как navigation accelerator, а не как canonical truth.

## Состав asset package

- [`traceability-system.md`](./traceability-system.md) — core model and boundaries.
- [`entity-registries.md`](./entity-registries.md) — registry pattern для graph vertices.
- [`edge-and-trace-maps.md`](./edge-and-trace-maps.md) — edge map and trace map model.
- [`graph-projection.md`](./graph-projection.md) — derived graph DB and MCP relationship.
- [`resources/`](./resources/) — templates для project materialization.

## Baseline project materialization

Recommended default project shape:

```text
project/
  traceabilityContext.md

docs/traceability/
  index.md
  entity-type-catalog.md
  relationship-label-catalog.md
  edges-map.md
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

- defines generic entity registry, edge map and trace map conventions;
- defines markdown-first Source of Truth rule;
- provides templates for project-local materialization;
- explains how graph database can be derived from markdown/code sources.

### This asset does not

- does not own project facts;
- does not define SDLC-specific entity families;
- does not decide product, architecture, system or testing semantics;
- does not define concrete graph DB schema or MCP API contract;
- does not replace methodology-specific traceability profiles.

## Related documents

- [`asset-taxonomy-and-composition-model.md`](../../asset-taxonomy-and-composition-model.md)
- [`agent-asset-manager.md`](../../agent-asset-manager.md)
- [`asset-environment-project-manager.md`](../../asset-environment-project-manager.md)
- [`documentation-lifecycle-layers.md`](../knowledge-lifecycle/documentation-lifecycle-layers.md)

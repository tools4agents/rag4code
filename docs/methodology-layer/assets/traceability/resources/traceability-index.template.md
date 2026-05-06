# Traceability

> Status: Draft  
> Scope: project traceability entry point  
> Role: navigation map for entity registries, edge map and trace map

## Назначение

Этот файл является root traceability entry point для проекта.

## Entity registries

| Domain | Registry | Notes |
| --- | --- | --- |
| `<domain>` | [`entities-map.md`](../<domain>/entities-map.md) | <What this domain owns> |

## Relationship maps

| Map | Purpose | Link |
| --- | --- | --- |
| Edges map | Atomic relationships between entities. | [`edges-map.md`](./edges-map.md) |
| Trace map | Curated meaningful paths over edges. | [`trace-map.md`](./trace-map.md) |

## Catalogs

| Catalog | Purpose | Link |
| --- | --- | --- |
| Entity type catalog | Active entity types, prefixes and registry locations. | [`entity-type-catalog.md`](./entity-type-catalog.md) |
| Relationship label catalog | Allowed or recommended edge labels and meanings. | [`relationship-label-catalog.md`](./relationship-label-catalog.md) |

## Notes

- Markdown/code files are Source of Truth.
- Graph DB and MCP are derived projection and navigation helpers.

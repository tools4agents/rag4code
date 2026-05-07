# Traceability

> Status: Draft  
> Scope: project traceability entry point  
> Role: navigation map for Entity registries, Relationship registry and Trace map

## Назначение

Этот файл является root traceability entry point для проекта.

## Entity registries

| Domain | Registry | Notes |
| --- | --- | --- |
| `<domain>` | [`entities-map.md`](../<domain>/entities-map.md) | <What this domain owns> |

## Relationship and trace registries

| Registry | Purpose | Link |
| --- | --- | --- |
| Relationship registry | Atomic Relationship instances between Entity instances. | [`relationships-map.md`](./relationships-map.md) |
| Trace map | Curated meaningful paths over Relationships. | [`trace-map.md`](./trace-map.md) |

## Catalogs

| Catalog | Purpose | Link |
| --- | --- | --- |
| Entity type catalog | Active Entity types, prefixes and registry locations. | [`entity-type-catalog.md`](./entity-type-catalog.md) |
| Relationship type catalog | Allowed or recommended Relationship types and meanings. | [`relationship-type-catalog.md`](./relationship-type-catalog.md) |

## Notes

- Markdown/code files are Source of Truth.
- Graph DB and MCP are derived projection and navigation helpers.

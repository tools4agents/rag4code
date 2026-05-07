# Entity Type Catalog

> Status: Draft  
> Scope: active project traceability Entity types and identifier families  
> Role: project-level SoT for Entity type meanings, prefixes and registry locations

## Назначение

Этот файл фиксирует, какие Entity types and identifier patterns используются в проекте.

## Entity type catalog

| Prefix / Pattern | Entity type | Domain | Registry | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| `<PREFIX>-` | `<entity-type>` | `<domain>` | [`entities-map.md`](../<domain>/entities-map.md) | active | <Meaning and usage notes.> |

## Status values

- `active` — prefix/type is currently used.
- `provisional` — prefix/type is allowed temporarily or under validation.
- `deprecated` — prefix/type should not be used for new entities.

## Notes

- This catalog defines where agents should look up identifiers.
- Entity instances live in domain `entities-map.md` files.
- Relationship types live in [`relationship-type-catalog.md`](./relationship-type-catalog.md).

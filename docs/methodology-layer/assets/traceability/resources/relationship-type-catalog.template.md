# Relationship Type Catalog

> Status: Draft  
> Scope: active project traceability Relationship types  
> Role: project-level SoT for Relationship type meanings

## Назначение

Этот файл фиксирует allowed or recommended Relationship types для `relationships-map.md`.

## Relationship type catalog

| Relationship type | Meaning | Typical From | Typical To | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| `<relationship-type>` | <Meaning.> | `<source Entity type>` | `<target Entity type>` | active | <Usage notes.> |

## Status values

- `active` — Relationship type is currently recommended.
- `provisional` — Relationship type is allowed temporarily or under validation.
- `deprecated` — Relationship type should not be used for new Relationship instances.

## Notes

- Relationship instances live in [`relationships-map.md`](./relationships-map.md).
- Curated paths live in [`trace-map.md`](./trace-map.md).
- Keep Relationship types stable and human-readable.
- If tooling calls a stored Relationship type value a `label`, treat it only as storage representation, not as a separate semantic concept.

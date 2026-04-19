# AGENTS.md

## Назначение

Этот документ фиксирует роль `AGENTS.md` внутри [`project-context-entry-system`](./project-context-entry-system.md).

## Что должно жить в `AGENTS.md`

`AGENTS.md` должен содержать только:

- краткое описание проекта;
- repository-wide loading order;
- links на project-local entry points;
- правило, что `docs/` побеждает `operational_scope/` при конфликте.

## Что не должно жить в `AGENTS.md`

- полный durable context;
- полный engineering SoT;
- execution status;
- большой rules corpus;
- детальная secret policy.

## Зачем это важно

Тонкий `AGENTS.md`:

- меньше дрейфует;
- проще переиспользуется между проектами;
- не превращается в монолитный memory bank replacement.

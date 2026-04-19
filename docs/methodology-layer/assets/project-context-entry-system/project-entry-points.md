# project/entry-points.md

## Назначение

Этот документ фиксирует роль `project/entry-points.md` внутри [`project-context-entry-system`](./project-context-entry-system.md).

## Что задает файл

`Project/entry-points.md` задает:

- local loading order;
- ownership split между `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и target-specific layers;
- project-specific routing details.

## Зачем нужен отдельный файл

Этот файл позволяет:

- не раздувать `AGENTS.md`;
- не смешивать navigation contract и другие durable context files;
- держать loading-order detail в одном месте.

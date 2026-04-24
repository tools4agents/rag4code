# project/entry-points.md

## Назначение

Этот документ фиксирует роль `project/entry-points.md` внутри [`project-context-entry-system`](./project-context-entry-system.md).

## Что задает файл

`Project/entry-points.md` задает:

- local loading order;
- ownership split между `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и target-specific layers;
- project-specific routing details.

## Отличие от `project/index.md`

`project/entry-points.md` не является индексом файлов `project/`.

- `project/index.md` владеет составом durable project context layer и кратким boundary summary.
- `project/entry-points.md` владеет маршрутом входа в контекст, переходами между context boundaries и ownership split.
- `project/index.md` может ссылаться на `project/entry-points.md`, но не должен дублировать его routing contract.

## Зачем нужен отдельный файл

Этот файл позволяет:

- не раздувать `AGENTS.md`;
- не смешивать navigation contract и другие durable context files;
- держать loading-order detail в одном месте.

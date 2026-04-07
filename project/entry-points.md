# Entry Points

## Назначение

Этот файл фиксирует concrete project-local реализацию [`repository-context-entry-model`](../docs/terms/project/terms/repository-context-entry-model.md) для HyperGraph.

Его задача - показать:
- какие entry-point artifacts используются в этом репозитории;
- в каком порядке человек и агент должны читать контекст;
- какой слой чем владеет;
- как работает [`nested-repo-context-switching`](../docs/terms/project/terms/nested-repo-context-switching.md) в текущем layout.

## Порядок чтения контекста

Для HyperGraph используется такой baseline route:

1. `AGENTS.md` как top-level router artifact.
2. `project/index.md` как durable context entry.
3. `project/gitContext.md` для repository ownership, nested repositories и git boundaries.
4. `project/techContext.md` для technical baseline и environment assumptions.
5. `project/codeStyle.md` для coding style и authoring conventions.
6. `project/repository-map.md` для top-level navigation по областям репозитория.
7. `docs/index.md` для navigation по [`Engineering Documentation SoT`](../docs/terms/project/terms/engineering-documentation-sot.md).
8. `operational_scope/index.md` только когда нужен execution context текущей итерации.
9. `.kilo/` artifacts только когда нужен Kilo-specific behavior или runtime/config layer.

Если временный operational artifact конфликтует с `docs/`, следуй `docs/`.

## Ownership model

### `AGENTS.md`

`AGENTS.md` владеет только:
- кратким описанием проекта;
- repository-wide loading order;
- links на основные entry points.

`AGENTS.md` не владеет:
- git boundary details;
- technical baseline во всех деталях;
- code style;
- engineering architecture canon.

### `project/`

`project/` владеет durable project context:
- repository boundaries;
- technical baseline;
- loading-order detail;
- repository map;
- code style;
- migration notes.

`project/` не является [`Engineering Documentation SoT`](../docs/terms/project/terms/engineering-documentation-sot.md).

### `docs/`

`docs/` владеет:
- архитектурой;
- glossary и terms;
- contracts;
- ADR;
- long-lived engineering decisions.

### `operational_scope/`

`operational_scope/` владеет временным execution context:
- tasks;
- plans;
- research;
- discussion;
- related execution artifacts.

Этот слой не должен подменять `docs/`.

### `.kilo/`

`.kilo/` владеет Kilo-specific project layer:
- rules;
- agents;
- commands;
- other target-specific config artifacts.

## Nested repo context switching

В этом репозитории [`nested-repo-context-switching`](../docs/terms/project/terms/nested-repo-context-switching.md) применяется к autonomous nested repositories, перечисленным в `project/gitContext.md`.

Текущее baseline rule:
- если task scope уходит в autonomous nested project со своим `AGENTS.md`, нужно переключиться на его local context;
- parent project используется только как outer navigation, пока task scope не вошел в nested project;
- fallback inheritance допустим только для отсутствующего слоя.

Boundary details и canonical список nested repositories задает `project/gitContext.md`.

## Связанные файлы

- `AGENTS.md`
- `project/index.md`
- `project/gitContext.md`
- `project/techContext.md`
- `project/codeStyle.md`
- `project/repository-map.md`
- `docs/index.md`
- `operational_scope/index.md`
- `docs/methodology-layer/repository-context-entry-model.md`

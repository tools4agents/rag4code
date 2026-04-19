# project/context-migration.md

## Назначение

Этот документ фиксирует optional роль `project/context-migration.md` внутри [`project-context-entry-system`](./project-context-entry-system.md).

## Когда файл нужен

`Project/context-migration.md` materialize-ится только тогда, когда проект реально проходит migration between context models, filesystem layouts или instruction layers.

## Что должен описывать файл

- current migration direction;
- coexistence of old and new layers;
- temporary compatibility rules.

## Что не должен описывать файл

- long-lived architecture canon;
- task-level migration execution plan.

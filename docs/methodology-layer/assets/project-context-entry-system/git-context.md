# project/gitContext.md

## Назначение

Этот документ фиксирует роль `project/gitContext.md` внутри [`project-context-entry-system`](./project-context-entry-system.md).

## Что должен описывать файл

- root repository path;
- nested repositories, если они есть;
- git ownership boundaries;
- working rules для git operations.

## Что не должен описывать файл

- architecture canon;
- secret masking policy во всех деталях;
- technical stack в целом.

## Boundary rule

Если secret-related note нужна как git reminder, она может кратко ссылаться на `project/secretsContext.md`, но не должна поглощать его роль.

# project/secretsContext.md

## Назначение

Этот документ фиксирует роль `project/secretsContext.md` внутри [`project-context-entry-system`](./project-context-entry-system.md).

## Почему нужен отдельный файл

Secret handling и local file policy не должны растворяться:

- ни в `gitContext.md`;
- ни в `techContext.md`;
- ни в `AGENTS.md`.

## Что должен описывать файл

- secret surfaces;
- local-only files;
- masking and logging rules;
- baseline policy для `.env`, key files и similar local artifacts.

## Что не должен описывать файл

- временные ссылки на iteration-specific task artifacts;
- engineering architecture;
- execution status.

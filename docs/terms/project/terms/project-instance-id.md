# project-instance-id

> Status: Draft  
> Scope: project-specific term for HyperGraph local registry model  
> Related: `../terms-map.md`

`Project-instance-id` — это machine-local identifier конкретной регистрации `project` в HyperGraph registry.

`Project-instance-id` нужен, чтобы:
- различать несколько локальных clones or worktrees одного project;
- связать root path, registry record and database reference;
- создать local identity, не зависящую только от `project-key`;
- безопасно хранить machine-specific metadata.

В baseline model `project-instance-id` создается при `project register` и хранится во внешнем `project-registry`.

`Project-instance-id` не является:
- portable logical identity проекта;
- частью shared project config;
- заменой `project-key`;
- Git commit or repository identifier.

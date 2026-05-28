# project-database

> Status: Draft  
> Scope: project-specific term for HyperGraph derived storage model  
> Related: `../terms-map.md`

`Project-database` — это logical derived graph database для одного `Project`.

`Project-database` нужна, чтобы:
- хранить текущий индекс файлов и связей проекта;
- поддерживать graph traversal and filtering queries;
- обслуживать CLI и MCP запросы без полного filesystem scan на каждый запрос;
- изолировать состояние одного project graph от другого.

`Project-database` является `derived-index`: ее состояние пересчитывается из project files, а не является главным Source of Truth.

Физически `project-database` может обслуживаться отдельным `database-service`. В таком случае `project-registry` хранит `project-database-binding`, а backend/service connection and startup settings описывает `database-backend-config`.

HyperGraph core обращается к database service через storage adapter and binding resolution: project instance selects logical project database, then backend config provides connection to the runtime service.

В первой итерации `project-database` отражает текущий active filesystem/current commit state. После Git checkout или branch switch пользователь отвечает за ручной reindex/rebuild.

`Project-database` не является:
- Git history;
- authoritative storage для project files;
- единственным владельцем graph truth;
- общей database для нескольких projects;
- конкретным Docker container или managed backend itself.

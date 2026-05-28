# project-registry

> Status: Draft  
> Scope: project-specific term for HyperGraph local project registry  
> Related: `../terms-map.md`

`Project-registry` — это machine-local реестр projects, зарегистрированных в HyperGraph на ОС пользователя.

`Project-registry` нужен, чтобы хранить:
- `project-instance-id`;
- `project-key`;
- root path;
- path к project-local config;
- `project-database-binding`;
- indexing metadata;
- optional references to `database-backend-config` records.

Registry помогает HyperGraph знать, какие projects пользователь отслеживает локально, и является будущей основой для cross-project references.

`Project-registry` может быть реализован через JSON artifacts, document-oriented database, MongoDB, MongoDB Atlas или другой backend, если он сохраняет machine-local registry semantics.

Registry не должен смешивать database service configuration and concrete project database binding: backend/service settings belong to `database-backend-config`, while project instance to logical database mapping belongs to `project-database-binding`.

`Project-registry` не является:
- project Source of Truth;
- Git-tracked project config;
- graph database самого project;
- единственным местом, где хранится logical project identity.

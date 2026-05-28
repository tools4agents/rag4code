# project-database-binding

> Status: Draft  
> Scope: project-specific term for HyperGraph project database binding model  
> Related: `../terms-map.md`

`Project-database-binding` — это machine-local registry record, который связывает конкретный `project-instance-id` с logical `project-database` inside selected `database-service`.

`Project-database-binding` обычно содержит:
- `project-instance-id`;
- database backend identifier;
- logical database name or namespace;
- schema/index version metadata;
- optional collection or graph namespace prefix.

`Project-database-binding` нужен, чтобы:
- определить, где physically served logical `project-database` конкретного project instance;
- связать project registration с selected database backend;
- позволить одному `database-service` обслуживать несколько project databases;
- поддержать перенос project database на другой backend without changing `project-key`;
- отделить project database selection от backend connection settings.

`Project-database-binding` не является:
- database backend configuration;
- Docker service description;
- project-local shared config;
- logical project identity;
- Source of Truth для project files.

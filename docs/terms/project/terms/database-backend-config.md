# database-backend-config

> Status: Draft  
> Scope: project-specific term for HyperGraph database backend configuration model  
> Related: `../terms-map.md`

`Database-backend-config` — это machine-local configuration, которая описывает available `database-service` backend и способ подключения или запуска этого backend.

`Database-backend-config` может описывать:
- backend type;
- local or managed service mode;
- connection URI or host/port;
- credentials reference;
- Docker image;
- container name;
- backend version;
- startup metadata;
- supported capabilities.

`Database-backend-config` нужен, чтобы:
- отделить database service configuration от конкретного project instance;
- позволить одному backend service обслуживать несколько project databases;
- сделать backend configurable per user/machine;
- поддержать local Docker backend and managed backends such as MongoDB Atlas;
- не дублировать connection settings in every project registry record.

`Database-backend-config` не является:
- logical `project-database`;
- binding конкретного project instance к database;
- project-local shared config;
- Source of Truth для project files.

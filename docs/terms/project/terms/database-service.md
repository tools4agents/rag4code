# database-service

> Status: Draft  
> Scope: project-specific term for HyperGraph database runtime backend  
> Related: `../terms-map.md`

`Database-service` — это runtime backend, с которым HyperGraph service общается для чтения и записи derived graph state.

`Database-service` нужен, чтобы:
- предоставить graph/database capabilities для `project-database`;
- обслуживать queries and updates через network or local service interface;
- позволить запуск backend через Docker container или внешний managed service;
- отделить logical database от конкретного runtime deployment.

В baseline model database service может быть локальным Docker-based сервисом или внешним managed backend, если connection settings are configured.

`Database-service` не является:
- project files Source of Truth;
- Git versioning layer;
- обязательно embedded database file;
- replacement for HyperGraph core logic.

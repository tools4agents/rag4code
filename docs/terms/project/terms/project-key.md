# project-key

> Status: Draft  
> Scope: project-specific term for HyperGraph project identity model  
> Related: `../terms-map.md`

`Project-key` — это portable logical identity одного `project`, заданный человеком в project-local config.

`Project-key` нужен, чтобы:
- дать project stable human-readable identifier;
- переносить logical project identity вместе с repository;
- использовать project identity в future cross-project references;
- отделить logical project identity от local machine registration.

В baseline model `project-key` хранится в `.hypergraph/project.toml`.

`Project-key` не является:
- local UUID регистрации;
- filesystem path;
- Git remote URL;
- гарантированно global unique identifier без отдельной policy.

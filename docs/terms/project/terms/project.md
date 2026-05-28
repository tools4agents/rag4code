# project

> Status: Draft  
> Scope: project-specific term for HyperGraph domain model  
> Related: `../terms-map.md`

`Project` — это доменная сущность HyperGraph, которая представляет один локальный engineering project с собственным root, config и производной graph database.

`Project` нужен, чтобы:
- явно отделять один indexed knowledge graph context от другого;
- связывать project root, project-local settings and derived graph state;
- выполнять CLI и MCP операции в конкретном project context;
- поддерживать будущую модель, где project сам может быть graph node во внешнем cross-project graph.

В первой итерации каждый `Project` имеет ровно один `project-root` и изолированную `project-database`.

`Project` не означает:
- Git repository как таковой;
- workspace с несколькими roots;
- автоматически связанный cross-project graph;
- deployment unit.

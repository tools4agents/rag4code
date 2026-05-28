# graph-node

> Status: Draft  
> Scope: project-specific term for HyperGraph graph model  
> Related: `../terms-map.md`

`Graph-node` — это vertex в graph representation HyperGraph, который представляет файл, инженерный artifact, термин, code artifact, project или другую domain entity.

`Graph-node` нужен, чтобы:
- задавать единицу graph relations;
- выполнять traversal по typed edges;
- фильтровать graph по type, tags and properties;
- строить impact analysis around affected artifacts.

В первой итерации primary `graph-node` — Markdown file. Future model допускает artifact-level nodes: term, ADR, requirement, user story, scenario, test case, code artifact and project.

`Graph-node` не равен обязательно одному physical file: в future semantic layer один file может быть container для нескольких semantic graph nodes.

# project-context-entry-system-asset

> Status: Draft  
> Scope: project-specific term for methodology asset taxonomy  
> Related: `../terms-map.md`

`Project-context-entry-system asset` — это asset type, который задает reusable систему project context entry points, loading order и ownership split между `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и related layers.

Этот asset type нужен, чтобы:

- делать инициализацию нового project context repeatable;
- держать `AGENTS.md` тонким router artifact;
- переносить baseline structure и templates между проектами;
- не смешивать durable context, engineering SoT и execution layer.

Concrete implementation этого asset type может включать:

- спецификацию самого asset-а;
- focused docs по `AGENTS.md`, `project/` и related files;
- reusable templates для project initialization.

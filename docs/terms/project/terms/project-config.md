# project-config

> Status: Draft  
> Scope: project-specific term for HyperGraph project settings model  
> Related: `../terms-map.md`

`Project-config` — это настройки одного `Project`, которые определяют project-local поведение HyperGraph.

`Project-config` нужен, чтобы хранить:
- root-related settings;
- include/exclude rules для индексации;
- настройки project-local database/indexing behavior;
- будущие project-specific graph semantics and conventions.

В первой итерации особенно важны exclude rules: пользователь сам задает, какие paths внутри `project-root` не должны анализироваться сервисом. Директория `.git` является hard-excluded всегда.

`Project-config` не является:
- Source of Truth для содержимого проекта;
- заменой `.gitignore`;
- глобальной настройкой всех проектов;
- architecture contract для конкретного storage backend.

# source-of-truth

> Status: Draft  
> Scope: project-specific term for HyperGraph state ownership model  
> Related: `../terms-map.md`

`Source-of-truth` — это слой или artifact, которому принадлежит authoritative state для конкретного вида знания или данных.

В HyperGraph first iteration project files под Git являются Source of Truth для содержимого проекта. `Project-database` хранит только derived representation, которую можно пересобрать из файлов.

Термин нужен, чтобы явно разделять:
- файловое содержимое проекта;
- Git version history;
- derived graph/index state;
- human-authored documentation semantics.

Для первой итерации действует инвариант:

```text
Git owns versioning.
Filesystem owns current project content.
HyperGraph database reflects indexed current state.
```

`Source-of-truth` не означает:
- что все данные обязаны жить в одном файле;
- что derived indexes нельзя хранить;
- что database может молча становиться authoritative вместо project files.

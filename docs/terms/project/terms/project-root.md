# project-root

> Status: Draft  
> Scope: project-specific term for HyperGraph project boundary model  
> Related: `../terms-map.md`

`Project-root` — это локальная filesystem директория, которая задает границу одного `Project` для индексации, анализа и файловых операций HyperGraph.

`Project-root` нужен, чтобы:
- нормализовать paths внутри проекта;
- ограничивать операции HyperGraph безопасной локальной областью;
- определять, какие файлы могут попасть в derived graph representation;
- отделять один project context от другого.

В первой итерации один `Project` имеет ровно один `project-root`.

`Project-root` не означает:
- multi-root workspace;
- Git repository boundary во всех случаях;
- автоматическую границу для nested repositories, если они не исключены через `project-config`.

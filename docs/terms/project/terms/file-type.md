# file-type

> Status: Draft  
> Scope: project-specific term for HyperGraph graph node classification  
> Related: `../terms-map.md`

`File-type` — это physical classification файла, из которого HyperGraph строит или может строить graph representation.

Примеры `file-type`:
- Markdown file: `*.md`;
- Python script/module: `*.py`;
- другие source/documentation formats в future scope.

`File-type` нужен, чтобы отделять physical nature artifact source от его semantic role. Например, Markdown file может быть term page, ADR или requirement document, а Python file может содержать module, class, function или test implementation.

`File-type` не равен `semantic-type`: один и тот же physical file type может содержать разные domain concepts.

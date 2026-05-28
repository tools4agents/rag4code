# semantic-type

> Status: Draft  
> Scope: project-specific term for HyperGraph graph node classification  
> Related: `../terms-map.md`

`Semantic-type` — это смысловая классификация graph node или artifact внутри HyperGraph.

Примеры `semantic-type`:
- `term` для term page;
- `ADR` для architectural decision record;
- `requirement`;
- `user-story`;
- `scenario`;
- `test-case`;
- `module`, `class`, `function`, `test-implementation` для future code graph.

`Semantic-type` нужен, чтобы:
- фильтровать graph nodes по смысловой роли;
- строить typed relations между artifacts;
- отделять physical source format от domain meaning;
- поддерживать future traceability and impact analysis.

`Semantic-type` не равен `file-type`: Markdown file может иметь semantic type `term`, а Python file может содержать несколько semantic nodes вроде class, function and test implementation.

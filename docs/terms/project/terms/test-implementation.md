# test-implementation

> Status: Draft  
> Scope: project-specific term for HyperGraph testing traceability model  
> Related: `../terms_map.md`

`Test-implementation` - это code-level реализация test case в test module, test class или test function.

Термин нужен, чтобы явно отделить:
- documentation-level `test-case`;
- suite-level navigation;
- конкретный код, который реально исполняется test runner.

`Test-implementation` может содержать structured metadata, например:
- `Suite: TS-...` на module level;
- `Test case: TC-...` в docstring test function;
- `Requirement: REQ-...` в docstring test function.

`Test-implementation` не является каноническим owner всей traceability semantics. Канонический source layer остается в testing documentation.

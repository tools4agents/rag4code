# test-case

> Status: Draft  
> Scope: project-specific term for HyperGraph testing traceability model  
> Related: `../terms_map.md`

`Test-case` - это минимальная documented verification unit внутри `test-suite`, которая имеет stable identifier и связывает requirement-level intent с конкретной test implementation.

`Test-case` нужен, чтобы:
- сделать traceability атомарной;
- дать агенту и человеку стабильную точку навигации;
- связывать documentation, suite и кодовую реализацию без зависимости от имени test function.

Обычно `test-case`:
- принадлежит одному `test-suite`;
- имеет identifier вида `TC-...`;
- ссылается на один или несколько requirement identifiers;
- materialize в одном или нескольких test implementations.

`Test-case` не равен:
- suite page;
- test module;
- имени test function в коде.

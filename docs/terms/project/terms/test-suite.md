# test-suite

> Status: Draft  
> Scope: project-specific term for HyperGraph testing traceability model  
> Related: `../terms_map.md`

`Test-suite` - это documentation unit, который объединяет связанный набор test cases, links на implementation roots и suite-level navigation metadata.

`Test-suite` нужен, чтобы:
- группировать связанные проверки в одну explainable область;
- связывать suite с upstream requirements или другими source artifacts;
- задавать documentation roots, implementation roots и search anchors;
- служить промежуточным звеном в цепочке `requirement -> suite -> test case -> test implementation`.

`Test-suite` не равен:
- одному test file;
- одному test case;
- execution report.

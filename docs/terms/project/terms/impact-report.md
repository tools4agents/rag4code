# impact-report

> Status: Draft  
> Scope: project-specific term for HyperGraph operation reporting model  
> Related: `../terms-map.md`

`Impact-report` — это explainable report, который показывает последствия planned или performed операции в HyperGraph.

`Impact-report` нужен, чтобы:
- показать affected files and graph nodes;
- перечислить incoming/outgoing references;
- отделить safe rewrites от unresolved или unsupported cases;
- дать человеку и агенту материал для осмысленной корректировки project files;
- сделать mutating и potentially destructive operations проверяемыми.

Для первой итерации ключевой special case — remove impact report: он показывает, какие files and references будут затронуты удалением, без автоматического destructive rewrite по умолчанию.

`Impact-report` не является:
- автоматическим планом выполнения всех изменений;
- гарантией, что semantic text correction не нужна;
- заменой review affected files.

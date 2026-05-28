# affected-file

> Status: Draft  
> Scope: project-specific term for HyperGraph impact analysis model  
> Related: `../terms-map.md`

`Affected-file` — это файл внутри `Project`, который может потребовать изменения, проверки или human/agent review из-за операции над другим artifact.

`Affected-file` нужен, чтобы:
- показывать blast radius операции;
- помогать агенту подкорректировать текст после удаления или перемещения linked document;
- явно отделять найденное влияние от автоматически примененного rewrite;
- формировать explainable reports для CLI и MCP users.

В первой итерации `affected-file` особенно важен для remove impact report: HyperGraph показывает файлы и места ссылок, которые будут затронуты удалением. HyperGraph строится на детерминированных алгоритмах и не переписывает смысл текста; смысловую корректировку выполняет человек или ИИ-агент, который использует HyperGraph через MCP или другой интерфейс.

`Affected-file` не означает:
- что файл уже изменен;
- что rewrite безопасен;
- что агент может пропустить semantic review.

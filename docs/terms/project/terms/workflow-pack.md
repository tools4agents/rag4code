# workflow-pack

> Status: Draft  
> Scope: project-specific term for HyperGraph artifact packaging model  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`workflow-pack` — это packaging boundary для одного `workflow`.

Он нужен, чтобы хранить связанные source artifacts workflow как согласованный package, не смешивая semantic process entity и filesystem layout.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:
- сам `workflow` как process map;
- физическую директорию, в которой лежат artifacts этого workflow;
- support artifacts, помогающие читать и поддерживать workflow;
- runtime materialization и execution state, которые не принадлежат source pack.

Без этого distinction легко спутать:
- процесс как смысловую сущность;
- markdown-файл с обзором процесса;
- директорию со связанными файлами;
- runtime entrypoint для агента.

## 3. Что может входить в `workflow-pack`

В `workflow-pack` могут входить:
- канонический workflow overview markdown;
- ссылки на связанные `workflow-step`;
- workflow-level metadata;
- общие references;
- support artifacts, относящиеся ко всему workflow.

При этом сам `workflow-pack` не должен подменять отдельные `workflow-step-pack`.

## 4. Важный invariant

`Workflow-pack` является packaging boundary, но не semantic collapse.

Это значит:
- файлы workflow могут лежать рядом внутри одной директории;
- но сам `workflow`, его шаги и support artifacts остаются разными сущностями;
- physical proximity не отменяет логических границ.

## 5. Что не стоит смешивать с `workflow-pack`

С `workflow-pack` не стоит смешивать:
- сам термин `workflow`;
- `workflow-step-pack`;
- `skill` как reusable capability;
- runtime materialization state;
- execution instance конкретного прогона workflow.

## 6. Связанные термины

`workflow-pack` нужно читать вместе с:
- `workflow`;
- `workflow-step`;
- `workflow-step-pack`;
- `skill`.

Этот термин нужен для artifact-oriented packaging model в HyperGraph.

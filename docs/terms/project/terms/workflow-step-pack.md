# workflow-step-pack

> Status: Draft  
> Scope: project-specific term for HyperGraph artifact packaging model  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`workflow-step-pack` — это packaging boundary для одного `workflow-step`.

Он нужен, чтобы хранить каноническое описание шага и все сопутствующие материалы как единый source package, не смешивая semantic step entity и filesystem layout.

## 2. Зачем нужен этот термин

Термин нужен, чтобы отделить:
- сам `workflow-step` как process unit;
- директорию, в которой лежат source artifacts этого шага;
- reusable `skills`, на которые шаг может ссылаться;
- runtime execution state, который не принадлежит source pack.

Без этого distinction легко спутать:
- шаг процесса;
- markdown-файл с описанием шага;
- templates и references для шага;
- reusable capabilities, применяемые внутри шага.

## 3. Что может входить в `workflow-step-pack`

В `workflow-step-pack` могут входить:
- канонический step markdown;
- templates и checklists;
- examples;
- references;
- дополнительные пояснения и support artifacts для шага.

При необходимости step-pack может ссылаться на reusable `skills`, но не должен копировать их смысл внутрь себя без необходимости.

## 4. Важный invariant

`Workflow-step-pack` является packaging boundary, но не semantic collapse.

Это значит:
- step description и support artifacts могут лежать рядом;
- но сам `workflow-step`, связанные `skills`, `step-vacancy` и runtime state остаются разными сущностями;
- physical proximity не отменяет логических границ.

## 5. Что не стоит смешивать с `workflow-step-pack`

С `workflow-step-pack` не стоит смешивать:
- сам термин `workflow-step`;
- `skill` как reusable capability;
- `agent-role` как reusable profile;
- runtime materialization state;
- execution instance шага.

## 6. Связанные термины

`workflow-step-pack` нужно читать вместе с:
- `workflow-step`;
- `workflow-pack`;
- `workflow`;
- `skill`;
- `step-vacancy`;
- `agent-role`.

Этот термин нужен для artifact-oriented packaging model в HyperGraph.

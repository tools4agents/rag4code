# workflow-step-gate

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`workflow-step-gate` — это specialized `workflow-step`, который принимает explicit readiness / eligibility / routing decision внутри workflow.

Он является обычным `workflow-step` по execution semantics, но имеет особую process role: проверить входные условия, зафиксировать verdict и направить workflow по следующему edge.

## 2. Зачем нужен этот термин

Термин нужен, чтобы не смешивать:

- обычный execution step, который создает или изменяет содержательный artifact;
- gate-step, который проверяет readiness и принимает routing decision;
- visual transition label на graph edge;
- human interaction node, где требуется external confirmation.

Для executable methodology workflow semantic gate не должен оставаться абстрактным нераскрытым условием.

Если routing decision требует inputs, checklist, verdict, rationale, handoff, observability или самостоятельной execution value, его нужно materialize-ить как `workflow-step-gate`.

Mermaid edge labels and simple transition labels may show routing outcomes, but they must not be treated as decision owners.

## 3. Связь с `workflow-step`

`workflow-step-gate` является подтипом `workflow-step`.

Это значит, что он наследует baseline expectations `workflow-step`:

- входы;
- действие;
- выходы;
- `DoD`;
- failure / return semantics;
- optional `step-vacancy` and `agent-role` assignment;
- optional handoff через `workflow-exchange layer`.

Отличие в том, что центральным output является не новый domain artifact, а explicit gate result.

## 4. Gate vs `workflow-step-gate`

В этой методологической модели `gate` не является самостоятельной executable process entity.

Allowed usage:

- как informal short name внутри названия конкретного `workflow-step-gate`, например `Intent Readiness Gate`;
- как visual label на transition edge, если решение уже принято конкретным step;
- как часть workflow-local terminology, если она ссылается на materialized gate-step.

Not allowed usage:

- оставить semantic routing decision как абстрактный gate без `STEP.md`;
- сказать агенту “пройти gate” без criteria, verdicts and rationale format;
- использовать edge label вместо observable decision artifact.

Policy for SDLC workflows:

```text
Every semantic routing decision is a workflow-step-gate.
```

Даже lightweight gate-step может быть коротким. Но он должен дать агенту понятные criteria, allowed verdicts, next path and required recorded rationale.

## 5. Что должен фиксировать `workflow-step-gate`

Минимально gate-step должен описывать:

- gate purpose;
- inputs required for the decision;
- readiness / eligibility checklist;
- allowed verdicts;
- meaning of each verdict;
- next path for each verdict;
- rationale format;
- handoff artifact, если следующий step зависит от gate result.
- expected operational artifact for the recorded decision.

## 6. Типичные verdicts

Verdicts зависят от конкретного workflow.

Примеры:

- `passed`;
- `blocked`;
- `pass-with-warnings`;
- `blocked-research`;
- `blocked-probe`;
- `split-required`;
- `defer`;
- `reject`.

Workflow-pack должен задавать локальный список verdicts и semantics для каждого gate-step, а не полагаться на неявные значения.

## 7. Что gate-step не должен делать

`workflow-step-gate` не должен:

- silently change source artifacts without recording the decision;
- подменять собой upstream analysis или implementation step;
- скрывать unresolved unknowns под verdict `passed`;
- принимать irreversible product, architecture или release decisions без rationale;
- смешивать gate result с user confirmation, если нужна отдельная human interaction node.
- оставлять semantic routing decision только в Mermaid edge label.

## 8. Примеры

Примеры gate-step:

- readiness gate перед release preparation;
- publication gate перед release publication;
- intent readiness gate перед переходом из discovery в system design;
- implementation readiness gate перед decomposition into tasks;
- documentation sync gate перед cleanup operational artifacts.

## 9. Связанные термины

`workflow-step-gate` нужно читать вместе с:

- [`workflow`](./workflow.md);
- [`workflow-step`](./workflow-step.md);
- [`workflow-pack`](./workflow-pack.md);
- [`workflow-step-pack`](./workflow-step-pack.md);
- [`workflow-exchange layer`](./workflow-exchange-layer.md);
- [`step-vacancy`](./step-vacancy.md);
- [`agent-role`](./agent-role.md).

Этот термин нужен для явного моделирования semantic gates как first-class executable process nodes, когда routing decision требует наблюдаемости, criteria и recorded rationale.

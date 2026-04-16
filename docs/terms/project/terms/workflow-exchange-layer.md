# workflow-exchange layer

> Status: Draft  
> Scope: project-specific term for HyperGraph methodology  
> Related: `docs/terms/project/terms-map.md`

## 1. Назначение термина

`workflow-exchange layer` — это временный workflow-specific exchange/handoff layer внутри [`Operational Documentation Layer`](./operational-documentation-layer.md), который хранит workflow-instance graph-state и handoff artifacts конкретного workflow-run.

Он нужен, чтобы отделить:

- `workflow` как semantic process map;
- `workflow-pack` как source packaging boundary;
- `workflow-step` как описание конкретной работы шага;
- временный execution-layer companion, через который агенты выполяющие шаги конкретного workflow-run обмениваются дополнительным контекстом и фиксируют текущее состояние графа исполнения.

## 2. Что хранится в `workflow-exchange layer`

На этом слое имеет смысл хранить:

- workflow-instance graph-state;
- handoff artifacts между шагами workflow;
- gate decisions и stage state;
- transition evidence и branch/eligibility decisions;
- run-specific scope decisions;
- explicit `handoff in` / `handoff out` материалы;
- remediation artifacts и return-to-graph artifacts для exception paths;
- временные execution notes, которые нужны следующему шагу, но не должны подменять SoT.

Этот слой предназначен именно для конкретного workflow-run, а не для долгоживущих архитектурных решений.

Важно:
- exchange layer не обязан хранить полный формальный snapshot всего graph runtime;
- но он должен хранить достаточный workflow-instance graph-state, чтобы следующий actor мог безопасно продолжить directed process graph.

## 3. Связь с knowledge lifecycle

По [`Documentation Lifecycle Layers`](../../../methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md) этот слой живет внутри [`Operational Documentation Layer`](./operational-documentation-layer.md).

Из этого следуют invariants:

- `workflow-exchange layer` не является [`Engineering Documentation SoT`](./engineering-documentation-sot.md);
- `workflow-exchange layer` не является [`Release Documentation Layer`](./release-documentation-layer.md);
- knowledge из этого слоя либо удаляется после завершения workflow-run, либо поднимается в SoT / release docs, если стало долгоживущим и publish-worthy.

## 4. Связь с `workflow`

`Workflow` может иметь свой `workflow-exchange layer`, если workflow реально исполняется как multi-step или multi-agent directed process graph.

Это означает:

- один и тот же reusable `workflow` может иметь однотипный exchange pattern;
- конкретный project-local путь exchange layer задается самим проектом или workflow-pack;
- exchange layer не является частью канонического определения workflow, а является execution-layer companion для конкретных прогонов.
- exchange layer поддерживает не только linear handoff, но и conditional transitions, blocked gates, exception branches и remediation loops.

## 5. Связь с `workflow-step`

`Workflow-step` может требовать:

- static context из workflow-pack, project context и SoT;
- `handoff in` из `workflow-exchange layer`;
- `handoff out` в тот же `workflow-exchange layer` для следующего шага.

То есть exchange layer помогает шагам обмениваться run-specific контекстом, которого нет в reusable описании шага.

Если workflow не линейный, exchange layer дополнительно помогает шагам понять:
- на какой вершине графа сейчас находится run;
- какие gates уже passed или blocked;
- какой transition path сейчас допустим;
- требуется ли возврат в graph после remediation.

## 6. Что не стоит смешивать с `workflow-exchange layer`

С этим термином не стоит смешивать:

- `workflow` как process entity;
- `workflow-pack` как source package;
- `workflow-step-pack` как packaging boundary шага;
- `task artifact` или `plan artifact` как общие execution artifacts проекта;
- Engineering SoT;
- release notes и другой `Release Documentation Layer`.

## 7. Почему это важно

Явное введение `workflow-exchange layer` нужно, чтобы:

- не перегружать reusable workflow и step definitions run-specific деталями;
- не пытаться хранить временный handoff context в SoT;
- поддерживать directed process graph execution, а не только линейный handoff между шагами;
- сделать multi-agent execution workflow прозрачнее;
- дать clean boundary для disposable execution-time exchange artifacts.

## 8. Связанные термины

`workflow-exchange layer` нужно читать вместе с:

- `workflow`;
- `workflow-step`;
- `workflow-pack`;
- `step-vacancy`;
- [`Operational Documentation Layer`](./operational-documentation-layer.md);
- [`Engineering Documentation SoT`](./engineering-documentation-sot.md);
- [`Release Documentation Layer`](./release-documentation-layer.md).

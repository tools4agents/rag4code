# Task: Design process workflow — Initiative Workspace Preparation

## Контекст

В текущем `Stage 01 — Discovery & Intent Framing` смешаны разные ответственности:

- подготовка рабочей области для размышлений;
- exploratory / opportunity discovery;
- Product Design внутри Early Design Convergence Loop.

По результатам разбора finding `Stage 01 противоречиво позиционирован: часть loop или pre-loop gate` принято решение развести эти ответственности.

`Initiative Workspace Preparation` должен стать отдельным process workflow: он готовит operational workspace, сохраняет provenance/source links и классифицирует входной сигнал, но не принимает product/system/architecture decisions.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)

### Current Stage 01 and findings

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- [`critic_early_design_loop_findings.md`](../findings/critic_early_design_loop_findings.md)

### Related resources

- [`early-design-stage-boundaries.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/early-design-stage-boundaries.md)
- [`discovery-workspace-lifecycle.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/resources/discovery-workspace-lifecycle.md)
- [`discovery-index.template.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/resources/discovery-index.template.md)
- [`source-links.template.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/resources/source-links.template.md)

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Спроектировать и materialize-ить отдельный process workflow `Initiative Workspace Preparation`.

Workflow должен отвечать за:

1. intake входного сигнала;
2. context classification;
3. initiative/workspace slug selection;
4. workspace activation or reuse;
5. source links and provenance preservation;
6. initial file map / index / next-step marker;
7. route decision: Opportunity Discovery, Product Design, Research/Spike, backlog/defer/reject или другой downstream workflow.

## Scope

Включить:

- process workflow graph;
- step vertices and gate vertices;
- happy path and return/remediation paths;
- правила создания/reuse workspace в `operational_scope/`;
- source link preservation rules;
- route decision rules для downstream workflows;
- explicit boundary: workspace preparation does not own product/system/architecture decisions;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- Product Design decisions;
- exploratory opportunity research content;
- system boundary design;
- architecture design;
- implementation planning;
- production code.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- является ли `Initiative Workspace Preparation` обязательным pre-step для всех initiatives или только для non-trivial work;
- где canonical workspace должен жить для разных типов работы: discovery, product design, research, planning;
- нужно ли сохранять существующий `operational_scope/discovery/<initiative-slug>/` или ввести более общий `operational_scope/initiatives/<initiative-slug>/`;
- какие route verdicts нужны;
- какие artifacts должны быть reusable downstream без превращения их в durable SoT.

## Expected output

После выполнения задачи должны появиться или быть обновлены:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/
  README.md
  workflow.md
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

Возможно обновление current Stage 01 resources, если workspace lifecycle будет вынесен из Stage 01.

## Definition of Done

- [ ] План workflow steps обсужден с человеком до создания step packs.
- [ ] `Initiative Workspace Preparation` оформлен как process workflow, не как SDLC delivery stage.
- [ ] Workflow явно отделяет workspace mechanics от Product Design and Opportunity Discovery.
- [ ] Route verdicts зафиксированы и linkable to downstream workflows.
- [ ] Existing Stage 01 workspace-related content либо переиспользован, либо помечен к migration.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: обсудить с человеком boundaries and route verdicts.
- Blockers: none
- Verification: pending

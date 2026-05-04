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

- Current State: in_progress — baseline workflow-pack materialized; key decision resources for handling classes, route decisions, workspace decisions, split handling, duplicate handling, source links schema, initiative index template and preparation decisions template created; operational artifact path rules and task-management scope model updated; detailed `STEP.md` / `vacancy.md` files not created yet.
- Next Step: decide migration policy for existing `operational_scope/discovery/<initiative-slug>/` workspaces or define detailed return/remediation paths for gates.
- Blockers: none
- Contract Changes: present — methodology workflow docs and stage naming updated.
- Verification: read/grep consistency checks only; no automated test command run because changes are documentation/process artifacts.

## Handoff Notes

### What is done

- Created baseline process workflow-pack:
  - [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/README.md)
  - [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/workflow.md)
- Fixed canonical initiative workspace root:
  - `operational_scope/initiatives/<initiative-slug>/`
- Created reusable methodology resource for handling classification:
  - [`work-item-handling-classes.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/work-item-handling-classes.md)
  - Handling classes fixed: `trivial-direct`, `standard-initiative`, `major-initiative`, `unclear-initiative`.
  - `unclear-initiative` enters through `Discovery`; Discovery may use Research / Deep Research / Spike and then reclassifies the initiative.
- Created workflow-local route resources:
  - [`route-decision-model.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/route-decision-model.md)
  - [`route-backlog-defer.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/route-backlog-defer.md)
  - Route model fixed: single route uses `primary-route` + `route-rationale`; multiple routes add `recommended-route-set` + `route-ordering`; `route-blocked` requires `blocked-by`.
- Created workflow-local workspace decision resource:
  - [`workspace-decision-model.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/workspace-decision-model.md)
  - Workspace verdicts fixed: `workspace-create-new`, `workspace-reuse-existing`, `workspace-merge-into-existing`, `workspace-stop-duplicate`, `workspace-split-required`, `workspace-conflict-human-clarification`.
  - `reuse` means target workspace explicit/obvious before analysis; `merge` means target chosen after semantic comparison and should be human-confirmed.
  - `workspace-stop-duplicate` annotates the input artifact as adding no new value; it does not delete artifacts automatically.
- Created workflow-local split handling resource:
  - [`split-handling.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/split-handling.md)
  - Split is fixed as gate/input handling verdict, not `index.md` preparation status.
  - Parent source split does not create parent initiative workspace; child initiatives receive independent workspaces and reference parent via `Relationship: split-origin`.
- Created workflow-local duplicate handling resource:
  - [`duplicate-handling.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/duplicate-handling.md)
  - `workspace-stop-duplicate` annotates input artifact only, does not update workspace and does not delete artifacts automatically.
- Created workflow-local source links schema:
  - [`source-links-schema.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/source-links-schema.md)
  - `source-links.md` required tables fixed: `Source artifacts` with `Source | Type | Status | Relationship | Notes`, and `Source decisions` with `Source | Decision | Rationale`.
  - `Type`, `Status`, `Relationship` catalogs are recommended and extensible; `split-origin` is used instead of `child-source`.
- Created workflow-local workspace artifact templates:
  - [`initiative-index-template.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/initiative-index-template.md)
  - [`preparation-decisions-template.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/resources/preparation-decisions-template.md)
- Updated task-management path model:
  - [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
  - [`operational-artifact-path-rules.md`](../../docs/methodology-layer/assets/task-management/resources/operational-artifact-path-rules.md)
  - [`task-map.template.md`](../../docs/methodology-layer/assets/task-management/resources/task-map.template.md)
  - Initiative-scoped tasks now live under `operational_scope/initiatives/<initiative-slug>/tasks/<task-type>/`.
  - Unscoped tasks live under `operational_scope/tasks/<task-type>/`.
  - Evidence outputs live outside `tasks/` under the matching evidence artifact area.
  - `task-management-learner` marked as legacy reference.
- Created general resource placement guideline:
  - [`resource-placement-guidelines.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/resource-placement-guidelines.md)
- Renamed Stage 05 across methodology assets from `Delivery Planning & Task Decomposition` to `Execution Planning & Task Decomposition`:
  - [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-execution-planning-task-decomposition/README.md)
  - [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/05-execution-planning-task-decomposition/workflow.md)
  - [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
  - [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
  - [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
  - [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
  - [`baseline-v0.md`](../../assets/metodologes/waterfall/software-development-methodology/decisions/baseline-v0.md)
  - [`task-map.md`](../task-map.md)
  - [`wf-013-design-stage-05-execution-planning-task-decomposition-internal-steps.md`](./wf-013-design-stage-05-execution-planning-task-decomposition-internal-steps.md)

### Immediate fix first

Discuss the next open question: migration policy for existing `operational_scope/discovery/<initiative-slug>/` workspaces or detailed return/remediation paths for gates.

### Pending work

- Decide migration policy for existing `operational_scope/discovery/<initiative-slug>/` workspaces. Context note: this workflow has not yet been applied to any project, so there are no real project migrations; question is mostly about Stage 01 legacy resource compatibility.
- Define detailed return/remediation paths for each gate.
- After open questions are resolved, materialize `steps/<step-slug>/STEP.md` and `steps/<step-slug>/vacancy.md` for agreed steps.
- Update Stage 01 / discovery workspace resources if needed after finalizing initiative workspace lifecycle.

### Commands to run

```bash
cd /data/develop/education/hyper-projects/hyper-graph
rg "work-item-triviality-boundaries|Delivery Planning|05-delivery-planning-task-decomposition" assets/metodologes/waterfall/software-development-methodology operational_scope
rg "source-links-schema|route-decision-model|workspace-decision-model|split-handling|duplicate-handling|preparation-decisions-template|work-item-handling-classes" assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation assets/metodologes/waterfall/software-development-methodology/resources
rg "tasks/<initiative-slug>|tasks/<scope-slug>|tasks/trivial|<initiative-slug>/evidence" docs/methodology-layer/assets/task-management assets/metodologes/waterfall/software-development-methodology/resources
```

### User constraints

- Рабочий язык documentation: русский, но accepted English terms and stage/workflow names remain English.
- Do not create `STEP.md` / `vacancy.md` until workflow steps and open questions are agreed with the human.
- Apply documentation granularity rules from [`documentation-navigation-and-granularity.md`](../../assets/rules/rules-documentation/documentation-navigation-and-granularity.md): keep runtime-focused docs small, move detailed local semantics into focused resources, and link instead of duplicating.
- Route decisions are recommendations for human-orchestrated execution, not automatic workflow execution.
- New entities/fields should follow Occam's razor: add them only when actually needed.

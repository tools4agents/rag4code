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

- human-orchestrated workflow overview;
- agreed lightweight steps and happy path;
- `STEP.md` для каждого agreed step as focus/guidance artifact;
- правила создания/reuse workspace в `operational_scope/`;
- source link preservation rules;
- route recommendation guidance для downstream workflows;
- explicit boundary: workspace preparation does not own product/system/architecture decisions.

Не включать:

- Product Design decisions;
- exploratory opportunity research content;
- system boundary design;
- architecture design;
- implementation planning;
- production code;
- strict gate verdict contracts;
- full Mermaid graph with return/remediation paths;
- exact input/output schemas between agents;
- `vacancy.md` files.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- является ли `Initiative Workspace Preparation` обязательным pre-step для всех initiatives или только для non-trivial work;
- где canonical workspace должен жить для разных типов работы: discovery, product design, research, planning;
- нужно ли сохранять существующий `operational_scope/discovery/<initiative-slug>/` или ввести более общий `operational_scope/initiatives/<initiative-slug>/`;
- какие route recommendations нужны;
- какие artifacts должны быть reusable downstream без превращения их в durable SoT.

## Expected output

После выполнения задачи должны появиться или быть обновлены:

```text
assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/
  README.md
  workflow.md
  steps/<step-slug>/STEP.md
```

Возможно обновление current Stage 01 resources, если workspace lifecycle будет вынесен из Stage 01.

## Definition of Done

- [x] План workflow steps обсужден с человеком до создания step packs.
- [x] `Initiative Workspace Preparation` оформлен как process workflow, не как SDLC delivery stage.
- [x] Workflow явно отделяет workspace mechanics от Product Design and Opportunity Discovery.
- [x] Route recommendations зафиксированы and linkable to downstream workflows without strict gate contract.
- [ ] Existing Stage 01 workspace-related content либо переиспользован, либо помечен к migration. Не входит в completed draft; оставить как follow-up для Stage 01/Product Design compatibility work.
- [x] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [x] `vacancy.md` intentionally not created under the updated human-orchestrated draft mode.
- [x] Links and terminology follow documentation rules for the completed draft scope.

## Execution Status

- Current State: completed as draft — `Initiative Workspace Preparation` materialized as human-orchestrated draft workflow; `workflow.md`, `README.md` and lightweight `STEP.md` files exist; `vacancy.md`, strict gate verdict contracts and full return/remediation graph intentionally not created.
- Next Step: use this draft in real project work. If legacy Stage 01 workspace resources become relevant, handle compatibility/migration in a follow-up task tied to Stage 01/Product Design redesign or workflow graph synchronization.
- Blockers: none
- Contract Changes: present — methodology workflow docs, task-management SoT, path rules and stage naming updated.
- Verification: read/grep consistency checks only; no automated test command run because changes are documentation/process artifacts.

## Handoff Notes

### Draft completion handoff

- Completed draft artifacts:
  - [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/README.md)
  - [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/workflow.md)
  - [`steps/01-incoming-signal-intake/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/01-incoming-signal-intake/STEP.md)
  - [`steps/02-context-classification/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/02-context-classification/STEP.md)
  - [`steps/03-initiative-identity-slug-selection/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/03-initiative-identity-slug-selection/STEP.md)
  - [`steps/04-workspace-decision/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/04-workspace-decision/STEP.md)
  - [`steps/05-workspace-activation-reuse/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/05-workspace-activation-reuse/STEP.md)
  - [`steps/06-source-links-provenance-preservation/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/06-source-links-provenance-preservation/STEP.md)
  - [`steps/07-initial-workspace-index/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/07-initial-workspace-index/STEP.md)
  - [`steps/08-downstream-route-recommendation/STEP.md`](../../assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation/steps/08-downstream-route-recommendation/STEP.md)
- Current design mode: human-orchestrated draft. Человек управляет order, returns and handoffs; workflow фиксирует happy path and step focus only.
- Explicitly postponed: `vacancy.md`, strict gate verdict contracts, exact input/output schemas between agents, full transition graph and legacy Stage 01 workspace migration.
- Supporting methodology additions created during this task:
  - [`human-orchestrated-stage-draft-authoring.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/human-orchestrated-stage-draft-authoring.md)
  - [`human-orchestrated-sdlc-evolution-pattern.md`](../../docs/methodology-layer/patterns/human-orchestrated-sdlc-evolution-pattern.md)
- Status in [`task-map.md`](../task-map.md): `completed as draft`.

### Previous conversation recall

- Current session title for local recall: `Подготовка workspace для wf-019`.
- A new agent can use the local conversation recall tool to search/read this session if more detailed discussion context is needed.
- Earlier relevant session title: `Шаги этапа Initiative Workspace Preparation`.

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
- Discussed and tentatively aligned on the “diploma model” for operational artifacts:
  - `operational_scope/inputs/<artifact-type>/` is the raw/external input inbox.
  - Initiative workspace is a namespace for processed local context, scoped tasks and scoped evidence outputs.
  - `source-links.md` remains useful as a bibliography/provenance map for external inputs, not as a replacement for local working artifacts.
  - `Context Intake` steps in Discovery/Product/System/Architecture workflows should be understood as converting external/raw context plus SoT into local stage-ready workspace context.
  - Execution task outputs are the project changes themselves (`docs/`, code, tests, contracts, etc.); no separate operational output folder is needed for execution results.
- Created general resource placement guideline:
  - [`resource-placement-guidelines.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/resource-placement-guidelines.md)
- Created reusable methodology resource for the “diploma model”:
  - [`operational-workspace-diploma-model.md`](../../assets/metodologes/waterfall/software-development-methodology/resources/operational-workspace-diploma-model.md)
  - Raw inputs live in `operational_scope/inputs/<artifact-type>/`.
  - `source-links.md` acts as bibliography/provenance map, not as local working context.
  - Initiative workspace owns processed local context, scoped tasks and scoped evidence outputs.
  - Context Intake converts external/raw context plus SoT into local stage-ready workspace context.
  - Accepted results materialize into durable SoT and cleanup prevents hidden competing SoT.
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

### Follow-up candidates after completed draft

These items are outside the completed draft scope and can be handled later if real usage shows they are needed:

1. Whether to update `initiative-index-template.md` minimal workspace shape/file map to mention local processed context areas, scoped tasks and evidence outputs.
2. Whether to update Stage 01/Product Design, Stage 02 and Stage 03 `Context Intake` step semantics later so they explicitly create/update local stage-ready workspace context instead of just collecting links.
3. Whether old `operational_scope/discovery/<initiative-slug>/` Stage 01 resources need compatibility notes or migration policy.

### Post-draft postponed work

- Decide whether `source-links-schema.md` needs structural changes after its role was clarified as bibliography/provenance map.
- Decide whether initiative workspace minimal shape stays `index.md`, `source-links.md`, `preparation-decisions.md` only, or should mention optional local areas (`tasks/`, `research/`, `deep-research/`, `spikes/`, stage-local context folders) in `initiative-index-template.md`.
- Decide how `Context Intake` in Stage 01/Product Design, Stage 02 Architecture Design and Stage 03 System Design should relate to initiative workspace local context. Current Stage 02/03 docs describe context reconstruction but not yet the “external input -> local processed context -> SoT” model explicitly.
- Decide migration policy for existing `operational_scope/discovery/<initiative-slug>/` workspaces. Context note: this workflow has not yet been applied to any project, so there are no real project migrations; question is mostly about Stage 01 legacy resource compatibility.
- Do not materialize `vacancy.md` files in the current draft mode.
- Update Stage 01 / discovery workspace resources if needed after finalizing initiative workspace lifecycle.
- Later cleanup/update outside immediate IWP scope: align operational skills (`task-materializer`, `taskset-materializer`, `active-task-setter`, research/spike setters) with the new task-management SoT and path rules. `task-management-learner` is legacy and should not drive the new SDLC model.

### Commands to run

```bash
cd /data/develop/education/hyper-projects/hyper-graph
rg "work-item-triviality-boundaries|Delivery Planning|05-delivery-planning-task-decomposition" assets/metodologes/waterfall/software-development-methodology operational_scope
rg "source-links-schema|route-decision-model|workspace-decision-model|split-handling|duplicate-handling|preparation-decisions-template|work-item-handling-classes" assets/metodologes/waterfall/software-development-methodology/workflows/initiative-workspace-preparation assets/metodologes/waterfall/software-development-methodology/resources
rg "tasks/<initiative-slug>|tasks/<scope-slug>|tasks/trivial|<initiative-slug>/evidence" docs/methodology-layer/assets/task-management assets/metodologes/waterfall/software-development-methodology/resources
rg "operational-artifact-path-rules|operational_scope/inputs|source-links.md|Context Intake" docs/methodology-layer/assets/task-management assets/metodologes/waterfall/software-development-methodology
```

### User constraints

- Рабочий язык documentation: русский, но accepted English terms and stage/workflow names remain English.
- Do not create `vacancy.md` in the current human-orchestrated draft mode.
- Apply documentation granularity rules from [`documentation-navigation-and-granularity.md`](../../assets/rules/rules-documentation/documentation-navigation-and-granularity.md): keep runtime-focused docs small, move detailed local semantics into focused resources, and link instead of duplicating.
- Route decisions are recommendations for human-orchestrated execution, not automatic workflow execution.
- New entities/fields should follow Occam's razor: add them only when actually needed.

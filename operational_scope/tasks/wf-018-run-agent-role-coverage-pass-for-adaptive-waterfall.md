# Task: Run agent-role coverage pass for Adaptive Waterfall internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` теперь содержит:

- SDLC stage workflows;
- process workflows;
- cross-cutting workflows;
- future `workflow-step` and `workflow-step-gate` packs with `vacancy.md`.

Эту задачу нужно выполнять только после того, как internal steps and vacancies будут materialized для всех stage/process workflows из текущей серии задач:

- `wf-008` — Stage 02 Architecture Design;
- `wf-009` — Stage 03 System Design;
- `wf-010` — Design Baseline Consolidation;
- `wf-011` — Stage 04 Test Design;
- `wf-012` — Pre-Planning Baseline Freeze;
- `wf-013` — Stage 05 Execution Planning & Task Decomposition;
- `wf-014` — Stage 06 Task Implementation;
- `wf-015` — Stage 07 Integration & Verification;
- `wf-016` — Stage 08 Engineering Docs & Knowledge Sync;
- `wf-017` — Stage 09 Release & Cleanup.

Цель этой задачи — не придумывать роли абстрактно, а вывести role coverage из фактических `vacancy.md`.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Stage and process workflows

Read all workflow docs under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/
assets/metodologes/waterfall/software-development-methodology/workflows/
```

Read all `vacancy.md` files under:

```text
assets/metodologes/waterfall/software-development-methodology/stages/**/steps/*/vacancy.md
assets/metodologes/waterfall/software-development-methodology/workflows/**/steps/*/vacancy.md
```

### Terms and prompt-steering context

- [`agent-role`](../../docs/terms/project/terms/agent-role.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)
- [`prompt-steering`](../../docs/terms/project/terms/resources/step-vacancy/prompt-steering.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-exchange layer`](../../docs/terms/project/terms/workflow-exchange-layer.md)

### Existing roles and agents

- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- project-local `.kilo/agent/` or `.kilo/agents/`, если такие есть;
- available built-in or runtime roles in the current Kilo environment;
- external assets listed in [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md).

## Цель

Сопоставить все actual `step-vacancy` requirements с существующими conceptual roles, runtime agents and reusable assets.

Нужно понять:

- какие role needs уже покрыты существующими roles/agents;
- какие role needs можно закрывать generic roles;
- какие role needs повторяются и требуют future `agent-role` materialization;
- какие roles в `roles.md` устарели или не соответствуют новой stage/process workflow model;
- какие external assets нужно добавить или уточнить в `agent-assets-registry.md`.

## Scope

Включить:

- сбор всех `vacancy.md` из stage workflows and process workflows;
- построение matrix `workflow -> step -> vacancy -> required steering -> suitable existing roles -> coverage gap`;
- проверку consistency между `roles.md`, actual vacancies and workflow graph;
- проверку, что `agent-assets-registry.md` покрывает referenced skills/assets;
- рекомендации по обновлению `roles.md`;
- рекомендации по созданию новых agent-role assets, если есть repeated role gap;
- follow-up tasks на role/materialization work, если нужно.

Не включать:

- немедленное создание всех новых agent roles без подтвержденной повторяемой потребности;
- изменение built-in runtime roles;
- переписывание stage workflows кроме small consistency fixes;
- создание production code;
- изменение methodology graph без отдельного architecture/design решения.

## Suggested discussion topics

Перед изменением `roles.md` обсудить с человеком:

- какие vacancies действительно требуют отдельной specialized role;
- какие vacancies можно покрыть existing `architect`, `critic`, `general`, `explore`, researcher-like или implementation roles;
- где достаточно conceptual workflow role без materialized `.kilo/agent`;
- какие gaps являются temporary и должны ждать практического использования;
- какие role names должны стать canonical;
- нужно ли расширять `agent-assets-registry.md`.

## Expected output

Ожидаемые outputs:

```text
operational_scope/...
  role-coverage-matrix.md              # exact location to be chosen during task execution
```

И при необходимости updates:

```text
assets/metodologes/waterfall/software-development-methodology/roles.md
assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md
operational_scope/tasks/<new-follow-up-task>.md
```

## Definition of Done

- [ ] Все `vacancy.md` из stage/process workflows прочитаны.
- [ ] Построена role coverage matrix.
- [ ] Existing roles and runtime agents сопоставлены с actual vacancy requirements.
- [ ] Repeated role gaps identified.
- [ ] `roles.md` обновлен или явно подтвержден как sufficient for current stage.
- [ ] `agent-assets-registry.md` обновлен, если workflow steps ссылаются на новые external assets.
- [ ] Follow-up tasks созданы для missing roles/assets, если materialization нужна.
- [ ] Не создано лишних agent roles без repeated vacancy pattern.

## Execution Status

- Current State: queued
- Next Step: Выполнить после завершения `wf-008`–`wf-017` и materialization всех internal step packs / vacancies.
- Blockers: internal steps and vacancies must exist first.
- Verification: Проверить, что role recommendations выводятся из actual `vacancy.md`, а не из абстрактных предположений.

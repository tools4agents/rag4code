# Task: Run agent-role coverage pass for Adaptive Waterfall

## Контекст

После создания черновиков всех stage workflows `02`–`07` нужно пройти по всем `vacancy.md` и понять, какие agent roles реально нужны методологии `Adaptive Waterfall for Agents`.

Это follow-up после проектирования stage workflows. Его не нужно выполнять до завершения `wf-001`–`wf-006`, потому что roles должны выводиться из фактических `workflow-step` and `workflow-step-gate` vacancies, а не из абстрактного списка.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`baseline-v0.md`](../../assets/metodologes/waterfall/software-development-methodology/decisions/baseline-v0.md)

### Stage workflows and vacancies

- [`01-discovery-intent-framing/workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/01-discovery-intent-framing/workflow.md)
- All `vacancy.md` files under `assets/metodologes/waterfall/software-development-methodology/stages/`.
- Stage 02 workflow produced by [`wf-001`](./wf-001-design-stage-02-product-specification-system-design.md).
- Stage 03 workflow produced by [`wf-002`](./wf-002-design-stage-03-delivery-planning-task-decomposition.md).
- Stage 04 workflow produced by [`wf-003`](./wf-003-design-stage-04-task-implementation.md).
- Stage 05 workflow produced by [`wf-004`](./wf-004-design-stage-05-integration-verification.md).
- Stage 06 workflow produced by [`wf-005`](./wf-005-design-stage-06-engineering-docs-knowledge-sync.md).
- Stage 07 workflow produced by [`wf-006`](./wf-006-design-stage-07-release-cleanup.md).

### Terms and prompt-steering context

- [`agent-role.md`](../../docs/terms/project/terms/agent-role.md)
- [`step-vacancy.md`](../../docs/terms/project/terms/step-vacancy.md)
- [`prompt-steering.md`](../../docs/terms/project/terms/resources/step-vacancy/prompt-steering.md)
- [`workflow-step.md`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate.md`](../../docs/terms/project/terms/workflow-step-gate.md)

### Existing runtime roles

- [`.kilo/agents/critic.md`](../../.kilo/agents/critic.md)
- [`.kilo/agents/deep-researcher.md`](../../.kilo/agents/deep-researcher.md)
- Existing active/built-in roles to consider: `architect`, `code`, `debug`, `general`, `explore`.

## Цель

Сопоставить все `step-vacancy` requirements с существующими roles and agents, выявить gaps и обновить role catalog.

## Scope

Включить:

- собрать список всех `vacancy.md`;
- построить matrix `workflow-step -> vacancy -> required steering -> suitable existing roles -> coverage gap`;
- определить, какие role needs покрываются существующими `.kilo/agents` и built-in roles;
- определить, какие roles пока можно оставить conceptual workflow roles;
- определить, какие roles нужно materialize-ить как новые `.kilo/agents/*.md` или future agent-role assets;
- обновить [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md) по результатам;
- при необходимости создать follow-up tasks на новые agent-role definitions.

Не включать:

- немедленное создание всех новых agent roles без подтвержденной повторяемой потребности;
- изменение системных промптов built-in roles;
- переписывание stage workflows, кроме мелких ссылочных/consistency fixes.

## Dependencies

Эта задача должна выполняться после:

- [`wf-001`](./wf-001-design-stage-02-product-specification-system-design.md)
- [`wf-002`](./wf-002-design-stage-03-delivery-planning-task-decomposition.md)
- [`wf-003`](./wf-003-design-stage-04-task-implementation.md)
- [`wf-004`](./wf-004-design-stage-05-integration-verification.md)
- [`wf-005`](./wf-005-design-stage-06-engineering-docs-knowledge-sync.md)
- [`wf-006`](./wf-006-design-stage-07-release-cleanup.md)

## Expected output

Ожидаемый результат:

- role coverage matrix в `operational_scope/` или внутри methodology resources;
- updated `roles.md`;
- список role gaps;
- follow-up tasks на materialization новых roles, если они действительно нужны.

## Definition of Done

- [ ] Все `vacancy.md` Stage 01–07 прочитаны.
- [ ] Есть matrix `step -> required steering -> existing role coverage -> gap`.
- [ ] Existing roles `.kilo/agents/critic.md`, `.kilo/agents/deep-researcher.md`, active `architect`, built-in `code`, `debug`, `general`, `explore` учтены.
- [ ] `roles.md` обновлен или явно подтвержден как достаточный.
- [ ] Для missing roles созданы follow-up tasks или явно зафиксировано, почему отдельная роль пока не нужна.
- [ ] Не создано лишних `agent-role` без повторяемого vacancy pattern.

## Execution Status

- Current State: queued
- Next Step: Выполнить после завершения `wf-001`–`wf-006`.
- Blockers: stage workflows 02–07 еще не materialized.
- Verification: Проверить, что role recommendations выводятся из `vacancy.md`, а не из абстрактных предположений.

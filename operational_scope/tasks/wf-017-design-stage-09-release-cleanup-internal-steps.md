# Task: Design Stage 09 — Release & Cleanup internal steps

## Контекст

Новая модель `Adaptive Waterfall for Agents` разделяет SDLC stage workflows и process workflows.

`Stage 09 — Release & Cleanup` уже имеет stage workflow-pack:

```text
assets/metodologes/waterfall/software-development-methodology/stages/09-release-cleanup/
  README.md
  workflow.md
```

Этот stage идет после `Stage 08 — Engineering Docs & Knowledge Sync` и закрывает workflow run:

```text
Engineering Docs & Knowledge Sync
  -> Release & Cleanup
  -> workflow run closed
```

`Release & Cleanup` готовит или обновляет release docs, фиксирует final delivery state и очищает temporary operational context без потери durable knowledge.

Важно различать:

- `docs/` — внутренняя engineering documentation для команды и агентов;
- release docs — user-facing documentation для опубликованного релиза, например Docusaurus, changelog, GitHub Releases, user guide, migration notes or upgrade guide.

Release docs не заменяют Engineering Documentation SoT.

## Обязательный reading context

Перед выполнением задачи прочитать:

### Methodology baseline

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/workflow.md)
- [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md)
- [`roles.md`](../../assets/metodologes/waterfall/software-development-methodology/roles.md)
- [`principles.md`](../../assets/metodologes/waterfall/software-development-methodology/principles.md)

### Target stage

- [`README.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/09-release-cleanup/README.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/09-release-cleanup/workflow.md)

### Adjacent workflow context

- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/08-engineering-docs-knowledge-sync/workflow.md)
- [`workflow.md`](../../assets/metodologes/waterfall/software-development-methodology/stages/07-integration-verification/workflow.md)

### Required dependent assets

- [`documentation-lifecycle-layers.md`](../../docs/methodology-layer/assets/knowledge-lifecycle/documentation-lifecycle-layers.md)
- [`task-map.md`](../../docs/methodology-layer/assets/task-management/task-map.md)
- [`terms-map.md`](../../docs/methodology-layer/assets/terms-management/terms-map.md)
- [`rules-documentation`](../../assets/rules/rules-documentation)

### Related assets

Use [`agent-assets-registry.md`](../../assets/metodologes/waterfall/software-development-methodology/agent-assets-registry.md) for external asset paths.

Relevant assets include:

- Documentation Rules;
- Task Management;
- Testing System;
- project-specific release workflow or publishing policy, если он существует.

### Workflow terms

- [`workflow`](../../docs/terms/project/terms/workflow.md)
- [`workflow-pack`](../../docs/terms/project/terms/workflow-pack.md)
- [`workflow-step`](../../docs/terms/project/terms/workflow-step.md)
- [`workflow-step-gate`](../../docs/terms/project/terms/workflow-step-gate.md)
- [`workflow-step-pack`](../../docs/terms/project/terms/workflow-step-pack.md)
- [`workflow-exchange layer`](../../docs/terms/project/terms/workflow-exchange-layer.md)
- [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md)

## Цель

Проработать internal steps для `Stage 09 — Release & Cleanup` по схеме:

1. обсудить с человеком план внутренних `workflow-step` and `workflow-step-gate`;
2. после согласования зафиксировать план в stage `workflow.md`;
3. создать `steps/<step-slug>/STEP.md` для каждого согласованного step;
4. создать `vacancy.md` для каждого step pack;
5. проверить согласованность stage workflow, step packs, vacancies and top-level methodology graph.

## Scope

Включить:

- Release & Cleanup internal workflow graph;
- список step vertices and gate vertices;
- happy path and return/remediation paths;
- intake from Engineering Docs & Knowledge Sync;
- release readiness validation;
- release docs update/preparation flow;
- changelog / release notes / GitHub release inputs when applicable;
- distinction between engineering SoT and release docs;
- final task-map state check;
- verification evidence and docs sync evidence availability check;
- operational artifact cleanup/archive/retention policy;
- check that operational artifacts do not contain hidden durable decisions;
- follow-up ideas/defects/improvements capture;
- cleanup / closure gate;
- `STEP.md` для каждого согласованного step;
- `vacancy.md` для каждого step pack.

Не включать:

- hardcoded Docusaurus assumptions;
- hardcoded GitHub release policy;
- project-specific release branch/version policy;
- production code changes;
- integration verification execution;
- deleting operational artifacts that still contain unpromoted durable knowledge;
- treating release docs as engineering SoT.

## Suggested discussion topics

Перед созданием step packs обсудить с человеком:

- какие release/cleanup steps являются обязательными, а какие project-specific;
- как проверять readiness после Engineering Docs & Knowledge Sync;
- где заканчивается generic Release & Cleanup и начинается project-specific release publication workflow;
- как готовить release docs без hardcoded publishing system assumptions;
- как проверить, что release docs derived from engineering SoT;
- как закрывать task-map;
- когда operational artifacts можно удалить, архивировать, сократить или оставить;
- как фиксировать follow-up ideas, defects and improvements;
- какой cleanup/readiness gate нужен перед closure;
- какие return paths должны быть first-class.

## Expected output

После выполнения задачи должны появиться:

```text
assets/metodologes/waterfall/software-development-methodology/stages/09-release-cleanup/
  workflow.md                         # updated with internal graph and step table
  steps/<step-slug>/STEP.md
  steps/<step-slug>/vacancy.md
```

## Definition of Done

- [ ] План internal steps обсужден с человеком до создания step packs.
- [ ] Согласованный internal workflow graph добавлен в `stages/09-release-cleanup/workflow.md`.
- [ ] Каждый meaningful semantic routing decision modeled as `workflow-step-gate`.
- [ ] Каждый agreed step имеет `steps/<step-slug>/STEP.md`.
- [ ] Каждый step pack имеет `vacancy.md`.
- [ ] Workflow distinguishes engineering SoT from release docs.
- [ ] Workflow includes release docs update/preparation without hardcoding Docusaurus or GitHub policy.
- [ ] Workflow defines when operational artifacts may be archived, shortened, retained or removed.
- [ ] Workflow prevents deletion of artifacts containing unpromoted durable knowledge.
- [ ] Workflow captures follow-up work instead of hiding it in cleanup notes.
- [ ] Links and terminology follow documentation rules.

## Execution Status

- Current State: queued
- Next Step: Обсудить с человеком план internal steps для Release & Cleanup.
- Blockers: none
- Verification: Проверить stage workflow, step packs and vacancies на consistency, progressive disclosure and link correctness.

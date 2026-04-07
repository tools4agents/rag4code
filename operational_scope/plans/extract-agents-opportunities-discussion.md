# Plan: Extract `agents_opportunities` discussion into focused operational artifacts

## Контекст

- Исходный [`discussion artifact`](../../docs/terms/project/terms/discussion-artifact.md): [`agents_opportunities.md`](../discussion/agents_opportunities.md)
- Уже существующий канон слоя: [`overview.md`](../../docs/methodology-layer/overview.md), [`artifact-model.md`](../../docs/methodology-layer/artifact-model.md), [`workflow-and-roles.md`](../../docs/methodology-layer/workflow-and-roles.md), [`interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md), [`asset-taxonomy-and-composition-model.md`](../../docs/methodology-layer/asset-taxonomy-and-composition-model.md)
- Уже существующие related operational artifacts:
  - [`dynamic-step-vacancy-role-binding.md`](../ideas/dynamic-step-vacancy-role-binding.md)
  - [`define-packaging-conventions-for-methodology-artifacts.md`](../plans/define-packaging-conventions-for-methodology-artifacts.md)

## Цель

Разложить ценные идеи из объемного и путаного `discussion artifact` по нескольким focused operational artifacts так, чтобы:
- не потерять полезные гипотезы и архитектурные направления;
- отделить полезные future ideas от шумовых фрагментов разговора;
- не дублировать уже принятый канон [`overview.md`](../../docs/methodology-layer/overview.md) и related methodology-layer docs;
- подготовить исходный discussion file к последующему безопасному удалению после review.

## Что уже считается канонизированным и не требует повторного пересказа

Из discussion не нужно повторно извлекать как отдельную новую идею то, что уже зафиксировано в [`overview.md`](../../docs/methodology-layer/overview.md) и related methodology-layer docs:
- [`agent-role`](../../docs/terms/project/terms/agent-role.md), [`workflow`](../../docs/terms/project/terms/workflow.md), [`workflow-step`](../../docs/terms/project/terms/workflow-step.md), [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md);
- distinction между [`agent-system`-agnostic asset](../../docs/terms/project/terms/agent-system-agnostic-asset.md), [`agent-system`-specific asset](../../docs/terms/project/terms/agent-system-specific-asset.md) и [`agent-system materialization`](../../docs/terms/project/terms/agent-system-materialization.md);
- [`role-pack`](../../docs/terms/project/terms/role-pack.md) и [`composition pack`](../../docs/terms/project/terms/composition-pack.md) как packaging concepts;
- [`primary-agent-system`](../../docs/terms/project/terms/primary-agent-system.md) / `primary_agent_system`;
- file-first SoT и runtime materialization как rebuildable projection.

## Карта извлечения

| Тема из discussion | Целевой artifact | Что сохраняем |
| --- | --- | --- |
| Registry-first marketplace | [`registry-first-marketplace-for-methodology-assets.md`](../ideas/registry-first-marketplace-for-methodology-assets.md) | marketplace как index/registry layer, а не как primary storage |
| Version resolution, lock, snapshot | [`version-resolution-lockfiles-and-runtime-snapshots.md`](../ideas/version-resolution-lockfiles-and-runtime-snapshots.md) | pinned composition, reproducibility, install/update semantics |
| MCP runtime orchestration | [`mcp-driven-workflow-runtime-and-human-orchestration.md`](../ideas/mcp-driven-workflow-runtime-and-human-orchestration.md) | MCP как navigation/control plane для workflow execution |
| Cross-system adaptation | [`cross-agent-system-materialization-and-role-adapters.md`](../ideas/cross-agent-system-materialization-and-role-adapters.md) | adapters, system-specific role assets, materialization policy |
| Moderation and trust | [`registry-moderation-and-trust-model.md`](../ideas/registry-moderation-and-trust-model.md) | staged publication, checks, trust signals |
| Capability-oriented remapping | [`dynamic-step-vacancy-role-binding.md`](../ideas/dynamic-step-vacancy-role-binding.md) | capability layer как future extension над current binding model |
| Packaging implications | [`define-packaging-conventions-for-methodology-artifacts.md`](../plans/define-packaging-conventions-for-methodology-artifacts.md) | skills/resources/templates, publish/install concerns |
| External ecosystem claims | [`external-ecosystem-for-agent-asset-packaging-and-registries.md`](../research/external-ecosystem-for-agent-asset-packaging-and-registries.md) | hypotheses and validation targets, а не канонические утверждения |

## Что нужно выбросить при нормализации

Из discussion не нужно переносить в новые artifacts:
- повторный пересказ уже принятого канона [`overview.md`](../../docs/methodology-layer/overview.md) и related methodology-layer docs;
- шумовые conversational turns без самостоятельной архитектурной ценности;
- неподтвержденные vendor claims как будто это уже установленный факт;
- детали, которые не дают reusable concept или отдельный research question;
- идею `Prompt-as-a-Resource`, так как в текущем подходе системный промпт остается частью `agent-role`.

## Принцип раскладки

Для нормализации используем следующие правила:
- новые reusable architectural directions оформляются как `ideas/` artifacts;
- вопросы publish/install/versioning и migration flow оформляются как `plans/` или packaging-related updates;
- vendor ecosystem assumptions и внешние analogies оформляются как `research/` artifact;
- discussion file остается на месте до review созданных artifacts и пока не удаляется.

## Критерий готовности к удалению исходного discussion file

Исходный [`agents_opportunities.md`](../discussion/agents_opportunities.md) можно удалять только после того, как:
- все целевые artifacts созданы и reviewed;
- каждая ценная идея имеет явный новый home;
- оставшийся текст discussion не содержит уникального reasoning, которого нет в новых artifacts;
- явно подтверждено, что `Prompt-as-a-Resource` и другой discarded material сознательно не переносится.

## Статус

План зафиксирован как operational guide для extraction pass.
Discussion file пока сохраняется как исходный buffer artifact до review созданных файлов.

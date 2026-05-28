# Idea: Cross-agent-system materialization and role adapters

## Контекст

Идея извлечена из [`agents_opportunities.md`](../discussion/agents_opportunities.md) после сопоставления с уже принятыми терминами:
- [`agent-system`](../../docs/terms/project/terms/agent-system.md)
- [`agent-system`-agnostic asset](../../docs/terms/project/terms/agent-system-agnostic-asset.md)
- [`agent-system`-specific asset](../../docs/terms/project/terms/agent-system-specific-asset.md)
- [`agent-system materialization`](../../docs/terms/project/terms/agent-system-materialization.md)

Связанный канон:
- [`artifact-model.md`](../../docs/methodology-layer/artifact-model.md)
- [`interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md)
- [`layered-sot-and-materialization-model.md`](../../docs/methodology-layer/layered-sot-and-materialization-model.md)

## Суть идеи

Нужно сохранить идею, что reusable methodology assets должны по возможности жить в portable, [`agent-system`-agnostic](../../docs/terms/project/terms/agent-system-agnostic-asset.md) форме, а совместимость с конкретными environments обеспечивается через adapters и [`agent-system`-specific assets](../../docs/terms/project/terms/agent-system-specific-asset.md).

Discussion усиливает это направление двумя важными акцентами:
- materialization под разные `agent-system` должна рассматриваться как first-class архитектурная задача;
- adaptation не должна восприниматься как разовый ручной экспорт, а как управляемый pipeline поверх reusable source assets.

## Что именно полезно сохранить

### 1. Adapter thinking как отдельное направление

Полезно мыслить в терминах adapter layer, который отвечает за:
- подбор compatible `agent-system`-specific assets;
- рендеринг runtime-facing artifacts под target environment;
- учет ограничений конкретной `agent-system` без переписывания core semantics.

### 2. Role adaptation не равна role semantics

Даже если одна и та же reusable role materialize в несколько systems:
- semantic owner остается core [`agent-role`](../../docs/terms/project/terms/agent-role.md);
- system-specific variant остается source artifact;
- runtime materialization остается derived output.

### 3. Cross-system portability требует явных boundaries

Чтобы methodology была переносимой, полезно заранее отделять:
- abstract reusable semantics;
- system-specific authored representations;
- final installed runtime files.

Discussion показывает, что без этих границ быстро возникает ложная идея «магического переноса агента между платформами», тогда как на практике нужна explainable adaptation model.

## Предварительная ценность

Такое направление может дать:
- более clean multi-system architecture вместо Kilo-only мышления;
- reuse одной methodology stack в разных developer contexts;
- более ясные границы для adapter-specific authoring;
- основу для будущих adapter packs, projections и compatibility matrices.

## Возможные направления дальнейшей детализации

- adapter capability profile для каждой `agent-system`;
- совместимость `role-pack` и `composition pack` с конкретными systems;
- policy для partial compatibility, fallback и degraded materialization;
- distinction между hand-authored system-specific assets и generated projections;
- tests для cross-system materialization quality.

## Что важно не смешивать

Не стоит смешивать с этой идеей:
- runtime output и reusable source asset;
- change of [`primary-agent-system`](../../docs/terms/project/terms/primary-agent-system.md) и change of role semantics;
- adapter compatibility policy и workflow assignment policy.

## Открытые вопросы

- Нужен ли отдельный reusable artifact family для adapters или достаточно current `agent-system`-specific assets?
- Должен ли `role-pack` включать все system-specific variants или они должны жить отдельно?
- Как описывать partial compatibility для workflow, если один `agent-system` покрывает только часть methodology stack?
- Где фиксировать adapter test expectations: в methodology docs, contracts или отдельном quality layer?

## Статус

Идея зафиксирована как future architecture direction для multi-system support.
Она развивает current materialization model, но не заменяет уже принятый канон terminology и layering.

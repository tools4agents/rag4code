# Idea: Registry-first marketplace for methodology assets

## Контекст

Идея извлечена из [`agents_opportunities.md`](../discussion/agents_opportunities.md) после сопоставления с уже канонизированными моделями:
- [`asset-taxonomy-and-composition-model.md`](../../docs/methodology-layer/asset-taxonomy-and-composition-model.md)
- [`artifact-model.md`](../../docs/methodology-layer/artifact-model.md)
- [`interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md)

В текущем каноне уже есть:
- reusable assets;
- [`role-pack`](../../docs/terms/project/terms/role-pack.md) и [`composition pack`](../../docs/terms/project/terms/composition-pack.md);
- `HyperGraph Asset Catalog SoT`;
- future direction в сторону package management.

Но пока не зафиксирована отдельная idea-level модель marketplace/registry layer.

## Суть идеи

HyperGraph может развиться не просто в файловый catalog, а в `registry-first marketplace` для reusable [`methodology asset`](../../docs/terms/project/terms/methodology-asset.md) и related reusable assets.

Ключевой тезис:
- marketplace не обязан быть primary storage для assets;
- marketplace может выступать как registry/index/discovery layer поверх внешних artifact sources и publishable releases.

## Что именно полезно сохранить

### 1. Marketplace как metadata and discovery layer

Marketplace отвечает за:
- поиск reusable assets;
- публикацию метаданных о packs;
- навигацию по версиям, совместимости и composition options;
- объяснение, что именно будет установлено в проект.

### 2. Storage и registry можно разделить

Полезно разделить:
- registry/index layer;
- physical distribution layer.

Практический вывод:
- asset payload может жить не в самом marketplace;
- registry может индексировать release artifacts, manifests, checksums и compatibility metadata.

### 3. Publishable units должны соответствовать канону assets

Marketplace должен оперировать уже знакомыми сущностями:
- [`role-pack`](../../docs/terms/project/terms/role-pack.md);
- [`composition pack`](../../docs/terms/project/terms/composition-pack.md);
- `skills pack`;
- `rules pack`;
- concrete reusable `methodology asset`.

То есть marketplace не вводит новый semantic layer поверх methodology runtime, а работает с уже существующими asset families.

## Предварительная ценность

Такой marketplace может дать:
- удобный обмен reusable methodology assets между разработчиками;
- discoverability без копирования артефактов вручную;
- воспроизводимые install flows для проектов;
- основу для future package management поверх `HyperGraph Asset Catalog SoT`.

## Базовая модель flow

Предварительно полезен следующий flow:
1. publisher подготавливает publishable asset или pack;
2. asset получает versioned release artifact и metadata;
3. registry индексирует release, совместимость, checksums и trust metadata;
4. project выбирает asset через portable references;
5. resolver строит resolved composition;
6. runtime materialization раскладывает environment-facing artifacts под выбранную [`primary-agent-system`](../../docs/terms/project/terms/primary-agent-system.md).

## Что важно не смешивать

С этой идеей не стоит смешивать:
- runtime materialization;
- storage path до central catalog;
- human-facing marketplace UI и canonical SoT;
- process semantics [`workflow`](../../docs/terms/project/terms/workflow.md) / [`step-vacancy`](../../docs/terms/project/terms/step-vacancy.md) / [`agent-role`](../../docs/terms/project/terms/agent-role.md).

Marketplace относится к distribution and discovery layer, а не к semantic owner layer.

## Возможные направления дальнейшей проработки

- package identity model для packs и reusable assets;
- publish metadata schema;
- compatibility model между `composition pack`, `role-pack`, `skills pack` и supported `agent-system`;
- install/update workflow;
- search and discovery UX;
- связь registry metadata с trust and moderation pipeline.

## Открытые вопросы

- Должен ли registry индексировать только publishable packs или также одиночные reusable assets?
- Нужен ли отдельный artifact type для publish manifest?
- Насколько registry должен знать про `primary-agent-system`, а насколько это concern resolver layer?
- Должен ли один registry entry указывать на несколько distribution backends?

## Статус

Идея полезна как отдельное направление для дальнейшей спецификации package ecosystem.
Она не заменяет текущий file-first catalog baseline и пока не считается канонической реализацией.

# Idea: Registry moderation and trust model for methodology assets

## Контекст

Идея извлечена из [`agents_opportunities.md`](../discussion/agents_opportunities.md) как продолжение направления про publishable packs и future marketplace layer.

Связанные канонические документы пока задают reusable assets и composition model, но не описывают publication governance:
- [`asset-taxonomy-and-composition-model.md`](../../docs/methodology-layer/asset-taxonomy-and-composition-model.md)
- [`artifact-model.md`](../../docs/methodology-layer/artifact-model.md)

## Суть идеи

Если HyperGraph будет поддерживать публикацию reusable [`methodology asset`](../../docs/terms/project/terms/methodology-asset.md) и related packs, понадобится отдельная trust and moderation model.

Ключевой тезис:
- publish/install ecosystem требует не только package identity и versioning;
- также нужен понятный lifecycle trust, review и publication status.

## Что именно полезно сохранить

### 1. Publication status lifecycle

Полезно заранее обсуждать lifecycle состояний вроде:
- `pending`;
- `staged`;
- `published`;
- возможно, `deprecated` или `revoked`.

Эти статусы относятся не к semantic quality methodology, а к publication governance and trust workflow.

### 2. Automated checks before publication

Перед публикацией reusable asset или pack полезны automated checks:
- manifest validation;
- structure linting;
- checksum generation;
- dry-run install;
- compatibility checks против supported `agent-system` или required asset types.

### 3. Trust signals for consumers

Registry может показывать trust metadata:
- verified publisher;
- validation status;
- supported systems;
- last successful install check;
- deprecation notice.

Это снижает риск слепого подключения неподготовленных packs.

## Предварительная ценность

Такая модель может дать:
- более безопасный open ecosystem вокруг reusable methodology assets;
- меньше случайных broken installs;
- понятные signals для выбора packs в marketplace;
- основу для public and private publication workflows.

## Что важно не смешивать

Не нужно смешивать moderation/trust model с:
- semantic каноном methodology docs;
- runtime materialization semantics;
- process model `workflow` and roles;
- developer-local experimentation, которое не обязано проходить publication pipeline.

## Возможные направления дальнейшей проработки

- publication policy для public и private registries;
- роль automated review vs human moderation;
- критерии verified publisher;
- revocation flow при broken or unsafe release;
- trust signals для `composition pack` по сравнению с отдельными packs.

## Открытые вопросы

- Нужна ли человеку-модератору отдельная role model внутри methodology ecosystem?
- Должен ли publish lifecycle быть единым для всех asset families?
- Как показывать trust для pack, который включает third-party dependencies?
- Нужно ли различать validation status и publication status?

## Статус

Идея зафиксирована как отдельное направление для будущего registry governance.
Пока это operational exploration, а не каноническая часть `Project Methodology Runtime`.

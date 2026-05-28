# Idea: Version resolution, lockfiles, and runtime snapshots for methodology assets

## Контекст

Идея извлечена из [`agents_opportunities.md`](../discussion/agents_opportunities.md) как развитие уже существующих слоев:
- [`layered-sot-and-materialization-model.md`](../../docs/methodology-layer/layered-sot-and-materialization-model.md)
- [`interfaces-and-storage.md`](../../docs/methodology-layer/interfaces-and-storage.md)
- [`asset-taxonomy-and-composition-model.md`](../../docs/methodology-layer/asset-taxonomy-and-composition-model.md)

В текущем каноне уже различаются:
- canonical source layers;
- resolved states;
- runtime materialization states.

Но пока не формализованы package-level semantics для version resolution, lock и reproducible install/update.

## Суть идеи

Для reusable methodology assets может понадобиться явная модель из трех уровней:
- published versions assets;
- resolved project composition;
- runtime snapshot materialized environment.

Это нужно, чтобы отличать:
- что опубликовано в registry;
- что именно выбрал проект;
- что реально materialized в текущем developer context.

## Что именно полезно сохранить

### 1. Version reference недостаточен без resolved selection

Даже если проект хранит `version_ref`, этого мало для воспроизводимости composition.

Может потребоваться зафиксировать:
- точные versions выбранных packs;
- конкретные artifact identities внутри composition;
- selected `agent-system`-specific assets;
- content hashes или equivalent integrity fields.

### 2. Lock layer полезен отдельно от portable intent

Полезно различать:
- project intent уровня «что мы хотим использовать»;
- lock layer уровня «во что это конкретно зарезолвилось».

Такой слой может быть ближе к `Service-project Resolved State`, но discussion поднимает вопрос, не нужен ли еще и project-visible portable lock artifact.

### 3. Runtime snapshot не равен lock

Даже при стабильном resolved composition полезно отдельно понимать:
- какой runtime materialized;
- для какой [`primary-agent-system`](../../docs/terms/project/terms/primary-agent-system.md);
- из каких exact sources и projections он собран;
- можно ли объяснить drift между lock-like state и текущим runtime.

## Предварительная ценность

Такая модель может дать:
- воспроизводимые installs methodology stack;
- explainable updates;
- безопасное сравнение resolved compositions между версиями;
- более четкий drift detection между desired state и runtime materialization;
- основу для rollback и audit.

## Возможный набор артефактов

Предварительно можно обсуждать такие artifacts:
- publish manifest для конкретной released version;
- project-level lock artifact для выбранной composition;
- runtime snapshot artifact или diagnostics snapshot для materialized environment.

Это пока не proposal на окончательный layout, а фиксация полезной architectural direction.

## Связь с текущим каноном

Идея должна развиваться без нарушения текущих инвариантов:
- canonical SoT остается file-first;
- runtime snapshot не становится semantic owner layer;
- project не должен хранить machine-specific internal paths;
- `primary_agent_system` остается selector для active runtime target, а не заменой version model.

## Открытые вопросы

- Нужен ли portable project-owned lock artifact или достаточно service-level resolved state?
- Должен ли lock фиксировать content hashes каждого selected artifact?
- Нужен ли отдельный snapshot для global runtime и project runtime?
- Как сочетать human-editable project intent и machine-produced lock без конфликтов?
- Что считать unit of update: отдельный pack, composition, role asset или целую methodology stack?

## Статус

Идея зафиксирована как важное направление для дальнейшей package-resolution спецификации.
Она дополняет current layered model, но пока не включена в канон как формальный contract.

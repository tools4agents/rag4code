# Terms Map

> Status: Draft  
> Scope: concrete `terms-management-system asset` под названием `terms-map`  
> Role: Source of Truth для scoped terminology maps, term navigation и progressive disclosure

## Назначение

Этот документ фиксирует первый concrete [`terms-management-system asset`](../../../terms/project/terms/terms-management-system-asset.md): `terms-map`.

Он задает минимальную систему хранения и раскрытия терминов через scoped `terms_map.md` files и optional detail pages.

## Что задает `terms-map`

`Terms-map` отвечает на вопросы:

- где живут terminology entry points;
- как организован scoped glossary;
- как устроен lazy loading терминов;
- как документация ссылается на терминологию вместо повторного пересказа определений.

## Baseline layout pattern

Для первой итерации `terms-map` использует такой обобщенный baseline pattern:

```text
docs/terms/<scope>/terms_map.md
```

Где `<scope>`:

- не фиксирован жестко;
- может отражать логическую группировку терминов;
- может быть устроен по-разному в разных проектах и compositions.

## Scoped terminology maps

`Terms-map` предполагает, что терминология раскрывается через scoped maps.

Типичные варианты scope:

- `common`
- `project`
- другие scope groups, если проекту так удобнее

Главный invariant:

- терминологическая система должна поддерживать несколько `terms_map.md`, а не требовать один глобальный файл на все случаи.

## Optional detail pages

Помимо `terms_map.md`, система может использовать detail pages.

Обобщенный pattern такой:

```text
docs/terms/<scope>/terms/*.md
```

Но detail pages являются supporting layer, а не обязательной заменой scoped `terms_map.md`.

## Как работает navigation

`Terms-map` строится вокруг progressive disclosure:

1. сначала читается краткое определение в `terms_map.md`;
2. затем при необходимости открывается detail page;
3. после этого читатель или агент возвращается в исходный архитектурный, методологический или operational документ.

## Связь с документацией

Если проект использует `terms-map`:

- docs должны ссылаться на термины, а не пересказывать определения в каждом документе;
- scoped `terms_map.md` должны быть canonical entry points в своей области;
- detail pages должны использоваться для нагруженных или часто переиспользуемых терминов.

## Связь с knowledge lifecycle

`Terms-map` не задает lifecycle знания в проекте.

Он задает только систему хранения и навигации по терминологии.

Knowledge movement между operational, engineering и release слоями принадлежит [`knowledge-lifecycle asset`](../../../terms/project/terms/knowledge-lifecycle-asset.md).

## Связь с task management

`Terms-map` не задает task storage.

Но [`task artifacts`](../../../terms/project/terms/task-artifact.md), plans и другие artifacts могут использовать `terms-map` как terminology baseline.

## Что этот документ не делает

Этот документ не описывает:

- process semantics конкретной methodology;
- task index и task storage layout;
- release publishing pipeline;
- полный artifact taxonomy проекта.

## Связь с другими документами

Этот документ нужно читать вместе с:

- [`Asset Taxonomy and Composition Model for Project Methodology Runtime`](../../asset-taxonomy-and-composition-model.md);
- [`Documentation Lifecycle Layers`](../knowledge-lifecycle/documentation-lifecycle-layers.md);
- [`Task Map`](../task-management/task-map.md);
- [`Project Methodology Runtime Overview`](../../overview.md).

## Canonical invariants

- `terms-map` является concrete `terms-management-system asset`.
- scoped `docs/terms/<scope>/terms_map.md` являются canonical terminology entry points.
- структура scope groups может различаться между проектами.
- detail pages являются optional supporting layer поверх scoped `terms_map.md`.
- docs и operational artifacts должны использовать glossary-first linking, а не дублировать определения терминов.

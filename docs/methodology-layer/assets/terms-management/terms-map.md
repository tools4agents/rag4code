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

Для первой итерации `terms-map` использует такой baseline pattern:

```text
docs/terms/
  index.md
  <scope>/
    terms-map.md
    terms/
      <term>.md
```

Где:

- `docs/terms/index.md` — карта всех `scope` groups и links на все scoped `terms-map.md` внутри проекта;
- `docs/terms/<scope>/terms-map.md` — краткая карта терминов для конкретного `scope`;
- `docs/terms/<scope>/terms/<term>.md` — detail page для индивидуального термина внутри `scope`.

Где `<scope>`:

- не фиксирован жестко;
- может отражать логическую группировку терминов;
- может быть устроен по-разному в разных проектах и compositions;
- должен допускать перенос между проектами как reusable terminology package.

Для единообразного bootstrap нового `terms-map.md` можно использовать шаблон:

- [`terms-map.template.md`](./resources/terms-map.template.md)

Для единообразного bootstrap root `docs/terms/index.md` можно использовать шаблон:

- [`terms-index.template.md`](./resources/terms-index.template.md)

## Scoped terminology maps

`Terms-map` предполагает, что терминология раскрывается через scoped maps, а root `docs/terms/index.md` играет роль entry point для всех scope groups проекта.

Типичные варианты scope:

- `common`
- `project`
- другие scope groups, если проекту так удобнее

Главные invariants:

- терминологическая система должна поддерживать несколько scoped `terms-map.md`, а не требовать один глобальный файл на все случаи;
- root `docs/terms/index.md` должен перечислять доступные scope groups и вести в их `terms-map.md`;
- scope groups должны быть устроены так, чтобы их можно было переносить между проектами как отдельные terminology packages.

## Optional detail pages

Помимо `terms-map.md`, система может использовать detail pages.

Обобщенный pattern такой:

```text
docs/terms/<scope>/terms/*.md
```

Но detail pages являются supporting layer, а не обязательной заменой scoped `terms-map.md`.

## Как работает navigation

`Terms-map` строится вокруг progressive disclosure:

1. сначала читается `docs/terms/index.md` как карта scopes;
2. затем открывается нужный scoped `terms-map.md`;
3. затем при необходимости открывается detail page термина;
4. после этого читатель или агент возвращается в исходный архитектурный, методологический или operational документ.

## Связь с документацией

Если проект использует `terms-map`:

- docs должны ссылаться на термины, а не пересказывать определения в каждом документе;
- `docs/terms/index.md` должен быть общим terminology entry point;
- scoped `terms-map.md` должны быть canonical entry points в своей области;
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

- [`asset-taxonomy-and-composition-model.md`](../../asset-taxonomy-and-composition-model.md);
- [`documentation-lifecycle-layers.md`](../knowledge-lifecycle/documentation-lifecycle-layers.md);
- [`task-map.md`](../task-management/task-map.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- `terms-map` является concrete `terms-management-system asset`.
- `docs/terms/index.md` является root terminology entry point проекта.
- scoped `docs/terms/<scope>/terms-map.md` являются canonical terminology entry points внутри своих scopes.
- структура scope groups может различаться между проектами.
- scope groups должны допускать перенос между проектами как reusable terminology packages.
- detail pages являются optional supporting layer поверх scoped `terms-map.md`.
- docs и operational artifacts должны использовать glossary-first linking, а не дублировать определения терминов.

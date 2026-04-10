# Research Tree

> Status: Draft  
> Scope: concrete [`research-management-system asset`](../../../terms/project/terms/research-management-system-asset.md) под названием `research-tree`  
> Role: Source of Truth для baseline research index, tree-shaped storage и continuation-friendly navigation model

## Назначение

Этот документ фиксирует первый concrete [`research-management-system asset`](../../../terms/project/terms/research-management-system-asset.md): `research-tree`.

Он задает file-first систему хранения и навигации для многоитерационных исследований, где один research topic раскладывается на ветки, ветки ведутся через bounded iterations, а distilled knowledge поднимается в отдельный knowledge layer.

## Что задает `research-tree`

`Research-tree` отвечает на вопросы:
- где живет research index;
- где живут topic roots и branch pages;
- где хранится topic-level focus memory;
- где живет distilled knowledge layer;
- как research topic раскладывается на branch-level dossiers;
- где хранится iteration history;
- как research artifacts поддерживают handoff и continuation;
- какой layout считается baseline для tree-shaped research storage.

## Baseline layout

Для первой итерации `research-tree` использует такой baseline layout:

```text
operational_scope/
  research-tree.md
  research/
    <topic-slug>/
      index.md
      research-map.md
      knowledge/
        index.md
      <branch-slug>/
        index.md
        iterations/
          iteration-01.md
```

## Роли элементов layout

- `operational_scope/research-tree.md` - канонический индекс research layer.
- `operational_scope/research/<topic-slug>/index.md` - canonical topic root dossier.
- `operational_scope/research/<topic-slug>/research-map.md` - topic-level working memory и handoff surface.
- `operational_scope/research/<topic-slug>/knowledge/` - topic-level distilled knowledge layer.
- `operational_scope/research/<topic-slug>/<branch-slug>/index.md` - canonical branch dossier.
- `operational_scope/research/<topic-slug>/<branch-slug>/iterations/` - storage location для bounded research iterations внутри ветки.

## Что считается research index

Для `research-tree` каноническим индексом research layer считается `operational_scope/research-tree.md`.

Этот файл должен давать краткую карту активных research topics:
- topic name;
- topic identifier;
- status;
- priority;
- root question или decision context;
- link на topic root dossier.

Индекс нужен для navigation, portfolio overview и focus management, а не для полного пересказа branch-level findings.

## Topic root и branch pages

`Research-tree` не хранит детальную структуру каждого topic root или branch page.

Эта ответственность принадлежит supporting document [`research-branches.md`](research-branches.md).

Важные invariants:
- topic root является canonical documentation entry для одного research topic;
- branch page является canonical documentation entry для одной ветки исследования;
- iteration files фиксируют wave-by-wave progress, но не заменяют topic root и branch page как navigation roots.

## Focus memory и knowledge layer

`Research-tree` различает два topic-level memory layers:

- `research-map.md` - working memory для current focus, counters, portfolio review triggers и next action;
- `knowledge/` - semantic memory layer для distilled notes, branch knowledge pages и synthesis.

Эта ответственность подробнее раскрывается в supporting document [`research-knowledge.md`](research-knowledge.md).

## Связь с traceability conventions

`Research-tree` не задает подробно identifier grammar, metadata keys и целевую traceability chain.

Эта ответственность принадлежит supporting document [`research-traceability.md`](research-traceability.md).

## Связь с knowledge lifecycle

`Research-tree` не задает lifecycle знания в проекте.

Он предполагает, что проект использует какой-то [`knowledge-lifecycle asset`](../../../terms/project/terms/knowledge-lifecycle-asset.md), например `document-driven-development`.

Следствие:
- research artifacts относятся к [`Operational Documentation Layer`](../../../terms/project/terms/operational-documentation-layer.md), а не к engineering SoT;
- findings, hypotheses и synthesis внутри `research-tree` не подменяют собой `docs/` как канонический engineering layer;
- если исследование приводит к устойчивому technical decision, результат должен быть отдельно канонизирован в engineering documentation.

## Связь с task management

`Research-tree` не задает task storage и task index.

Он может ссылаться на [`task artifacts`](../../../terms/project/terms/task-artifact.md), но не подменяет [`task-management-system asset`](../../../terms/project/terms/task-management-system-asset.md).

## Связь с terms management

`Research-tree` не задает glossary system.

Если в проекте есть [`terms-management-system asset`](../../../terms/project/terms/terms-management-system-asset.md), topic и branch pages должны использовать его terminology baseline, а не дублировать термины без необходимости.

## Связь с derived graph

Этот asset проектируется как file-first SoT для будущей graph-backed traceability и navigation.

Следствие:
- markdown остается каноническим источником структуры дерева, identifiers и links;
- branch cross-links и iteration metadata являются supporting anchors для будущего graph projection;
- graph database позже может строиться как derived representation по markdown artifacts, а не заменять их как source layer.

## Что этот документ не делает

Этот документ не описывает:
- точную структуру topic root и branch pages;
- branch scoring model и portfolio review semantics в деталях;
- identifier grammar и grep-friendly metadata placement;
- исследовательский workflow конкретного skill или agent-role.

## Связь с другими документами

Этот документ нужно читать вместе с:
- [`asset-taxonomy-and-composition-model.md`](../../asset-taxonomy-and-composition-model.md);
- [`documentation-lifecycle-layers.md`](../knowledge-lifecycle/documentation-lifecycle-layers.md);
- [`research-branches.md`](research-branches.md);
- [`research-knowledge.md`](research-knowledge.md);
- [`research-traceability.md`](research-traceability.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- `research-tree` является concrete [`research-management-system asset`](../../../terms/project/terms/research-management-system-asset.md).
- `operational_scope/research-tree.md` является каноническим research index для этой системы.
- `operational_scope/research/` является baseline storage location для tree-shaped [`research artifacts`](../../../terms/project/terms/research-artifact.md).
- `research-map.md` является working memory и handoff surface темы, а не long-form knowledge archive.
- `knowledge/` является distilled semantic memory layer поверх history layer.
- topic root и branch page являются разными navigation levels и не должны сливаться в один монолитный файл.
- iteration files являются bounded progress artifacts внутри branch scope.
- markdown остается canonical Source of Truth для research structure, navigation и continuation metadata.

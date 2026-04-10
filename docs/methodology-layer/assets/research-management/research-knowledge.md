# Research Knowledge

> Status: Draft  
> Scope: supporting specification для concrete [`research-management-system asset`](../../../terms/project/terms/research-management-system-asset.md) `research-tree`  
> Role: Source of Truth для layered research memory, knowledge distillation и map-of-content navigation поверх history layer

## Назначение

Этот документ задает knowledge layer для `research-tree`.

Его задача - описать:
- как отделяются history, focus memory и semantic knowledge memory;
- как raw research iterations перерабатываются в связанное knowledge space;
- как knowledge layer поддерживает `lazy loading` и `progressive disclosure`;
- как агент и человек читают distilled knowledge без обязательного перечитывания всей истории.

## Почему нужен отдельный knowledge layer

В больших исследованиях одного summary-файла недостаточно.

Если вся distilled knowledge сводится в один `knowledge-map.md`, он быстро превращается в перегруженный монолит и теряет свойства удобной navigation surface.

Поэтому `research-tree` использует не один knowledge file, а отдельный knowledge layer, который:
- повторяет структуру исследования в более дистиллированном виде;
- хранит не ход работы, а knowledge notes и synthesis pages;
- дает человеку и агенту map-of-content navigation вместо перечитывания полного history layer.

## Memory classes inside `research-tree`

Для первой итерации рекомендуется различать четыре memory classes:

1. `Topic dossier`
   - файл: `<topic>/index.md`
   - роль: стабильный canonical dossier темы.

2. `Working memory`
   - файл: `<topic>/research-map.md`
   - роль: оперативная память фокуса, branch priorities, counters и handoff triggers.

3. `Semantic knowledge memory`
   - каталог: `<topic>/knowledge/`
   - роль: distilled knowledge notes, branch-level maps и synthesis pages.

4. `History memory`
   - каталог: `<topic>/<branch>/iterations/`
   - роль: append-only episodic history поисковых проходов.

Главный invariant:
- `research-map.md` хранит focus state, а не substantive knowledge body;
- важное знание не должно оставаться только в `iterations/`, если оно нужно для дальнейшей работы.

## Baseline layout for knowledge layer

Для первой итерации рекомендуется такой baseline layout:

```text
operational_scope/
  research/
    <topic-slug>/
      index.md
      research-map.md
      knowledge/
        index.md
        branches/
          <branch-slug>.md
        findings/
          RF-<...>.md
        questions/
          RQ-<...>.md
        syntheses/
          current-synthesis.md
```

Optional supporting families:
- `knowledge/comparisons/`
- `knowledge/decisions/`
- `knowledge/dead-ends/`

## Roles of knowledge files

- `knowledge/index.md`
  - topic-level `Map of Content`;
  - главный navigation entry в distilled knowledge темы.

- `knowledge/branches/<branch-slug>.md`
  - branch-level knowledge page;
  - короткая карта того, что ветка дала и куда по ней углубляться.

- `knowledge/findings/RF-<...>.md`
  - атомарная knowledge card для одного важного finding.

- `knowledge/questions/RQ-<...>.md`
  - first-class note для открытого или частично закрытого research question.

- `knowledge/syntheses/current-synthesis.md`
  - текущая topic-level synthesis page;
  - связывает findings и branch outcomes обратно с decision context.

## Why `knowledge/index.md` is a Map of Content

`Knowledge/index.md` не должен быть длинным narrative summary.

Его роль ближе к `Map of Content`:
- кратко показать, какие knowledge pages существуют;
- сгруппировать их по branches или subtopics;
- указать, какие notes читать first;
- поддерживать переход от общего к частному.

Это делает knowledge layer совместимым с принципом `lazy loading`:
- сначала карта знаний;
- затем branch knowledge page;
- затем atomized notes;
- и только потом raw iterations, если они реально нужны.

## Atomic knowledge notes

Для первой итерации рекомендуется считать baseline atom types:
- `Finding notes`
- `Question notes`

Optional derived note types:
- `Comparison notes`
- `Decision notes`
- `Dead-end notes`
- дополнительные synthesis pages

### Recommended minimal structure for finding note

- `Finding ID`
- `Claim`
- `Related branch`
- `Related questions`
- `Evidence basis`
- `Confidence`
- `Why it matters`
- `Related findings`
- `Derived from iterations`

### Recommended minimal structure for question note

- `Research question`
- `Current status`
- `What is already known`
- `What is still unresolved`
- `Related branches`
- `Related findings`
- `Next useful evidence`

## Distillation loop

Knowledge layer должен пополняться не напрямую из broad search, а через краткий distillation loop:

`capture -> distill -> verify -> link -> surface`

Где:
- `capture` - findings и raw observations фиксируются в iteration history;
- `distill` - из history выделяются reusable knowledge notes;
- `verify` - note проходит локальные checks перед включением в memory layer;
- `link` - note получает cross-links на branches, questions и related findings;
- `surface` - knowledge note поднимается в `knowledge/index.md`, branch knowledge page или synthesis page.

## Verification checks for knowledge notes

Перед включением important note в semantic memory рекомендуется пройти четыре baseline checks:

1. `Evidence check`
   - есть ли достаточно понятная evidence basis.

2. `Conflict check`
   - не противоречит ли note уже существующим findings или synthesis.

3. `Explainability check`
   - можно ли кратко и непротиворечиво объяснить note в 2-4 предложениях.

4. `Link completeness check`
   - привязана ли note к branch, question, related findings и relevant iterations.

Для synthesis pages дополнительно рекомендуется:
- `Coverage check`
- `Decision usefulness check`

## Working memory is not knowledge memory

`<topic>/research-map.md` не должен дублировать knowledge layer.

Это файл оперативной памяти, в котором рекомендуется хранить:
- current focus;
- active branches now;
- branch priority snapshot;
- `Deep iterations since last portfolio review`;
- `Portfolio review required`;
- `Recommended next action`;
- `Read-first links`.

`Research-map.md` можно перезаписывать. Его задача - передавать следующему агенту фокус, а не хранить накопленное знание темы.

## Hot path and cold path

Для чтения темы рекомендуется различать hot path и cold path.

### Hot path

Новый исследователь по теме должен по умолчанию идти так:
1. `operational_scope/research-tree.md`
2. `<topic>/research-map.md`
3. `<topic>/knowledge/index.md`
4. relevant `knowledge/branches/<branch>.md`
5. relevant finding or question notes

### Cold path

`iterations/*.md` остаются cold path и читаются только если нужно:
- перепроверить evidence;
- восстановить reasoning history;
- разрешить конфликт между distilled notes;
- понять, откуда появился спорный вывод.

## Compression invariant

Если finding, caveat, rejected hypothesis или cross-branch insight все еще важны для дальнейшей работы, они не должны оставаться только в raw history.

Они должны быть подняты в один или несколько слоев:
- в branch knowledge page;
- в finding/question note;
- в topic-level synthesis page.

Иначе новый агент будет вынужден каждый раз перечитывать историю, что нарушает `lazy loading` и перегружает context window.

## Relation to human-oriented note systems

Этот knowledge layer intentionally ближе к:
- `Map of Content`;
- atomized Zettelkasten-style notes;
- linked knowledge pages;

чем к одному большому summary или plain archive of notes.

Но `research-tree` использует эту идею в project-oriented форме:
- IDs и traceability обязательны;
- focus memory отделена от semantic memory;
- raw iterations не заменяются knowledge notes, а остаются history layer.

## Что этот документ не делает

Этот документ не задает:
- identifier grammar для research tree;
- branch scoring policy;
- конкретный search workflow исследователя;
- правила канонизации research knowledge в engineering SoT.

Эти вопросы принадлежат другим documents внутри `research-management`.

## Связь с другими документами

Этот документ нужно читать вместе с:
- [`research-tree.md`](research-tree.md);
- [`research-branches.md`](research-branches.md);
- [`research-traceability.md`](research-traceability.md);
- [`principles.md`](../../principles.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- knowledge layer является отдельным memory layer поверх history, а не заменой `iterations/`.
- `research-map.md` является working memory и не должен разрастаться в knowledge archive.
- `knowledge/index.md` является map-of-content для distilled knowledge темы.
- important knowledge не должно оставаться только в raw iterations, если оно нужно для продолжения исследования.
- distilled notes должны поддерживать cross-links и progressive disclosure.

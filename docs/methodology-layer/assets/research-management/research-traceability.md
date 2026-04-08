# Research Traceability

> Status: Draft  
> Scope: supporting specification для concrete [`research-management-system asset`](../../../terms/project/terms/research-management-system-asset.md) `research-tree`  
> Role: Source of Truth для identifier conventions, traceability chain и grep-friendly metadata placement внутри research tree

## Назначение

Этот документ задает traceability conventions для tree-shaped research documentation.

Его задача - описать:
- целевую traceability chain;
- baseline identifier families;
- fixed metadata keys для topic, branch и iteration pages;
- conventions, удобные для grep, regex и agent navigation.

## Целевая traceability chain

Для `research-tree` целевой считается chain:

`white spot / open question / research brief -> research topic -> research branch -> research iteration -> evidence source -> research finding -> current synthesis`

В этой цепочке:
- upstream driver задает, почему исследование вообще было открыто;
- topic root задает общий decision context;
- branch page задает scoped направление исследования;
- iteration file фиксирует bounded волну поиска;
- evidence source дает внешний или внутренний anchor;
- research finding фиксирует локальный вывод;
- current synthesis связывает findings обратно с вопросом topic-level.

## Identifier families

Для первой итерации фиксируются пять baseline families:
- `RT-<AREA>-<TOPIC>` для topic identifiers;
- `RB-<AREA>-<TOPIC>-<BRANCH>` для branch identifiers;
- `RI-<AREA>-<TOPIC>-<BRANCH>-<NNN>` для iteration identifiers;
- `RQ-<AREA>-<TOPIC>-<NNN>` для research question identifiers;
- `RF-<AREA>-<TOPIC>-<NNN>` для finding identifiers.

Примеры:
- `RT-PROVIDERS-MODEL-SELECTION`
- `RB-PROVIDERS-MODEL-SELECTION-OFFICIAL-DOCS`
- `RI-PROVIDERS-MODEL-SELECTION-OFFICIAL-DOCS-001`
- `RQ-PROVIDERS-MODEL-SELECTION-002`
- `RF-PROVIDERS-MODEL-SELECTION-004`

Главные требования к identifier:
- стабильность;
- уникальность в пределах проекта;
- отсутствие пробелов;
- grep-friendly and regex-friendly shape.

## Почему prefixes обязательны

Entity prefixes фиксируются явно:
- `RT-`
- `RB-`
- `RI-`
- `RQ-`
- `RF-`

Это нужно, чтобы:
- не путать topic ids, branch ids, findings и вопросы;
- сделать поиск точнее;
- упростить автоматическую валидацию;
- облегчить будущую graph-backed traceability.

## Markdown metadata keys

Для markdown-level metadata фиксируются human-readable fixed keys:
- `Topic ID:`
- `Branch ID:`
- `Iteration ID:`
- `Research question:`
- `Finding ID:`
- `Upstream driver:`
- `Related branch:`

Примеры:

```text
Topic ID: RT-PROVIDERS-MODEL-SELECTION
Branch ID: RB-PROVIDERS-MODEL-SELECTION-OFFICIAL-DOCS
Iteration ID: RI-PROVIDERS-MODEL-SELECTION-OFFICIAL-DOCS-001
Research question: RQ-PROVIDERS-MODEL-SELECTION-002
Finding ID: RF-PROVIDERS-MODEL-SELECTION-004
Upstream driver: white-spot: provider capability mismatch
Related branch: RB-PROVIDERS-MODEL-SELECTION-REAL-WORLD-REPORTS
```

Именно эти fixed keys считаются baseline convention для grep, regex и agent navigation.

## Placement rules

### Topic level

Topic metadata рекомендуется ставить в начале topic root dossier.

Минимально рекомендуется фиксировать:
- `Topic ID:`
- один или несколько `Upstream driver:`
- один или несколько `Research question:`

### Branch level

Branch metadata рекомендуется ставить в начале branch page.

Минимально рекомендуется фиксировать:
- `Branch ID:`
- related `Research question:`
- optional `Related branch:` lines, если ветка явно пересекается с другими.

### Iteration level

Iteration metadata рекомендуется ставить в начале iteration file.

Минимально рекомендуется фиксировать:
- `Iteration ID:`
- parent `Branch ID:`
- relevant `Research question:`

### Finding level

Finding identifier рекомендуется фиксировать в заголовке finding или первой metadata line внутри finding block.

Пример:

```text
### Finding RF-PROVIDERS-MODEL-SELECTION-004: Official docs confirm feature gap
```

или

```text
Finding ID: RF-PROVIDERS-MODEL-SELECTION-004
```

## Search and grep policy

Conventions проектируются так, чтобы агент или человек мог быстро сузить scope поиска.

Практически это означает:
- navigation начинается с `operational_scope/research-tree.md`;
- затем search сужается до `topic/index.md`;
- потом до `branch/index.md` и только затем до `iterations/`;
- поиск по `RT-`, `RB-`, `RI-`, `RQ-` и `RF-` identifiers должен быть тривиальным через grep или regex;
- broad web search должен по возможности опираться на `Search anchors`, зафиксированные в branch page.

## Recommended regex baseline

Для первой итерации достаточно такой baseline grammar:

```regex
^Topic ID:\s+(RT-[A-Z0-9-]+)$
^Branch ID:\s+(RB-[A-Z0-9-]+)$
^Iteration ID:\s+(RI-[A-Z0-9-]+)$
^Research question:\s+(RQ-[A-Z0-9-]+)$
^Finding ID:\s+(RF-[A-Z0-9-]+)$
^Upstream driver:\s+(.+)$
^Related branch:\s+(RB-[A-Z0-9-]+)$
```

## Что этот документ не делает

Этот документ не задает:
- детальный branch scoring model;
- skill-level search workflow;
- storage layout вне `research-tree`;
- правила канонизации findings в engineering SoT.

## Связь с другими документами

Этот документ нужно читать вместе с:
- [`research-tree.md`](research-tree.md);
- [`research-branches.md`](research-branches.md);
- [`testing-system/test-case-traceability.md`](../testing-system/test-case-traceability.md);
- [`Engineering Documentation SoT`](../../../terms/project/terms/engineering-documentation-sot.md).

## Canonical invariants

- target traceability chain для `research-tree` - `white spot / open question / research brief -> research topic -> research branch -> research iteration -> evidence source -> research finding -> current synthesis`.
- `RT-`, `RB-`, `RI-`, `RQ-` и `RF-` являются baseline identifier families.
- `Topic ID:`, `Branch ID:`, `Iteration ID:`, `Research question:`, `Finding ID:`, `Upstream driver:` и `Related branch:` являются baseline markdown metadata keys.
- topic, branch и iteration metadata должны быть grep-friendly и machine-readable без отказа от human-readable markdown.
- markdown-level traceability metadata дополняет narrative text, а не заменяет его.

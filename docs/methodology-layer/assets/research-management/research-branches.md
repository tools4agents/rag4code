# Research Branches

> Status: Draft  
> Scope: supporting specification для concrete [`research-management-system asset`](../../../terms/project/terms/research-management-system-asset.md) `research-tree`  
> Role: Source of Truth для структуры topic roots, branch pages и branch-level portfolio navigation

## Назначение

Этот документ задает baseline structure для topic roots и branch pages внутри `research-tree`.

Его задача - описать:
- какую роль играет topic root dossier;
- какую роль играет branch dossier;
- какие sections рекомендуется иметь на каждом уровне;
- как фиксируются branch boundaries, search anchors и cross-branch links;
- как поддерживается portfolio-level navigation между ветками.

## Роль topic root dossier

Topic root - это canonical documentation entry для одного research topic.

Он нужен, чтобы:
- кратко описать цель исследования и decision context;
- связать topic с upstream `white spots`, `open questions` или research brief;
- показать карту веток исследования;
- вести branch portfolio и current synthesis;
- оставлять handoff для следующей волны исследования.

## Recommended topic root sections

Для первой итерации topic root рекомендуется делать со следующими sections:

1. `Topic ID`
2. `Goal / Decision context`
3. `Upstream drivers`
4. `Research map`
5. `Branch registry`
6. `Branch status board`
7. `Cross-branch dependencies`
8. `Current best synthesis`
9. `Open questions`
10. `Next iteration plan`
11. optional `Related artifacts`

## Роль branch dossier

Branch page - это canonical documentation entry для одной ветки исследования.

Она нужна, чтобы:
- сформулировать branch question или branch hypothesis;
- зафиксировать scope ветки;
- показать, почему ветка важна;
- указать, где искать внутренний контекст и внешние evidence sources;
- кратко зафиксировать ключевые findings ветки;
- связать ветку с related branches и iteration history.

## Recommended branch page sections

Для первой итерации branch page рекомендуется делать со следующими sections:

1. `Branch ID`
2. `Parent topic`
3. `Branch question` или `Branch hypothesis`
4. `Why this branch matters`
5. `Scope boundaries`
6. `Context roots`
7. `Evidence roots`
8. `Search anchors`
9. `Branch score / priority`
10. `Key findings`
11. `Unresolved unknowns`
12. `Related branches`
13. `Iteration log`
14. `Next action`

## Context roots

`Context roots` должны указывать, где искать внутренний канонический контекст для ветки.

Обычно это:
- topic root dossier;
- related `docs/` pages;
- relevant `plan artifacts`, `task artifacts` или `discussion artifacts`, если они реально нужны для ветки.

## Evidence roots

`Evidence roots` должны указывать, какие типы внешних источников приоритетны для ветки.

Обычно это:
- official docs;
- repositories;
- issue trackers;
- standards / RFC / specifications;
- benchmark or market sources;
- expert discussions, если они нужны для practical signal.

Ветка не обязана использовать все source families. Она должна явно фиксировать, какие families релевантны именно здесь.

## Search anchors

Каждая branch page должна задавать `search anchors`, пригодные для grep, search queries и agent navigation.

Baseline anchors:
- canonical product / library names;
- competing terms и aliases;
- standards, RFC или protocol names;
- repository names и issue labels;
- identifiers из internal docs, если ветка привязана к существующим artifacts.

## Branch statuses

Для первой итерации рекомендуется такой baseline status model:
- `unseen`
- `scouted`
- `priority-deep`
- `in-progress`
- `blocked`
- `sufficient-for-now`
- `closed`

## Scout-before-deep-focus

Для sibling branches первого уровня рекомендуется invariant:

- никакая ветка не должна переходить в sustained deep-focus, пока остальные sibling branches не получили хотя бы status `scouted`, если только в topic root явно не зафиксирован `hot-path reason`.

Это правило нужно, чтобы не потерять high-value ветку только потому, что первая исследованная ветка выглядела достаточно убедительно.

## Branch portfolio review

После каждой 1-2 глубоких итераций topic root рекомендуется обновлять branch board и явно отвечать на вопросы:
- какие ветки уже scouted;
- где highest decision impact;
- где highest information gain potential;
- почему следующая deep iteration идет именно в выбранную ветку, а не в sibling branches.

## Cross-branch links

Branch pages должны поддерживать explicit cross-links.

Минимально рекомендуется:
- branch page ссылается на parent topic;
- topic root ссылается на все active branches;
- branch page ссылается на related branches, если findings или hypotheses пересекаются;
- iteration file ссылается на branch page и при необходимости на impacted related branches.

## Что этот документ не делает

Этот документ не фиксирует:
- identifier grammar и metadata keys;
- detailed traceability chain;
- search protocol конкретного skill;
- final format research reports вне tree-based storage model.

Эти вопросы принадлежат [`research-traceability.md`](research-traceability.md).

## Связь с другими документами

Этот документ нужно читать вместе с:
- [`research-tree.md`](research-tree.md);
- [`research-traceability.md`](research-traceability.md);
- [`testing-system/test-suites.md`](../testing-system/test-suites.md);
- [`overview.md`](../../overview.md).

## Canonical invariants

- topic root является canonical documentation entry для одного research topic.
- branch page является canonical documentation entry для одной ветки исследования.
- branch page должна задавать `Branch ID`, `Context roots`, `Evidence roots`, `Search anchors` и `Next action`.
- topic root должен поддерживать branch-level navigation и portfolio overview, а не подменять собой branch dossiers.
- sibling branches должны рассматриваться как branch portfolio, а не как линейная очередь без повторной приоритизации.

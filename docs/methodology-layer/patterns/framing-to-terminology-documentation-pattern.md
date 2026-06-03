# Framing-to-Terminology Documentation Pattern

> Status: Draft  
> Scope: reusable pattern для фиксации новой архитектурной модели через focused docs и terminology layer  
> Role: guidance по выбору порядка между discussion framing, Architecture focused specs, terms-map и term pages

## 1. Назначение паттерна

Этот pattern фиксирует workflow для ситуаций, когда человек и агент в обсуждении пришли к новой архитектурной модели и хотят превратить ее в качественную документацию.

Pattern помогает решить, что создавать сначала:

```text
Architecture focused specs
или
terms-map / term pages
```

Ключевая идея: порядок зависит от зрелости модели. Если модель еще формируется, сначала нужны focused docs/framing. Если DDD сущности уже устойчивы, можно сначала создать terminology layer and then write focused docs with links.

## 2. Documentation layers

Паттерн различает три слоя документации.

### Architecture focused specs

Architecture focused specs фиксируют:

- relationships;
- ownership;
- lifecycle;
- execution flow;
- constraints;
- trade-offs;
- boundaries между components, actors and artifacts.

Они не должны становиться главным Source of Truth для определений терминов, если термин уже вынесен в terminology layer.

### Terms-map

Terms-map дает scoped overview всех терминов и DDD сущностей внутри выбранного scope.

Он отвечает за:

- terminology entry point;
- compact glossary map;
- navigation to term pages;
- progressive disclosure для терминов.

### Term pages

Term pages дают более полное представление о конкретном термине.

Они нужны для:

- reusable definition;
- дедупликации документации;
- glossary-first linking;
- единого SoT о DDD сущности или важном architecture concept.

## 3. Default rule

```text
Unstable model -> focused docs first, terms after.
Stable enough model -> terms first, focused docs with links.
```

Это правило защищает от двух ошибок:

1. преждевременно канонизировать терминологию, пока boundaries еще неясны;
2. написать большие focused docs без terminology SoT, а потом получить duplication and inconsistent wording.

## 4. Workflow for unstable model

Используй этот route, когда модель рождается прямо в discussion and many concepts are still being tested.

```text
1. Discussion / framing
2. Architecture focused docs
3. Term extraction
4. Terms-map / term pages sync
5. Dedup / consistency pass
```

Почему так:

- focused docs лучше удерживают relationships and execution flow;
- temporary labels can evolve without pretending to be canonical terms;
- после focused docs видно, какие concepts действительно reusable;
- terminology layer создается на основе уже понятных boundaries.

Этот route подходит для early architecture work, exploratory design, semantic disentangling and Cluster-style discussion.

## 5. Workflow for stable-enough model

Используй этот route, когда после discussion уже ясно, какие DDD сущности and key terms нужно закрепить.

```text
1. Short model outline / decision sketch
2. Term candidate list
3. Minimal terms-map update / key term pages
4. Architecture focused docs with links
5. Consistency pass
```

Почему так:

- focused docs сразу используют agreed terms;
- term pages становятся reusable anchors;
- уменьшается количество локальных определений в focused specs;
- consistency pass становится дешевле.

Этот route подходит, когда concepts уже имеют clear names, responsibilities and boundaries.

## 6. Term candidate checkpoint

Перед созданием term pages полезно сделать checkpoint:

```text
Term candidate review
  -> existing canonical terms
  -> new terms needing terms-map entry
  -> complex terms needing term page
  -> prose-only labels that should not become terms
```

Не каждый label из discussion должен стать термином.

Term page стоит создавать, если concept:

- часто переиспользуется;
- имеет самостоятельную semantic boundary;
- участвует в relationships across multiple focused docs;
- нужен для glossary-first linking;
- иначе будет многократно определяться в prose.

Если concept используется только как локальный explanatory label, его можно оставить внутри focused doc.

## 7. Mini-batch execution

Для больших тем применяй mini-batches:

```text
Batch A: framing / focused docs skeleton
Batch B: term candidate review
Batch C: terms-map and key term pages
Batch D: focused specs completion or dedup
Batch E: final consistency pass
```

Если focused docs уже созданы до terminology sync, не считай работу завершенной до dedup pass.

## 8. Dedup / consistency pass

После terminology sync нужно проверить:

- focused docs ссылками используют term pages при первом meaningful mention;
- definitions не дублируются в нескольких focused docs;
- focused docs остаются про relationships, ownership, lifecycle and flow;
- terms-map содержит новые terms and points to detail pages;
- term pages do not become implementation specs;
- нет competing definitions or contradictory boundaries.

## 9. Anti-patterns

### Premature terminology canon

Создать много term pages до того, как понятны boundaries.

Риск:

- false stability;
- wrong DDD entities;
- expensive renaming;
- fragmented docs.

### Focused-doc-only canon

Зафиксировать всю модель только в focused docs and never extract terms.

Риск:

- duplicated definitions;
- inconsistent wording;
- hard navigation;
- no reusable glossary anchors.

### Everything-is-a-term

Превратить каждый label into term page.

Риск:

- noisy terminology layer;
- too many low-value pages;
- weakened distinction between DDD entity and prose label.

## 10. Invariants

- Focused specs own relationships, ownership, lifecycle and execution flow.
- Terms-map owns terminology overview and navigation.
- Term pages own reusable definitions and semantic boundaries.
- If term boundary is unstable, do not prematurely canonize it.
- If term is repeatedly reused, do not keep redefining it in focused docs.
- The right workflow depends on model maturity, not on a fixed documentation ritual.

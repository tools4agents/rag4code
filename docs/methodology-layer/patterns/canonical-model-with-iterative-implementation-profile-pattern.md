# Canonical Model with Iterative Implementation Profile Pattern

> Status: Draft  
> Scope: reusable pattern для итеративной разработки сложных систем без подмены canonical architecture terms временной реализацией  
> Role: guidance по фиксации стабильной смысловой модели и текущего executable implementation profile в одной эволюционирующей документации

## 1. Назначение паттерна

Этот pattern используется, когда команда разрабатывает систему итеративно и уже имеет работающий упрощенный executable вариант, но не хочет превращать временные scripts, proto components или walking-skeleton shortcuts в canonical domain/architecture terms.

Ключевая идея:

```text
canonical model stays stable enough to guide architecture
  +
current implementation profile documents how this iteration approximates it
  +
git history captures each executable checkpoint
```

Pattern особенно полезен для framework-like systems, где есть разрыв между:

- целевой архитектурной моделью;
- текущей упрощенной реализацией;
- промежуточными стадиями вроде `walking skeleton`, `proto`, `Stage 2 executable increment`;
- scripts/helpers, которые временно исполняют responsibilities будущих компонентов.

## 2. Problem

В итеративной разработке легко смешать два слоя:

```text
Canonical architecture term
  -> durable responsibility / boundary / lifecycle role.

Current implementation detail
  -> how this responsibility is executed in this iteration.
```

Типичный риск:

```text
Storage Worker
  -> canonical term

storage-worker-scripts
  -> temporary implementation label

Proto Storage Worker
  -> another label

Walking Skeleton Storage Worker
  -> another label
```

Через несколько итераций документация начинает содержать много competing entities, хотя реально менялся не domain model, а только способ исполнения.

## 3. Pattern

Фиксируй stable architecture concept как canonical term, а текущую реализацию описывай как `implementation profile` внутри focused architecture spec.

```text
Architecture focused spec
  -> Canonical model
  -> Current implementation profile
  -> Known gaps / non-goals
  -> Evolution policy
```

Не создавай новый canonical term только потому, что текущая реализация script-based, proto или simplified.

Используй descriptive phrase вместо term, например:

```text
current script-based implementation profile of Storage Worker responsibilities
```

а не:

```text
Storage Worker Scripts
```

если это не действительно новая самостоятельная сущность архитектуры.

## 4. Documentation structure

Рекомендуемый focused spec layout:

```text
# <Canonical Architecture Model Name>

## Scope
## Canonical model
## Canonical terms and ownership boundaries
## Current implementation profile: <profile_name>
## What is simplified in this profile
## What remains canonical despite simplification
## Known gaps and future replacement path
## Non-goals
```

В начале документа полезно явно написать:

```text
This document separates canonical architecture terms from the current simplified implementation profile.

Canonical terms define durable responsibilities and boundaries.
The current implementation profile is an executable approximation used in this iteration.
Implementation profile labels are not new domain terms unless explicitly added to the terminology map.
```

## 5. Term canon rule

Новый term стоит добавлять в terminology layer только если concept:

- имеет самостоятельную semantic boundary;
- будет жить дольше одной реализации;
- участвует в нескольких flows/specs;
- не является только packaging/location/script-name detail;
- нужен для glossary-first linking.

Если label описывает только текущий способ исполнения, оставь его в implementation profile section.

Примеры:

| Label | Canonical term? | Почему |
| --- | --- | --- |
| `Storage Worker` | yes | Durable worker family / responsibility boundary. |
| `script-based storage worker implementation profile` | no | Описание текущего способа исполнения. |
| `Node Runner` | yes | Durable runtime/control-plane role. |
| `node-runner-scripts` | no by default | Component source folder / current implementation package. |
| `Dataset Card` | yes | Reusable dataset definition entity. |
| `smoke_classification_6_docs.json` | no | Concrete card instance / config file, not term type. |

## 6. Iterative development loop

Pattern предполагает повторяемый цикл:

```text
1. Agree canonical model slice
2. Document current implementation profile
3. Implement or adjust executable scripts/components
4. Verify the runnable path
5. Commit docs + code as one coherent checkpoint
6. In next iteration, replace implementation profile details without multiplying terms
```

Git history становится механизмом фиксации версий реализации:

```text
commit N:
  canonical model + script-based profile v1 + runnable code

commit N+1:
  same canonical model + improved componentized profile + updated code
```

Если canonical model изменилась, обновляются:

- focused architecture spec;
- terminology map;
- affected term pages;
- implementation profile;
- code/configs.

Если изменилась только реализация, обычно достаточно обновить:

- implementation profile section;
- component README / script docs;
- code/configs.

## 7. Relationship to implementation maturity labels

Labels вроде `walking skeleton`, `proto`, `Stage 2`, `script-based` should describe maturity/status, not create new architecture entities.

Хороший формат:

```yaml
implementation_profile:
  name: script_based_proto
  status: current
  maturity: stage_2_executable_increment
```

Плохой формат:

```text
Stage2StorageWorker
ProtoNodeRunner
WalkingSkeletonOrchestrator
```

если эти names начинают жить как отдельные terms.

## 8. Anti-patterns

### Implementation-name canonization

Временное имя папки, script или helper становится term page.

Риск:

- terminology layer быстро разрастается;
- future replacement requires semantic cleanup;
- readers confuse package names with architecture roles.

### Canonical model overwritten by proto

Документ описывает только то, что делает текущий script, и забывает target responsibility.

Риск:

- архитектура начинает повторять ограничения временной реализации;
- future design кажется breaking change, хотя это planned evolution;
- canonical boundaries становятся слишком низкоуровневыми.

### Parallel model per iteration

Каждая стадия получает свой architecture model:

```text
walking skeleton model
proto model
stage 2 model
target model
```

Риск:

- competing sources of truth;
- unclear migration path;
- semantic drift между docs and code.

## 9. When to use

Use this pattern when:

- текущая реализация intentionally simplified;
- scripts temporarily perform future component responsibilities;
- команда хочет фиксировать progress in git;
- canonical terms уже достаточно ясны;
- implementation will evolve through multiple replacements;
- важно не плодить terms for every maturity stage.

## 10. When not to use

Pattern может быть избыточен, если:

- задача маленькая и одноразовая;
- нет отдельной canonical model;
- implementation detail действительно является новым stable component type;
- документация описывает только локальный script, а не architecture boundary.

## 11. Relationship to other patterns

This pattern complements:

- [`framing-to-terminology-documentation-pattern.md`](./framing-to-terminology-documentation-pattern.md) — for choosing focused spec vs terminology order;
- [`spike-to-prototype-evolution-pattern.md`](./spike-to-prototype-evolution-pattern.md) — for moving from spike to hardened prototype;
- [`reviewable-automation-pattern.md`](./reviewable-automation-pattern.md) — when docs/code updates should follow plan/review/apply/verify.

## 12. Canonical invariants

- Canonical terms describe durable responsibilities, not current shortcuts.
- Implementation profiles describe how the current iteration approximates canonical responsibilities.
- Do not add a term page for every script, folder, maturity stage or temporary adapter.
- If implementation changes but responsibilities stay the same, update the implementation profile, not the canonical term.
- If responsibilities change, update focused spec and terminology layer together.
- Git commits can capture executable checkpoints; terminology should not encode every checkpoint as a new concept.

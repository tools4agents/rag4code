# Trace Chain Type Catalog Decision

> Status: Draft  
> Scope: `traceability-system asset` local design decision  
> Role: объясняет, почему Trace chain instances сейчас используют единую identifier family `TR-` и не имеют отдельного Trace chain type catalog

## Решение

`traceability-system asset` сейчас не вводит `Trace chain type` taxonomy и отдельный `Trace chain type catalog`.

Все Trace chain instances используют одну default Trace Identifier family:

```text
TR-
```

Concrete Trace chain instances различаются через поля Trace map:

- `Trace ID`;
- `Chain`;
- `Meaning`;
- `Status`;
- `Notes`;
- project-local source/context вокруг `docs/traceability/trace-map.md`.

## Контекст

Traceability model разделяет три разных слоя:

```text
Entity / Entity type / Entity instance
Relationship / Relationship type / Relationship instance
Trace chain / Trace chain instance
```

Entity instances представляют разные kinds of traceable things: requirement, user story, architecture component, ADR, test case and others. Поэтому Entity layer нуждается в `Entity type catalog` и Entity Identifier families.

Relationship instances представляют directed semantic links между Entity instances. Их semantics различаются через `Relationship type`, например `details`, `realizes`, `supports`, `constrains`, `verifies` or `implemented-by`. Поэтому Relationship layer нуждается в `Relationship type catalog`.

Trace chain instances представляют curated meaningful paths over Relationship instances. На текущем уровне зрелости asset нет достаточно устойчивых Trace chain classes, которые требовали бы отдельной taxonomy, разных identifier families или разных lifecycle/governance rules.

## Rationale

Отдельный `Trace chain type catalog` сейчас не вводится, потому что он создал бы premature taxonomy.

Потенциальные названия вроде `verification trace`, `implementation trace`, `risk trace` or `release trace` могут оказаться полезными позже, но заранее неясно:

- будут ли это действительно reusable Trace chain types;
- будут ли у них разные lifecycle, review, routing or ownership rules;
- будут ли они отличаться от обычного значения в `Meaning`/`Notes`;
- не приведут ли они к weak labels без operational difference;
- не начнут ли agents придумывать trace categories вместо фиксации actual Relationship instances and meaningful Trace chains.

Пока Trace chain instance достаточно описывается самим path and its meaning:

```text
TR-001: REQ-001 -> CAP-002 -> SCN-003 -> AC-004
Meaning: core product acceptance path for onboarding
```

Если semantic difference важна, она должна быть явно описана в `Meaning` and `Notes`, а не скрыта в premature type label.

## Текущая граница

Этот asset определяет:

- `Entity type catalog`;
- `Relationship type catalog`;
- Entity registries;
- Relationship registry;
- Trace map / Trace chain registry;
- default Trace Identifier family `TR-`.

Этот asset не определяет:

- `Trace chain type catalog`;
- `Trace chain type` drafting skill;
- multiple Trace Identifier families;
- project-wide Trace chain taxonomy.

## Последствия для агентов

Агенты не должны придумывать `Trace chain types`, Trace chain type catalogs or alternative Trace Identifier families во время обычного traceability capture.

Для Trace chain instances нужно использовать `TR-###`, если project-local documentation явно не переопределяет default.

Если candidate Trace chain выглядит как часть recurring class, зафиксируй это как observation, design gap or revisit note. Не создавай новый Trace chain type молча.

Trace chain capture все равно должен проверять, что:

- каждый Entity ID в `Chain` разрешается в Entity instance или явно reported as a gap;
- каждая adjacent pair backed by a Relationship instance или explicit missing prerequisite;
- `Meaning` объясняет, почему этот path важен;
- Trace chain не заменяет missing atomic Relationship instances.

## Условие пересмотра

Это решение можно пересмотреть, если practical usage of the model выявит stable clusters of Trace chains with distinct operational semantics.

Пересмотр оправдан, если у candidate clusters появляются различия такого типа:

- distinct lifecycle or status promotion rules;
- distinct review or consolidation workflow;
- distinct ownership or routing rules;
- distinct downstream consumers;
- distinct graph projection or query semantics;
- repeated need for type-level policy, которую нельзя чисто выразить через `Meaning` and `Notes`.

Возможные future clusters:

- verification traces;
- implementation traces;
- release traces;
- risk traces;
- migration traces.

Такие clusters не следует вводить только ради naming convenience. У них должны быть observable governance, lifecycle or operational differences.

## Последствия

Преимущества:

- более простой traceability language;
- меньше premature classification;
- ниже governance burden;
- более ясное различие между Relationship type semantics and Trace chain path meaning;
- ниже риск, что agents будут придумывать weak trace categories.

Trade-offs:

- Trace map сейчас не может фильтровать записи по formal Trace chain type;
- recurring Trace chain patterns нужно обнаруживать через `Meaning`, `Notes`, source context or derived analysis;
- если позже появятся strong clusters, может понадобиться migration from untyped `TR-###` rows to typed Trace chain taxonomy.

Принятое ограничение:

```text
No Trace chain type catalog until practical usage proves stable, reusable and operationally meaningful Trace chain classes.
```

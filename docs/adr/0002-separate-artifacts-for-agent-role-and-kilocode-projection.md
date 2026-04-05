# ADR 0002: Separate artifacts for `agent-role` core and KiloCode projection

- Status: Accepted
- Date: 2026-03-30
- Deciders: User + Architect
- Related Task: `operational_scope/tasks/arch-011-consolidate-project-methodology-runtime-planning.md`
- Related Architecture: `docs/methodology-layer/workflow-and-roles.md`
- Related Artifact Model: `docs/methodology-layer/artifact-model.md`

## Контекст

В `Project Methodology Runtime` мы проектируем сущность `agent-role` как переносимый и переиспользуемый профиль исполнителя для AI-first разработки.

При этом в Kilo Code уже существует runtime-представление роли через mode model с полями вроде `slug`, `roleDefinition`, `whenToUse`, `customInstructions` и `groups`.

По итогам обсуждения были выделены две разные сущности:
- portable core `agent-role` как reusable role profile;
- KiloCode-specific projection как adapter-specific runtime representation.

Также зафиксировано, что:
- `agent-role` не равен шагу workflow;
- `agent-role` не должен знать, на каких шагах workflow его используют;
- назначение роли на конкретный шаг делается через `step-vacancy` и workflow binding;
- `agent-role` не фиксирует конкретную `LLM model`;
- в долгосрочной перспективе архитектура должна поддерживать несколько agent systems, а не только Kilo Code.

Дополнительный контекст:
- tool access в целевой архитектуре будет идти через HyperToolProxy, а не через прямое копирование KiloCode tool semantics в core model;
- file restrictions остаются полезной role policy, но их runtime mapping может зависеть от adapter;
- графовая БД планируется как механизм навигации и объяснимого связывания reusable core artifacts, adapter projections и workflow bindings.

## Decision statement

Мы выбираем вариант `separate artifacts`.

Portable core `agent-role` и KiloCode projection должны храниться как разные artifacts с явной связью `core role -> adapter projection`.

## Рассмотренные варианты

### 1. No-op: считать KiloCode mode и `agent-role` одной и той же сущностью

Суть:
- использовать KiloCode mode model как фактическую модель роли;
- не разделять core и adapter-specific semantics.

Почему отклонено:
- это слишком рано привязывает домен к Kilo Code;
- усложняет поддержку будущих agent systems;
- смешивает reusable semantics роли и runtime-specific shape.

### 2. `extension block`

Суть:
- один artifact для роли;
- внутри него секция вроде `runtime_overrides.kilocode`.

Плюсы:
- проще стартовать;
- все про роль лежит в одном месте;
- удобно для быстрой миграции из Kilo Code.

Минусы:
- adapter-specific поля загрязняют core artifact;
- падает переносимость роли;
- KiloCode-first shape начинает диктовать модель домена.

Почему не выбрано:
- противоречит приоритету долгосрочной чистоты multi-agent architecture.

### 3. `hybrid`

Суть:
- core роль отдельно;
- projection рядом как sibling artifact в одном role pack.

Плюсы:
- лучше навигация, чем в strict split;
- migration path мягче;
- физическая близость файлов удобна для человека.

Минусы:
- граница между core и adapter может размываться;
- высокий риск, что sibling projection начнет восприниматься как обязательная часть core.

Почему не выбрано:
- архитектурно лучше, чем `extension block`, но все еще оставляет слишком много пространства для semantic drift.

### 4. `separate artifacts`

Суть:
- core `agent-role` хранится как отдельный artifact;
- KiloCode projection хранится как отдельный adapter-specific artifact;
- связь между ними задается явно через references и resolver rules.

Плюсы:
- чистое разделение domain semantics и runtime projection;
- лучше переносимость между проектами и agent systems;
- проще поддерживать future adapters;
- яснее трассировка `workflow -> step-vacancy -> agent-role -> adapter projection`.

Минусы:
- больше сущностей;
- нужен явный resolver;
- выше требования к навигации и traceability tooling.

Почему выбрано:
- это лучший вариант для долгосрочной multi-agent architecture;
- наличие графовой БД и planned traceability tooling снижает навигационный риск;
- пользователь явно выбрал приоритет архитектурной чистоты над краткосрочной простотой.

## Решение

Фиксируем следующие правила.

### 1. Core role artifact

Portable core `agent-role` является отдельным artifact и содержит reusable semantics роли.

Он описывает как минимум:
- identity роли;
- смысловое имя и описание;
- `system_prompt`;
- `allowed_rules`;
- `allowed_skills`;
- `allowed_mcp_tools`;
- optional `when_to_use`;
- optional portable policy вроде `file_access_policy`.

### 2. Adapter projection artifact

KiloCode projection является отдельным artifact.

Он описывает runtime-specific representation core роли для Kilo Code, включая:
- `slug`;
- `roleDefinition` как rendered field;
- optional `customInstructions`;
- runtime mapping для file restrictions и других adapter-specific ограничений.

### 3. Workflow binding layer

`step-vacancy` и workflow bindings не должны ссылаться напрямую на KiloCode projection.

Они должны ссылаться на core `agent-role`.

Adapter projection подключается позднее, на этапе runtime resolution.

### 4. Явная связь

Связь между core и projection должна быть явной и трассируемой:
- `core role -> adapter projection`;
- не через неявное совпадение структуры;
- не через смешение полей в одном artifact.

### 5. Архитектурные состояния

Решение согласуется с четырьмя состояниями архитектуры:

- `Catalog Source of Truth`: хранит reusable core role artifacts и отдельные adapter projection artifacts;
- `Project Portable Intent`: хранит выбор ролей, workflow bindings и `step-vacancy -> role_id` связи;
- `Service-local Runtime State`: хранит resolved operational representation после merge core, overrides и adapter rules;
- `Runtime Materialization State`: хранит уже materialized KiloCode runtime artifacts.

## Rationale

Это решение выбрано потому что:
- reusable `agent-role` не должен зависеть от конкретной agent system;
- KiloCode — только один runtime adapter среди будущих возможных систем;
- `when_to_use` полезен как explainability hint роли, но не должен смешиваться с workflow assignment;
- `customInstructions` полезен как optional overlay, но не должен попадать в core semantics автоматически;
- file restrictions полезны, но должны сначала быть осмыслены как portable role policy, а потом уже проецироваться в KiloCode runtime;
- planned graph database и traceability слой уменьшают стоимость явного split между artifacts.

## Consequences

### Позитивные

- core model остается чище;
- reusable роли легче переносить между проектами;
- легче добавлять новые adapters;
- clearer boundaries между semantic layer, domain layer и adapter layer;
- workflow assignment model остается независимой от runtime implementation.

### Негативные

- появляется больше artifacts и ссылок;
- нужен resolver для `core role -> adapter projection`;
- повышаются требования к documentation quality, graph linking и traceability tooling;
- миграция из текущего KiloCode-first мышления становится немного сложнее.

## Review conditions

Это решение должно быть пересмотрено, если:
- появится evidence, что explicit split создает непропорционально высокую сложность без практической выгоды;
- проект фактически останется навсегда KiloCode-only без реального второго adapter scenario;
- role authoring станет слишком дорогим даже при наличии graph navigation;
- выяснится, что отдельный resolver layer слишком сложен или хрупок.

## Follow-up

После этого ADR нужно:
1. Поддерживать согласованность `separate artifacts` baseline в [`docs/methodology-layer/workflow-and-roles.md`](docs/methodology-layer/workflow-and-roles.md) и [`docs/methodology-layer/artifact-model.md`](docs/methodology-layer/artifact-model.md).
2. Поддерживать термин `step-vacancy` в project terminology artifacts.
3. Развивать packaging conventions для core role artifact и adapter projection artifact через buffer-plan и будущий canonical packaging doc.
4. Увязать будущие contracts с этим ADR после появления соответствующих документов в `docs/contracts/`.

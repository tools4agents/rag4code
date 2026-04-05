# Обсуждение спецификации `agent-role`

> Status: Draft  
> Scope: discussion document before formal specification  
> Related: `docs/terms/project/terms/agent-role.md`  
> Related: `docs/terms/project/terms_map.md`  
> Related: `../../../../.kilocode/how_kilocode_works/modes.md`

## 1. Зачем нужен этот документ

Этот документ нужен как промежуточный discussion layer перед формализацией спецификации `agent-role`.

Здесь мы обсуждаем, как совместить:
- смысловой термин `agent-role` внутри методологии проекта;
- будущую domain entity для реализации в `Project Methodology Runtime`;
- особенности проекции этой сущности в runtime Kilo Code через mode model.

Главная цель — не смешать:
- переносимую сущность роли;
- назначение роли на шаг workflow;
- KiloCode-specific mode fields.

## 2. Зафиксированный semantic baseline

На текущем этапе принято следующее:

### 2.1 `agent-role`

`agent-role` — это самодостаточный reusable профиль исполнителя.

Он задает:
- `system prompt`;
- подмножество `rules`;
- подмножество `skills`;
- подмножество `MCP tools`.

Важно:
- `agent-role` не знает, на каких шагах workflow его используют;
- `agent-role` не фиксирует конкретную `LLM model`;
- одна и та же роль может использоваться в разных workflow и в разных проектах.

### 2.2 `step-vacancy`

`step-vacancy` — это позиция на конкретном шаге конкретного workflow.

Именно `step-vacancy` или сам workflow решает:
- какая `agent-role` подходит для шага;
- какая роль назначается на этот шаг;
- какие результаты ожидаются от шага.

Связь однонаправленная:
- workflow → `step-vacancy` → `agent-role`
- `agent-role` не содержит знания о конкретных шагах workflow.

## 3. Что мы увидели в модели Kilo Code

В [`modes.md`](../../../../.kilocode/how_kilocode_works/modes.md:29) mode включает следующие важные поля:
- [`slug`](../../../../.kilocode/how_kilocode_works/modes.md:179)
- [`name`](../../../../.kilocode/how_kilocode_works/modes.md:189)
- [`description`](../../../../.kilocode/how_kilocode_works/modes.md:197)
- [`roleDefinition`](../../../../.kilocode/how_kilocode_works/modes.md:206)
- [`groups`](../../../../.kilocode/how_kilocode_works/modes.md:222)
- [`whenToUse`](../../../../.kilocode/how_kilocode_works/modes.md:258)
- [`customInstructions`](../../../../.kilocode/how_kilocode_works/modes.md:267)

Это важное наблюдение: mode в Kilo Code уже является runtime projection роли, но не совпадает с проектным понятием `agent-role` один в один.

## 4. Предварительное разделение на слои

Чтобы избежать смешения смыслов, полезно разделить три слоя.

### 4.1 Semantic layer

Смысловой слой термина `agent-role`.

Это уровень `docs/terms/project/terms/agent-role.md`, где объясняется, что такое роль и почему она reusable.

### 4.2 Domain layer

Будущая domain entity `agent-role` внутри `Project Methodology Runtime`.

Это переносимая проектная сущность, которая не должна жестко зависеть от конкретного agent runtime.

### 4.3 Adapter projection layer

Способ проекции `agent-role` в конкретную agent environment.

Для Kilo Code это mode-like representation со своими runtime-specific полями и ограничениями.

## 5. Обсуждение непокрытых полей из Kilo Code

Ниже — предварительный разбор полей, которые пользователь попросил обсудить отдельно.

### 5.1 `slug`

Что это в Kilo Code:
- уникальный identifier mode;
- используется в runtime и в naming для mode-specific directories;
- должен соответствовать ограниченному формату без пробелов и специальных символов.

Вопрос для нашего домена:
- должен ли `slug` быть частью core `agent-role`, или это только adapter-specific projection?
- можно ли считать, что `agent-role.name` и `slug` — это одно и то же?

Наблюдение:
- в Kilo Code [`name`](../../../../.kilocode/how_kilocode_works/modes.md:189) и [`slug`](../../../../.kilocode/how_kilocode_works/modes.md:179) — разные поля;
- `name` человекочитаемое и свободнее по формату;
- `slug` технический идентификатор.

Предварительная позиция:
- в core domain обязателен `role_id` как канонический portable identifier;
- `name` нужен как человекочитаемое имя роли;
- `slug` полезен как projection-friendly identifier, особенно для Kilo Code;
- если `name` уже slug-safe, KiloCode projection может использовать то же значение для `slug`;
- но жестко сливать `name` и `slug` в одно поле рискованно, потому что это ухудшает переносимость и ограничивает именование.

Предварительный вывод:
- `role_id` — канонический identity;
- `name` — обязательное человекочитаемое имя;
- `slug` — optional portable alias или adapter field, который для Kilo Code может совпадать с `name`, если формат подходит.

### 5.2 `whenToUse`

Что это в Kilo Code:
- guidance для mode selection и orchestration.

Наблюдение пользователя:
- это поле полезно, потому что помогает агенту и разработчику понимать, для чего роль вообще создавалась;
- в механике Kilo Code это особенно полезно для динамического переключения роли внутри одного диалога.

Важное различие:
- `whenToUse` не должен описывать конкретный шаг workflow;
- это скорее краткое объяснение, в каких типах задач и ситуаций роль в целом полезна.

Предварительная позиция:
- `whenToUse` стоит поддержать как optional field роли;
- это поле должно жить на уровне reusable role profile, а не на уровне `step-vacancy`;
- workflow по-прежнему решает, где именно назначить роль, но `whenToUse` помогает понять, зачем такая роль существует и когда ее стоит выбирать.

Предварительный вывод:
- `whenToUse` полезен и не должен теряться;
- его можно трактовать как `role activation hint` или краткую guidance-аннотацию роли;
- поле не заменяет workflow assignment, но усиливает explainability и dynamic role switching.

### 5.3 `customInstructions`

Что это в Kilo Code:
- дополнительные behavioral instructions, добавляемые в prompt.

Проблема:
- часть таких инструкций может быть частью самой роли;
- часть может быть project overlay;
- часть может быть runtime-specific prompt augmentation.

Предварительная позиция:
- базовый смысл роли должен жить в `system_prompt`;
- `customInstructions` лучше трактовать как optional overlay;
- это поле не стоит делать обязательным в core, но полезно предусмотреть как extension layer.

Предварительный вывод:
- в core domain можно обсуждать поле вроде `prompt_overlays` или `role_overrides`;
- для Kilo Code projection `customInstructions` стоит сохранить как adapter-specific prompt extension.

### 5.4 `groups`

Что это в Kilo Code:
- доступ к tool groups и file restrictions.

Наблюдение пользователя:
- tool groups в Kilo Code нас не должны жестко ограничивать, потому что в целевой архитектуре доступ к инструментам будет идти через HyperToolProxy;
- при этом file restrictions остаются полезной и осмысленной частью role policy.

Предварительная позиция:
- KiloCode-specific `groups` не стоит переносить в core role spec как есть;
- до появления HyperToolProxy можно считать, что tools доступны всем ролям;
- однако ограничения на тип редактируемых артефактов полезны как portable policy самой роли.

Предварительный вывод:
- вместо прямого поля `groups` в core лучше обсуждать abstract field вроде `file_access_policy` или `edit_scope_policy`;
- default policy может быть `Any`;
- для ролей вроде Architect policy может быть ограничена документацией;
- KiloCode-specific mapping в [`groups`](../../../../.kilocode/how_kilocode_works/modes.md:222) должен жить в adapter projection.

### 5.5 `roleDefinition`

Что это в Kilo Code:
- текст роли, который помещается в начало system prompt.

Вопрос для нашего домена:
- является ли `roleDefinition` отдельным смысловым полем, или это runtime rendering нашего `system_prompt`.

Предварительная позиция:
- на уровне core role model достаточно поля `system_prompt`;
- `roleDefinition` для Kilo Code можно считать projection field, получаемым из `system_prompt` и, возможно, prompt overlays;
- отдельная сущность `roleDefinition` в core пока не нужна.

Предварительный вывод:
- `system_prompt` — core semantic field;
- `roleDefinition` — KiloCode-specific rendered field.

### 5.6 Runtime-specific extensions

Возникает общий вопрос: как работать с полями, которые нужны только отдельной agent system.

Предварительная позиция:
- у нас должен быть portable core role schema;
- поверх него должны существовать adapter-specific extensions;
- Kilo Code — только один из возможных adapters.

Предварительный вывод:
- core слой описывает reusable смысл роли;
- adapter layer добавляет runtime-specific поля;
- для Kilo Code это могут быть `slug`, `roleDefinition`, `customInstructions`, `groups` mapping и другие runtime-specific настройки.

## 6. Предварительный portable core для `agent-role`

На текущем этапе как кандидат на core fields выглядят:
- `role_id`
- `name`
- optional `slug` или другой stable alias для projection-friendly identity
- `description`
- `system_prompt`
- optional `when_to_use`
- `allowed_rules`
- `allowed_skills`
- `allowed_mcp_tools`
- optional `file_access_policy`

Предварительная трактовка:
- `name` — смысловое имя роли;
- `slug` — технический alias, который для Kilo Code может совпадать с `name`, если формат подходит;
- `when_to_use` — короткая guidance-аннотация, зачем роль существует и когда ее в целом полезно выбирать;
- `file_access_policy` — portable ограничение на типы файлов или артефактов, которые роль вправе изменять.

Пока открытые вопросы:
- обязателен ли `slug` в core;
- делать ли `when_to_use` truly core field или optional advisory metadata;
- насколько детализированным должен быть `file_access_policy`.

## 7. Предварительный KiloCode projection для `agent-role`

Если смотреть на проекцию роли в Kilo Code, то для нее вероятно понадобятся:
- `slug`
- `name`
- `description`
- `roleDefinition`
- optional `whenToUse`
- optional `customInstructions`
- optional KiloCode-specific mapping для file restrictions внутри [`groups`](../../../../.kilocode/how_kilocode_works/modes.md:222)

При этом:
- `roleDefinition` трактуется как rendered field из `system_prompt`;
- `customInstructions` трактуется как optional overlay;
- runtime-specific tool groups не считаются канонической частью core, потому что в целевой архитектуре доступ к инструментам должен идти через HyperToolProxy.

Это выглядит как adapter-specific projection schema, а не как полная core спецификация `agent-role`.

## 8. `agent-role` и `KiloCode projection` в четырех состояниях архитектуры

Ниже — предложение, как разнести core и runtime projection по четырем уже принятым состояниям архитектуры.

### 8.1 Catalog Source of Truth

Здесь живут канонические reusable artifacts.

Для `agent-role` это означает:
- portable core role artifact;
- optional adapter-profile artifact для Kilo Code или другой agent system;
- терминологические и specification artifacts, которые объясняют смысл роли.

Здесь важно:
- core роль хранится независимо от конкретного проекта;
- KiloCode projection не подменяет core artifact, а только дополняет его как adapter-specific слой;
- `when_to_use` на этом уровне уместен как часть reusable описания роли;
- `customInstructions` на этом уровне не обязательны и, скорее, не должны быть частью core.

Примерно здесь же должен жить reusable набор ролей, который потом может подключаться разными проектами.

### 8.2 Project Portable Intent

Здесь живет project-owned выбор и настройка reusable сущностей.

Для `agent-role` это означает:
- какие роли активированы в проекте;
- какие роли доступны конкретной methodology;
- какие `step-vacancy` и workflow bindings ссылаются на какие `role_id`;
- project-level overrides это допускается политикой;
- project-specific activation policy и selection policy.

Именно здесь workflow решает:
- какую роль использовать на шаге;
- где одна роль переиспользуется несколько раз;
- как reusable role set входит в конкретную methodology проекта.

На этом уровне не должно быть:
- service-local snapshots;
- materialized Kilo files;
- machine-specific runtime state.

### 8.3 Service-local Runtime State

Здесь живет уже resolved operational representation.

Для `agent-role` это означает:
- merged profile после применения catalog artifacts и project overrides;
- resolved KiloCode projection для конкретного проекта;
- internal records о том, какие runtime fields получаются после сборки;
- snapshots, cache, diagnostics и traceability metadata.

Это не portable слой.

Он нужен, чтобы сервис мог:
- быстро пересобирать runtime;
- объяснять, откуда взялось конкретное materialized mode поле;
- хранить промежуточный resolved state без загрязнения project metadata.

### 8.4 Runtime Materialization State

Здесь живут уже environment-facing runtime artifacts.

Для Kilo Code это означает:
- materialized mode config;
- runtime files и directories, которые реально потребляет Kilo Code;
- rendered `roleDefinition`;
- optional rendered `customInstructions`;
- file restrictions в форме, понятной Kilo runtime.

На этом уровне:
- core semantics уже не редактируются как источник истины;
- это projection, которую можно rebuild;
- shape артефактов зависит от adapter implementation.

## 9. Trade-offs: `separate artifacts` vs `extension block` vs `hybrid`

Ниже — сравнение трех вариантов для связи между portable core роли и KiloCode projection.

### 9.1 Вариант `separate artifacts`

Суть:
- core `agent-role` хранится как отдельный artifact;
- KiloCode projection хранится как отдельный adapter-specific artifact;
- связь между ними задается через references и binding rules.

Как это выглядит:
- reusable role pack содержит core role;
- рядом или в другом adapter namespace лежит KiloCode profile;
- project methodology выбирает core role, а runtime resolver подтягивает нужную projection.

Плюсы для `agent-role`:
- максимально чистое разделение между semantic core и runtime-specific полями;
- проще переносить роль в другую agent system без шума от KiloCode;
- легче развивать несколько adapters параллельно;
- проще объяснить, что `roleDefinition`, `customInstructions` и KiloCode restrictions не являются core role semantics.

Плюсы для `step-vacancy`:
- `step-vacancy` ссылается только на `role_id` и не знает о деталях KiloCode;
- workflow assignment остается чистым и не протекает в adapter layer.

Плюсы для миграции в KiloCode:
- можно постепенно вводить projection artifacts поверх уже существующих role artifacts;
- удобно тестировать альтернативные projections без переписывания core.

Минусы:
- больше сущностей и ссылок;
- выше стоимость навигации и authoring;
- нужен явный resolver `core role -> adapter projection`.

Главный риск:
- если tooling слабый, документация и конфиги могут стать излишне фрагментированными.

### 9.2 Вариант `extension block`

Суть:
- есть один portable role artifact;
- внутри него живет секция вроде `runtime_overrides.kilocode`.

Как это выглядит:
- одна сущность содержит core role fields;
- ниже вложены adapter-specific extensions для KiloCode;
- проект и runtime читают один и тот же artifact.

Плюсы для `agent-role`:
- один файл проще читать и сопровождать;
- все, что относится к роли, находится в одном месте;
- хороший DX на ранней стадии, пока adapters немного.

Плюсы для `step-vacancy`:
- `step-vacancy` по-прежнему может ссылаться только на `role_id`;
- меньше переходов между файлами при понимании, как роль будет выглядеть в runtime.

Плюсы для миграции в KiloCode:
- легче стартовать;
- проще быстро замапить текущие KiloCode modes в новую модель.

Минусы:
- core artifact начинает знать про конкретный runtime;
- снижается переносимость роли между agent systems;
- есть риск, что KiloCode поля постепенно начнут доминировать над core semantics.

Главный риск:
- adapter-specific слой загрязнит Source of Truth и затруднит future adapters.

### 9.3 Вариант `hybrid`

Суть:
- core `agent-role` остается отдельным artifact;
- adapter-specific artifacts допускаются как sibling artifacts в том же role pack;
- pack выступает как контейнер для связанных representation одной роли.

Как это выглядит:
- role pack содержит core role;
- рядом в том же logical bundle лежит KiloCode profile;
- tooling видит это как один role pack, но модель данных различает artifacts.

Плюсы для `agent-role`:
- semantic split сохраняется;
- навигация проще, чем в полностью separate варианте;
- reusable role pack можно переносить между проектами целиком.

Плюсы для `step-vacancy`:
- workflow по-прежнему ссылается на core role, а не на KiloCode projection;
- vacancy binding не загрязняется adapter-specific деталями.

Плюсы для миграции в KiloCode:
- можно начать с role packs, близких к текущему способу мышления;
- KiloCode projection живет рядом и проще понимается человеком;
- легче перейти позже к более строгому split, если понадобится.

Минусы:
- все равно нужен явный semantic boundary;
- без дисциплины sibling artifact может начать восприниматься как обязательная часть core;
- сложнее стандартизировать pack layout, чем один extension block.

Главный риск:
- люди начнут путать удобную физическую близость файлов с логическим отсутствием границы между core и adapter.

### 9.4 Сравнение по ключевым критериям

| Критерий | separate artifacts | extension block | hybrid |
| --- | --- | --- | --- |
| Чистота core model | высокая | низкая | средняя-высокая |
| Простота старта | средняя | высокая | высокая |
| Удобство для future adapters | высокая | низкая | средняя-высокая |
| Удобство чтения человеком | средняя | высокая | высокая |
| Риск загрязнения KiloCode-спецификой | низкий | высокий | средний |
| Удобство миграции текущих modes | среднее | высокое | высокое |
| Чистота связи `workflow -> step-vacancy -> agent-role` | высокая | средняя | высокая |

### 9.5 Предварительное архитектурное ощущение

На текущем этапе наиболее сбалансированно выглядит `hybrid`:
- semantic core роли остается отдельным artifact;
- KiloCode projection лежит рядом как sibling artifact;
- `step-vacancy` и workflow bindings продолжают ссылаться только на core role;
- migration path из текущего KiloCode-first мира получается мягче, чем при strict `separate artifacts`.

Но если приоритет номер один — долгосрочная чистота multi-agent architecture, то сильнее выглядит `separate artifacts`.

## 10. Связь между `agent-role` и `step-vacancy`

Чтобы модель была гибкой, полезно держать следующую структуру:

- `agent-role` — reusable специалист;
- `step-vacancy` — позиция на шаге workflow;
- workflow или vacancy binding выбирает, какая роль закрывает позицию.

Тогда:
- одна роль может использоваться в нескольких `step-vacancy`;
- один workflow может переиспользовать одну и ту же роль в нескольких шагах;
- роль можно переносить между проектами и методологиями.

## 11. Что важно не потерять при формализации

При переходе к формальной спецификации важно не потерять следующие инварианты:
- `agent-role` не равен конкретной `LLM model`;
- `agent-role` не равен шагу workflow;
- `agent-role` потенциально переносим между проектами;
- `when_to_use` не должен подменять workflow assignment;
- `customInstructions` действительно optional overlay и не обязателен даже в KiloCode projection;
- `file_access_policy` полезен как portable policy роли;
- runtime-specific поля Kilo Code не должны загрязнять core domain без явной adapter boundary.

## 12. Как проект выбирает agent system для materialization

Появился дополнительный архитектурный вопрос: сервис должен понимать, для какой agent system materialize runtime projection внутри проекта.

Это означает, что в `Project Portable Intent` должен существовать явный project-level выбор target agent system.

Минимально нужен concept вроде:
- `agent_system_id`
- `adapter_id`
- optional `adapter_profile`

Предварительная позиция:
- проект не должен неявно наследовать agent system только из факта наличия каких-то runtime files;
- project config должен явно говорить, какой adapter projection materialize как основной runtime;
- в будущем проект может поддерживать больше одного adapter target, но в первой итерации лучше иметь один primary target.

Предлагаемый baseline:
- в project settings хранить `primary_agent_system`;
- туда подставляются Enum values из тех agent systems, которые зарегистрированы в нашем сервисе.
- для первой итерации допустимые значения могут быть ограничены, например `kilocode`;
- runtime resolver использует это поле, чтобы понять, какой adapter projection искать и materialize.

Это хорошо согласуется с уже принятой моделью четырех состояний:
- в `Catalog Source of Truth` лежат reusable core artifacts и adapter projections;
- в `Project Portable Intent` хранится выбор agent system для проекта;
- в `Service-local Runtime State` строится resolved projection именно для выбранной system;
- в `Runtime Materialization State` появляются уже конкретные runtime artifacts выбранного adapter.

## 13. Как хранить reusable `agent-role` как пакет

Поскольку `agent-role` по смыслу близок к reusable сущностям вроде `skills`, `rules` и `tools`, важно сделать его удобным для пакетного обмена.

Предварительная цель:
- role definitions должно быть легко переносить между проектами;
- adapter projections должно быть легко переносить вместе с core role или отдельно;
- человек и агент должны быстро понимать состав role pack.

### 13.1 Базовая идея role pack

Предлагаю рассматривать `agent-role` не как одиночный файл, а как logical pack.

Внутри pack могут жить:
- core role artifact;
- optional adapter projection artifacts;
- optional связанная документация и notes;
- optional metadata о версии и совместимости.

При этом из-за принятого ADR core role и adapter projection должны оставаться разными artifacts, даже если физически лежат рядом.

### 13.2 Почему pack полезен

Role pack дает:
- удобный export and import одной роли как reusable capability unit;
- возможность переносить роль вместе с KiloCode projection или без него;
- предсказуемую навигацию для человека и агента;
- меньше риска потерять связанный projection artifact при переносе.

### 13.3 Что должно быть Source of Truth внутри pack

Даже если мы используем pack layout, нужно сохранять разделение:
- core role artifact — Source of Truth для reusable semantics роли;
- adapter projection artifact — Source of Truth для runtime-specific mapping этой роли в конкретную agent system.

То есть pack — это packaging boundary, а не отмена semantic boundary.

## 14. Canonical pack-oriented layout для role packs

Ниже — зафиксированный discussion baseline для хранения role packs.

```text
role-packs/
  architect/
    core/
      role.yaml
    projections/
      kilocode.yaml
    docs/
      overview.md
```

Смысл layout:
- `core/role.yaml` хранит portable core `agent-role`;
- `projections/kilocode.yaml` хранит KiloCode-specific projection как отдельный artifact;
- `docs/overview.md` хранит удобное human-readable описание role pack.

Почему выбран именно этот layout:
- он хорошо согласуется с решением `separate artifacts`;
- явно разделяет semantic core и adapter projection;
- остается удобным для export and import как целого pack;
- хорошо подходит для reusable роли, которую можно переносить между проектами.

Важно:
- pack-oriented layout — это storage and packaging convention;
- он не отменяет semantic split между core и projection;
- workflow bindings по-прежнему должны ссылаться только на core role.

## 15. Где живут описания `agent-role` и adapter projections

### 15.1 В `Catalog Source of Truth`

Именно здесь должен жить reusable набор role packs.

То есть catalog может содержать:
- общий набор reusable ролей;
- общий набор reusable projections для разных agent systems;
- documentation artifacts, объясняющие роли и их назначение.

Это дает возможность:
- переиспользовать роли между проектами;
- хранить KiloCode projection рядом, но отдельно от core role;
- подключать одни и те же роли в разные methodologies.

### 15.2 В `Project Portable Intent`

Здесь проект не должен дублировать полные role definitions.

Здесь должны жить только:
- references на role packs или role ids;
- выбор `primary_agent_system`;
- workflow bindings и `step-vacancy -> role_id`;
- project-level overrides, если они допускаются политикой.

То есть проект выбирает reusable pack, но не копирует его целиком в свой intent layer.

### 15.3 В `Service-local Runtime State`

Здесь сервис строит resolved role bundle для конкретного проекта и конкретной agent system.

Именно здесь соединяются:
- core role artifact;
- project overrides;
- adapter projection;
- runtime-specific derived fields.

### 15.4 В `Runtime Materialization State`

Здесь role pack уже не хранится как pack.

Здесь появляются materialized runtime artifacts выбранной agent system, например:
- mode config для Kilo Code;
- generated instructions;
- runtime file restrictions;
- другие projection outputs.

## 16. Как это соотносится с reusable `skills`, `rules` и `tools`

Удобнее всего мыслить так:
- `agent-role` — это reusable orchestration profile;
- `skills`, `rules` и `tools` — reusable capability sets;
- methodology и workflow связывают их в конкретный process.

Это значит, что role pack по смыслу похож на capability pack:
- роль может ссылаться на reusable skills;
- роль может ссылаться на reusable rules;
- роль может ссылаться на abstract tool capabilities;
- adapter projection уже переводит это в shape конкретной agent system.

Такой подход делает role packs удобными для обмена и сборки methodology по LEGO-принципу.

## 17. Зафиксированный discussion baseline

На текущем этапе как discussion baseline зафиксировано следующее:
- reusable `agent-role` хранится как core artifact внутри role pack;
- adapter projections вроде KiloCode хранятся как отдельные artifacts внутри `projections/` того же pack;
- project config хранит `primary_agent_system` и workflow bindings, но не копирует role pack целиком;
- service runtime resolver по `primary_agent_system` выбирает нужный adapter projection;
- materialization делает только projection выбранной agent system.

Это сохраняет:
- переносимость reusable ролей;
- чистое разделение core и adapter;
- удобство обмена role packs;
- предсказуемую materialization policy.

## 18. Следующий шаг

Следующим шагом нужно решить:
- как назвать project-level поле выбора agent system;
- нужен ли отдельный reusable pack concept не только для ролей, но и для связок role + skills + rules;
- как formal spec должна описать `step-vacancy` и workflow assignment layer поверх role packs.

Этот документ пока остается discussion draft и должен стать источником для будущей формальной спецификации `agent-role`.

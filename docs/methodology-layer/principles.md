# Principles for Project Methodology Runtime

> Status: Draft  
> Scope: принципы, которыми мы руководствуемся при проектировании слоя `Project Methodology Runtime`  
> Role: канонический список архитектурных и методологических принципов слоя

## 1. Назначение документа

Этот документ фиксирует принципы, которыми мы руководствуемся при принятии решений по слою `Project Methodology Runtime`.

Он нужен, чтобы:
- не повторять одни и те же rationale в каждом spec-документе;
- сохранять единый стиль архитектурных решений;
- упростить обсуждение trade-offs между человеком и агентом;
- дать устойчивую опору для дальнейшей formal specification.

Базовые проектные ценности и общие принципы вынесены в [`docs/principles.md`](docs/principles.md).

Этот документ описывает уже не общую философию проекта, а производные архитектурные принципы и patterns решений именно для слоя `Project Methodology Runtime`.

## 2. Принцип удобства для человека и агента

Мы проектируем слой так, чтобы с ним было удобно работать:
- разработчику-человеку;
- ИИ-агенту;
- смешанной команде человек + агент.

Это означает, что документация, role packs, workflow и runtime artifacts должны быть:
- понятными;
- предсказуемыми;
- навигируемыми;
- пригодными для постепенного чтения и повторного использования.

### 2.1 Базовые ценности

Поверх общего принципа удобства мы явно фиксируем четыре базовые ценности:
- открытость;
- понятность;
- гибкость;
- трассируемость.

#### Открытость

Мы стремимся к открытой и `open source`-дружественной платформе, в которой разработчики могут делиться workflow, roles, skills, rules, projections и другими assets друг с другом.

Открытость означает:
- понятные структуры артефактов;
- переносимые packs;
- минимум скрытой магии;
- возможность повторного использования наработок в других проектах.

#### Понятность

Система должна быть понятной человеку и агенту без необходимости угадывать скрытые правила.

Это означает:
- явные термины;
- ясные boundaries между сущностями;
- предсказуемую документационную структуру;
- читаемые explanation layers до перехода к runtime detail.

#### Гибкость

Архитектура не должна жестко прибивать проект к одной методологии, одному workflow или одной agent system.

Гибкость означает:
- возможность менять методологии
- возможность менять workflow без пересборки core role semantics;
- переиспользуемые `agent-role`;
- поддержку разных adapter projections;
- возможность эволюции через overlays, bindings и новые packs.

#### Трассируемость

Любое важное решение, binding и runtime projection должно быть объяснимо.

Трассируемость означает:
- понятные связи `workflow -> workflow-step -> step-vacancy -> agent-role`;
- явные связи `core artifact -> adapter projection`;
- навигацию через derived graph;
- возможность восстановить, почему в проекте materialized именно такой runtime.

## 3. `lazy loading` и `progressive disclosure`

Документация и methodology artifacts не должны заставлять человека или агента читать все сразу.

Поэтому мы придерживаемся многоуровневой структуры:
- обзорный уровень;
- терминологический уровень;
- focused specs;
- discussion docs;
- contracts и runtime-facing artifacts.

Чтение должно идти от общего к частному:
- сначала карта слоя;
- затем карта терминов;
- затем только нужный focused spec;
- затем конкретный contract или detailed artifact.

## 4. Модульность и удобство распространения assets

Workflow, `agent-role`, skills, rules, projections и другие artifacts должны быть устроены так, чтобы разработчикам было удобно делиться ими друг с другом.

Мы стремимся к построению `open source` платформы для открытого обмена наработками между всеми разработчиками, которые захотят ими поделиться. 

Мы стремимся к тому, чтобы assets можно было:
- переносить как пакеты;
- подключать как reusable наборы;
- комбинировать по LEGO-принципу;
- адаптировать под конкретный проект без копирования всей системы целиком.

Именно поэтому reusable сущности отделяются от project-specific bindings и runtime materialization.

## 5. Reusable first

Если сущность может быть переиспользована в другом проекте, она должна проектироваться как reusable по умолчанию.

Это особенно относится к:
- `agent-role`;
- skills;
- rules;
- workflows;
- adapter projections;
- packs of assets.

Project-specific слой должен прежде всего ссылаться на reusable artifacts, а не дублировать их.

## 6. Явное разделение semantic layers

Мы стараемся не смешивать в одном артефакте разные уровни смысла.

Нужно отделять:
- смысловой термин;
- reusable domain entity;
- workflow assignment;
- adapter-specific projection;
- runtime materialization.

Примеры разделения:
- `agent-role` не равен шагу workflow;
- `step-vacancy` не равен reusable роли;
- `workflow-step` не равен overview workflow;
- `workflow-step` не равен `workflow-step-pack`;
- `workflow` не равен `workflow-pack`;
- KiloCode projection не равен core role artifact.

## 7. Separate artifacts вместо скрытого смешения

Если reusable core и adapter-specific projection имеют разную природу, они должны быть разными artifacts.

Это помогает:
- сохранить чистоту domain model;
- не привязывать core слой к одной agent system;
- поддерживать future adapters без переписывания core semantics.

Именно поэтому core `agent-role` и KiloCode projection мы рассматриваем как separate artifacts.

## 8. `pack-oriented layout` как packaging convention

Хотя semantic сущности должны быть разделены, физически их удобно хранить в `pack-oriented layout`.

Это значит:
- core artifacts;
- adapter projections;
- human-readable docs;
- связанная metadata

могут жить рядом внутри одного pack, но не теряют своей логической границы.

Этот подход нужен для:
- удобного export and import;
- простой навигации;
- удобного обмена наработками между разработчиками и проектами.

## 9. File-first Source of Truth

Канонический `Source of Truth` для methodology artifacts — это files, а не database.

В частности:
- markdown и yaml artifacts остаются каноническими;
- database хранит derived representation;
- runtime materialization считается projection, а не главным источником смысла.

Это сохраняет:
- прозрачность;
- git-friendly versioning;
- возможность восстановления состояния;
- удобство ручного редактирования человеком.

## 10. Portable intent, local runtime

Проект должен хранить только переносимое намерение, а не machine-specific состояние.

Поэтому мы различаем:
- `Catalog Source of Truth`;
- `Project Portable Intent`;
- `Service-local Runtime State`;
- `Runtime Materialization State`.

Это разделение помогает:
- переносить проект между машинами;
- materialize разные agent systems из одного intent layer;
- избегать смешения логического выбора и физического размещения файлов.

## 11. Adapter isolation

Каждая agent system должна подключаться через adapter boundary.

Это значит:
- core model не должен протекать KiloCode-specific details;
- runtime-specific поля должны жить в projection layer;
- project может выбирать `primary_agent_system`, а сервис materialize только нужный adapter projection.

Это создает основу для multi-agent architecture вместо KiloCode-only дизайна.

## 12. Workflow-centered development

Методология проекта рассматривается как организация разработки через workflow.

При этом нужно различать:
- `workflow` как карту процесса;
- `workflow-step` как подробное и исполнимое описание конкретного шага;
- `workflow-pack` как packaging boundary для workflow artifacts;
- `workflow-step-pack` как packaging boundary для artifacts конкретного шага;
- `step-vacancy` как позицию на шаге;
- `agent-role` как reusable профиль исполнителя.

Такое разделение делает процесс:
- более явным;
- более трассируемым;
- более гибким для замены ролей и адаптеров.

## 13. Explainability и traceability by design

Мы проектируем слой так, чтобы человек и агент могли понять:
- почему активирована конкретная роль;
- откуда взялся runtime artifact;
- какой workflow использует какой step;
- какой adapter projection materialized в проекте;
- как связаны artifacts, роли, шаги и runtime outputs.

Именно поэтому графовая БД и derived graph projection рассматриваются как важный слой навигации и объяснимости.

## 14. Explicit over implicit

Где возможно, мы предпочитаем явные решения неявным эвристикам.

Это относится к:
- `manual-hybrid discovery`;
- выбору `primary_agent_system`;
- связи `workflow -> step-vacancy -> agent-role`;
- связыванию core artifacts и adapter projections;
- file access policy и runtime restrictions.

Явность снижает риск скрытых предположений и делает систему безопаснее для эволюции.

## 15. Recommendation over coercion

Методология должна помогать разработчикам и агентам, а не мешать им.

Поэтому методология проекта носит рекомендательный характер:
- она предлагает удобные workflow;
- задает reusable роли и assets;
- помогает навигации и согласованности;
- но не должна превращаться в чрезмерно жесткую бюрократию.

Главная цель — сделать работу над проектом удобнее, а не формальнее ради формальности.

## 16. Эволюционность

Мы допускаем, что архитектура будет развиваться.

Поэтому при проектировании решений мы стараемся:
- оставлять extension points;
- избегать преждевременного hardcoding;
- сохранять future-friendly boundaries;
- фиксировать идеи дальнейшего развития отдельно, не смешивая их с текущим baseline.

Это уже проявляется в идеях вроде dynamic step-vacancy role binding, которые зафиксированы как future evolution, но не включены в текущую реализацию.

## 17. Как использовать этот документ

Этот документ должен использоваться как reference при:
- создании новых focused specs;
- обсуждении trade-offs;
- создании ADR;
- проектировании role packs, workflow artifacts и adapter projections;
- миграции planning docs в каноническую структуру документации.

Если новое решение противоречит этим принципам, это должно быть либо явно обосновано, либо вынесено в отдельное архитектурное обсуждение.

# Карта project-specific терминов

> Status: Draft  
> Scope: термины, специфичные для HyperGraph и слоя `Project Methodology Runtime`  
> Role: локальный glossary для человека и агента, который дополняет общую карту из `docs/terms/common/terms_map.md`

## 1. Назначение

Этот документ хранит термины, которые значимы именно для текущего проекта или для его локальной методологии.

Он нужен для:
- отделения project-specific понятий от общих reusable terms;
- поддержки `lazy loading` для человека и агента;
- фиксации локальных договоренностей проекта без смешения с переносимой общей терминологией;
- постепенного раскрытия сложных понятий через отдельные страницы по мере необходимости.

Общие термины должны жить в `docs/terms/common/terms_map.md`.

## 2. Как пользоваться этим файлом

Рекомендуемый маршрут чтения:
1. сначала прочитать краткое определение здесь;
2. если термин имеет отдельную detail page, открыть ее только при необходимости;
3. вернуться в текущий архитектурный или методологический документ.

Для полного терминологического контекста агент и человек должны сначала читать:
- `docs/terms/common/terms_map.md`;
- `docs/terms/project/terms_map.md`.

## 3. Правила для project-specific terms

- сюда попадают только термины, смысл которых задается текущим проектом или его методологией;
- если термин требует подробного раскрытия, для него создается отдельная страница в `docs/terms/project/terms/`;
- архитектурные документы должны ссылаться на эту карту вместо повторения длинных определений;
- если локальный термин со временем становится reusable для других проектов, его можно перенести в `docs/terms/common/`.

## 4. Канонический реестр project-specific терминов

| Термин | Краткое определение | Детальная страница |
| --- | --- | --- |
| Project Methodology Runtime | Слой HyperGraph, который управляет methodology artifacts проекта, хранит project methodology intent, materialize runtime для agent environment и поддерживает traceability через derived graph. | none |
| methodology | В контексте проекта это формализованная модель разработки ПО вместе с командой ИИ-агентов: она задает `methodology workflow`, активные rules, skills, MCP tools и другие process artifacts. Методология также может содержать описания отдельных `workflow`, которые используются внутри проекта. | none |
| methodology workflow | Центральный workflow разработки проекта. Он задает основную методологию разработки, главный процесс, которого придерживаются при разработке проекта, и определяет как связываются workflow, шаги, роли и результаты. Методология носит рекомендательный характер и должна быть удобной для разработчиков и агентов. | none |
| workflow | Markdown-артефакт, который описывает цель процесса, optional входы, последовательность шагов с кратким идейным описанием и optional общий выход. `workflow` не назначает `step-vacancy` напрямую: он только задает карту процесса и ссылки на подробные `workflow-step`. | `docs/terms/project/terms/workflow.md` |
| workflow-step | Отдельный markdown-артефакт, который подробно описывает конкретный шаг workflow: входы, что нужно сделать, связанную `step-vacancy`, назначенную на нее `agent-role`, выходы, `DoD` и критерии возврата на предыдущие шаги. | `docs/terms/project/terms/workflow-step.md` |
| agent-role | Самодостаточный reusable role profile агента или человека с `system_prompt` и подмножествами `rules`, `skills` и `MCP tools`. Роль не знает, на каких шагах ее будут использовать: это решает `workflow-step` через `step-vacancy`. Одна и та же роль может входить в общий reusable набор и затем подключаться как подмножество в разных workflow конкретной методологии. | `docs/terms/project/terms/agent-role.md` |
| step-vacancy | Позиция на конкретном шаге конкретного workflow, которая должна быть закрыта подходящей `agent-role`. `step-vacancy` отвечает за назначение роли на шаг, а не за описание самой роли или полной логики шага. | `docs/terms/project/terms/step-vacancy.md` |
| role-specific rules | Подмножество rules, которое привязано к конкретной `agent-role` как к reusable role profile и затем используется там, где `workflow-step` через `step-vacancy` выбирает эту роль. | none |
| role-specific skills | Подмножество skills, которое доступно конкретной `agent-role` как reusable role profile и затем используется в тех workflow-step, где эта роль назначена исполнителем через `step-vacancy`. | none |
| role-specific MCP tools | Подмножество MCP tools, доступных или приоритетных для конкретной `agent-role` как reusable role profile. | none |
| project-scoped runtime | Согласованный runtime layer проекта, который materialize для agent system как единый локальный слой consumption. | none |
| Central methodology catalog | Локально для этого слоя — внутренний catalog methodology artifacts, откуда проект получает reusable artifacts по stable references. | none |
| manual-hybrid discovery | Discovery mode для этого слоя, в котором сервис heuristically находит candidates, а разработчик вручную подтверждает final classification. | none |
| project candidate | Найденная discovery-механизмом директория, которая может оказаться `root-project`, `nested-project`, `external-project-reference`, `ignored-git-root` или `service-managed-root`. | none |
| nested-project | Вложенный project внутри другого project root, который классифицирован как самостоятельный project node. | none |
| external-project-reference | Связанный project, важный для navigation и integration, но не обязательно локально indexed как редактируемый project. | none |
| service-managed-root | Служебная директория слоя, принадлежащая самому сервису и не считающаяся user project. | none |

## 5. Какие термины требуют особой синхронизации

Следующие project-specific термины должны использоваться во всех документах слоя строго единообразно:
- Project Methodology Runtime
- methodology
- methodology workflow
- workflow
- agent-role
- role-specific rules
- role-specific skills
- role-specific MCP tools
- project-scoped runtime
- Central methodology catalog
- manual-hybrid discovery
- nested-project
- external-project-reference
- service-managed-root

## 6. Какие термины стоит раскрывать отдельными страницами в первую очередь

Первыми кандидатами на отдельные detail pages являются:
- `agent-role`;
- `methodology`;
- `methodology workflow`;
- `workflow`;
- `Project Methodology Runtime`.

Именно эти понятия сильнее всего влияют на архитектуру слоя и на то, как агент читает и исполняет проектную методологию.

## 7. Политика обновления

Обновляй эту карту, если:
- в документации появляется новый локальный термин, важный для понимания workflow или architecture;
- проект меняет трактовку роли агента, workflow или runtime behavior;
- появляется новая detail page в `docs/terms/project/terms/`;
- часть терминов перестает быть project-specific и переносится в `docs/terms/common/`.

Эта карта является канонической точкой входа для project-specific терминов HyperGraph.
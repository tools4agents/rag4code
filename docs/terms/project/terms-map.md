# Карта project-specific терминов

> Status: Draft  
> Scope: термины, специфичные для HyperGraph и слоя `Project Methodology Runtime`  
> Role: локальный glossary для человека и агента, который дополняет общую карту из `docs/terms/common/terms-map.md`

## 1. Назначение

Этот документ хранит термины, которые значимы именно для текущего проекта или для его локальной методологии.

Он нужен для:
- отделения project-specific понятий от общих reusable terms;
- поддержки `lazy loading` для человека и агента;
- фиксации локальных договоренностей проекта без смешения с переносимой общей терминологией;
- постепенного раскрытия сложных понятий через отдельные страницы по мере необходимости.

Общие термины должны жить в `docs/terms/common/terms-map.md`.

## 2. Как пользоваться этим файлом

Рекомендуемый маршрут чтения:
1. сначала прочитать краткое определение здесь;
2. если термин имеет отдельную detail page, открыть ее только при необходимости;
3. вернуться в текущий архитектурный или методологический документ.

Для полного терминологического контекста агент и человек должны сначала читать:
- `docs/terms/common/terms-map.md`;
- `docs/terms/project/terms-map.md`.

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
| workflow | Семантическая process entity, которая описывает последовательность шагов, объединенных общей целью и смыслом. Технически workflow обычно authoring-ся через `workflow-pack`, внутри которого есть канонический markdown с картой процесса и ссылками на `workflow-step`. | `docs/terms/project/terms/workflow.md` |
| workflow-pack | Packaging boundary для одного `workflow`: директория, в которой лежат канонический workflow overview, ссылки на шаги, optional workflow-level metadata и общие сопутствующие материалы. | `docs/terms/project/terms/workflow-pack.md` |
| workflow-step | Семантическая process entity, которая описывает конкретный шаг workflow: его входы, действие, выходы, `DoD`, failure/return semantics и связь с `step-vacancy`. Технически шаг обычно authoring-ся через `workflow-step-pack`, который содержит каноническое описание шага и support artifacts. | `docs/terms/project/terms/workflow-step.md` |
| workflow-step-pack | Packaging boundary для одного `workflow-step`: директория, в которой лежат канонический step markdown, шаблоны, чеклисты, references, examples и другие материалы, нужные для выполнения шага. | `docs/terms/project/terms/workflow-step-pack.md` |
| workflow-exchange layer | Временный workflow-specific exchange layer внутри `Operational Documentation Layer`, который хранит instance-specific handoff artifacts между шагами конкретного workflow-run. | `docs/terms/project/terms/workflow-exchange-layer.md` |
| agent-role | Самодостаточный reusable role profile агента или человека с `system_prompt` и подмножествами `rules`, `skills` и `MCP tools`. Роль не знает, на каких шагах ее будут использовать: это решает `workflow-step` через `step-vacancy`. Одна и та же роль может входить в общий reusable набор и затем подключаться как подмножество в разных workflow конкретной методологии. | `docs/terms/project/terms/agent-role.md` |
| step-vacancy | Позиция на конкретном шаге конкретного workflow, которая должна быть закрыта подходящей `agent-role`. `step-vacancy` отвечает за назначение роли на шаг, а не за описание самой роли или полной логики шага. | `docs/terms/project/terms/step-vacancy.md` |
| knowledge-lifecycle asset | Asset type, который задает lifecycle знания в проекте: где оно рождается, где канонизируется и где публикуется для внешнего потребления. | `docs/terms/project/terms/knowledge-lifecycle-asset.md` |
| task-management-system asset | Asset type, который задает систему хранения, индексации и управления task artifacts. | `docs/terms/project/terms/task-management-system-asset.md` |
| project-context-entry-system asset | Asset type, который задает reusable систему project context entry points, loading order и ownership split между `AGENTS.md`, `project/`, `docs/`, `operational_scope/` и related layers. | `docs/terms/project/terms/project-context-entry-system-asset.md` |
| terms-management-system asset | Asset type, который задает систему хранения и progressive disclosure терминов. | `docs/terms/project/terms/terms-management-system-asset.md` |
| research-management-system asset | Asset type, который задает систему хранения, дерева веток и traceability для research artifacts. | `docs/terms/project/terms/research-management-system-asset.md` |
| testing-system asset | Asset type, который задает систему хранения, индексации и traceability для testing documentation и links к test implementation. | `docs/terms/project/terms/testing-system-asset.md` |
| methodology asset | Asset type, который задает process model разработки и methodology-specific semantics. | `docs/terms/project/terms/methodology-asset.md` |
| project stage | Крупная bounded phase внутри execution plan проекта, которая группирует связанные задачи и задает dependency order между слоями работы. | `docs/terms/project/terms/project-stage.md` |
| composition pack | Publishable совместимый набор assets разных типов, который можно подключить как готовый методологический стек. | `docs/terms/project/terms/composition-pack.md` |
| Operational Documentation Layer | Временный operational слой, в котором рождается, уточняется и проверяется новое знание до его канонизации. | `docs/terms/project/terms/operational-documentation-layer.md` |
| Engineering Documentation SoT | Канонический инженерный Source of Truth проекта. | `docs/terms/project/terms/engineering-documentation-sot.md` |
| Release Documentation Layer | Release-ready documentation для внешнего потребления. | `docs/terms/project/terms/release-documentation-layer.md` |
| idea artifact | Operational artifact для фиксации новой идеи, инсайта или направления дальнейшей проработки. | `docs/terms/project/terms/idea-artifact.md` |
| plan artifact | Operational artifact для фиксации плана изменения, проектирования или исследования. | `docs/terms/project/terms/plan-artifact.md` |
| task artifact | Operational artifact для фиксации исполнимой задачи, ее контекста и execution status. | `docs/terms/project/terms/task-artifact.md` |
| research artifact | Operational artifact для фиксации результатов исследования и сравнения вариантов. | `docs/terms/project/terms/research-artifact.md` |
| discussion artifact | Operational artifact для фиксации обсуждения, альтернатив и промежуточных выводов. | `docs/terms/project/terms/discussion-artifact.md` |
| review artifact | Operational artifact для фиксации critic/reviewer feedback и quality assessment. | `docs/terms/project/terms/review-artifact.md` |
| open question | Явно зафиксированный нерешенный вопрос, требующий дальнейшей проработки. | `docs/terms/project/terms/open-question.md` |
| white spot | Зафиксированный пробел в знаниях, документации или понимании системы. | `docs/terms/project/terms/white-spot.md` |
| spike report | Operational artifact с результатом небольшого PoC или кодового эксперимента для проверки гипотезы. | `docs/terms/project/terms/spike-report.md` |
| role-specific rules | Подмножество rules, которое привязано к конкретной `agent-role` как к reusable role profile и затем используется там, где `workflow-step` через `step-vacancy` выбирает эту роль. | none |
| role-specific skills | Подмножество skills, которое доступно конкретной `agent-role` как reusable role profile и затем используется в тех workflow-step, где эта роль назначена исполнителем через `step-vacancy`. | none |
| role-specific MCP tools | Подмножество MCP tools, доступных или приоритетных для конкретной `agent-role` как reusable role profile. | none |
| project-scoped runtime | Согласованный runtime layer проекта, который materialize для agent system как единый локальный слой consumption. | none |
| Central methodology catalog | Локально для этого слоя — внутренний catalog methodology artifacts, откуда проект получает reusable artifacts по stable references. | none |
| test-suite | Documentation unit, который объединяет связанный набор test cases, links на implementation roots и suite-level navigation metadata. | `docs/terms/project/terms/test-suite.md` |
| test-case | Минимальная documented verification unit внутри `test-suite`, которая имеет stable identifier и связывает requirement-level intent с конкретной test implementation. | `docs/terms/project/terms/test-case.md` |
| test-implementation | Code-level реализация test case в test module, test class или test function. | `docs/terms/project/terms/test-implementation.md` |
| repository-context-entry-model | Система входных точек и загрузки контекста проекта, которая задает `structure + navigation + ownership` для project-scoped agent work. | `docs/terms/project/terms/repository-context-entry-model.md` |
| nested-repo-context-switching | Правило переключения агента с parent project context на local context автономного nested project, когда task scope уходит внутрь этого repository. | `docs/terms/project/terms/nested-repo-context-switching.md` |
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
- workflow-pack
- workflow-step
- workflow-step-pack
- workflow-exchange layer
- agent-role
- knowledge-lifecycle asset
- task-management-system asset
- project-context-entry-system asset
- terms-management-system asset
- research-management-system asset
- testing-system asset
- methodology asset
- project stage
- composition pack
- Operational Documentation Layer
- Engineering Documentation SoT
- Release Documentation Layer
- idea artifact
- plan artifact
- task artifact
- research artifact
- discussion artifact
- review artifact
- open question
- white spot
- spike report
- role-specific rules
- role-specific skills
- role-specific MCP tools
- project-scoped runtime
- Central methodology catalog
- test-suite
- test-case
- test-implementation
- repository-context-entry-model
- nested-repo-context-switching
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

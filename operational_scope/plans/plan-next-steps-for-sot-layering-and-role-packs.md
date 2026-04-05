# Plan: Следующие шаги по SoT layering, asset packs и agent-role projections

## Контекст

В ходе текущей проработки `Project Methodology Runtime` уже удалось согласовать несколько важных решений:

- нужны четыре уровня Source of Truth:
  - `HyperGraph domain SoT`;
  - `Methodology SoT`;
  - `Project SoT`;
  - `Global runtime/tooling SoT`;
- reusable `agent-role` нужно отличать от `workflow-step` и `step-vacancy`;
- `workflow-step` является methodology-bound executable step, а не reusable role semantics;
- `skill` рассматривается как reusable capability, которую не нужно преждевременно выделять из workflow-step;
- core `agent-role` и adapter-specific projection должны оставаться separate artifacts;
- `role pack` уже принят как packaging boundary для reusable role unit.

Связанные канонические документы:

- `docs/methodology-layer/overview.md`
- `docs/methodology-layer/principles.md`
- `docs/methodology-layer/artifact-model.md`
- `docs/methodology-layer/workflow-and-roles.md`
- `docs/methodology-layer/interfaces-and-storage.md`
- `docs/terms/terms_map.md`
- `docs/terms/project/terms/agent-role.md`
- `docs/terms/project/terms/workflow.md`
- `docs/terms/project/terms/workflow-step.md`
- `docs/terms/project/terms/step-vacancy.md`
- `docs/adr/0002-separate-artifacts-for-agent-role-and-kilocode-projection.md`

## Цель

Собрать следующий практический слой решений так, чтобы:

- зафиксировать ownership и sync model между слоями SoT;
- нормализовать представление reusable asset packs;
- подготовить multi-agent-system модель через abstract artifact + adapter projection;
- убрать оставшиеся терминологические gaps между `methodology-layer` и `docs/terms/`;
- подготовить удобную структуру для дальнейшей materialization в конкретные agent systems.

## Уже принятые направляющие решения

### 1. Four-layer SoT model

Принимаем следующие logical layers:

- `HyperGraph domain SoT` — владеет domain entities, governance и layering rules;
- `Methodology SoT` — владеет reusable methodology packs вроде `waterfall`;
- `Project SoT` — владеет project-specific overlay и adoption decisions;
- `Global runtime/tooling SoT` — владеет global runtime defaults, reusable packs и environment-facing tooling settings.

### 2. `workflow-step` vs `skill`

Принимаем следующий рабочий baseline:

- `workflow-step` — это methodology-bound executable step;
- `skill` — это reusable capability, не привязанная к одному workflow;
- на раннем этапе проектируем rich workflow-steps;
- в reusable skills выносим только стабилизированные и действительно повторяемые протоколы.

### 3. Multi-representation model for `agent-role`

Для reusable role unit принимаем трехуровневую модель:

1. abstract core artifact;
2. adapter-specific artifact для конкретной agent system;
3. runtime materialization в проекте для выбранной environment.

Целевой пример для role pack:

```text
agent_roles/
  critic/
    role.md
    kilo/
      role.md
```

## Проблема текущего состояния

Сейчас модель уже почти сложилась, но еще не доведена до полностью явного состояния:

- ownership между слоями SoT проговорен, но еще не зафиксирован как канонический policy set;
- representation model для reusable assets уже поддерживается `methodology-layer`, но еще не до конца отражен в glossary;
- naming и taxonomy для references, methodologies, role packs и projections еще нужно стандартизовать;
- структура materialized assets и abstract assets начинает складываться, но ей пока не хватает короткого roadmap и набора follow-up задач.

## Что именно нужно сделать

### Workstream 1. Зафиксировать governance поверх SoT layers

Нужно описать и канонизировать:

1. `ownership matrix`
   - какой слой чем владеет;
   - где находится semantic owner;
   - что может быть только overlay, а не independent canon.

2. `promotion protocol`
   - как поднимать полезное уточнение из project-specific или adapter-specific контекста в owner layer;
   - как различать `origin layer` и `owner layer`;
   - как выполнять downstream sync после promotion.

3. `composition manifest`
   - как описывать согласованную композицию domain, methodology, role, skill и project overlay assets;
   - как фиксировать selected versions и active agent system.

Ожидаемый результат:
- layered SoT model перестает быть устной договоренностью и становится explicit governance baseline.

### Workstream 2. Нормализовать taxonomy reusable packs

Нужно зафиксировать distinction между:

- `agent-role pack`;
- `skill pack`;
- `rule pack`;
- `methodology pack`;
- `reference pack`;
- `project overlay pack`.

Дополнительно нужно определить:

- какие packs являются abstract/reusable;
- какие являются adapter-specific;
- какие являются materialized runtime outputs;
- где проходит граница между pack structure и semantic ownership.

Ожидаемый результат:
- все основные families reusable assets получают единый vocabulary и перестают смешиваться.

### Workstream 3. Нормализовать references как отдельную family of assets

Нужно заменить Kilo-only naming на более общий reference model.

Целевое направление:

```text
assets/
  references/
    kilo/
    opencode/
```

Нужно зафиксировать, что:

- reference packs не являются domain canon HyperGraph;
- они нужны как external knowledge about target agent systems;
- у проекта может быть несколько reference families для разных adapters.

Ожидаемый результат:
- `how_kilocode_works` перестает выглядеть как частный случай доменного asset и становится частью общей adapter/reference model.

### Workstream 4. Довести `agent-role` pack model до explicit состояния

Нужно формализовать:

- abstract core role artifact;
- adapter-specific role artifact;
- relationship между ними;
- связь с runtime materialization;
- minimal canonical pack structure для role unit.

Нужно явно подтвердить, что структура вида:

```text
agent_roles/
  critic/
    role.md
    kilo/
      role.md
```

совместима с:

- `docs/methodology-layer/artifact-model.md`;
- `docs/methodology-layer/workflow-and-roles.md`;
- `docs/methodology-layer/interfaces-and-storage.md`;
- `docs/adr/0002-separate-artifacts-for-agent-role-and-kilocode-projection.md`.

Ожидаемый результат:
- role pack model становится не только имплицитно поддерживаемой, но и явно описанной в каноническом контуре.

### Workstream 5. Догнать glossary до уже принятой архитектуры

Нужно оценить и при необходимости добавить term pages или entries для:

- `role pack`;
- `adapter projection`;
- `primary_agent_system`;
- `Catalog Source of Truth`;
- возможно `composition manifest` и related governance terms.

Особенно важно убрать разрыв, когда focused specs уже используют понятие, а glossary еще не дает короткой канонической точки входа.

Ожидаемый результат:
- `docs/terms/` снова становится опережающей или хотя бы не отстающей точкой входа для человека и агента.

### Workstream 6. Подготовить governance skills как reusable augmentation

После фиксации governance policy можно спроектировать global reusable skills:

- `sot-layer-router`;
- `sot-consistency-check`;
- `sot-promotion-planner`;
- `sot-composition-review`.

Важно:

- сами policy documents должны жить в каноническом SoT;
- skills должны помогать применять policy, а не заменять ее.

Ожидаемый результат:
- layered SoT governance становится не только documented, но и operationally assisted.

## Предлагаемый порядок выполнения

1. Зафиксировать `ownership matrix`.
2. Зафиксировать `promotion protocol`.
3. Зафиксировать `composition manifest` как concept/spec.
4. Нормализовать taxonomy reusable packs.
5. Перенести references в модель `assets/references/<agent-system>/`.
6. Явно закрепить target structure для `agent_roles/<role>/role.md` и `agent_roles/<role>/<agent-system>/role.md`.
7. Обновить `docs/terms/`, чтобы glossary покрывал уже принятые понятия.
8. После стабилизации policy спроектировать governance skills.

## Что пока не нужно делать преждевременно

- не дробить каждый `agent-role` в отдельный repository до появления реальной operational необходимости;
- не выделять каждый rich `workflow-step` в отдельный skill до стабилизации reusable pattern;
- не смешивать abstract role semantics и Kilo-specific rendered fields в одном canonical artifact;
- не считать runtime materialization самостоятельным SoT.

## Риски

- governance policy может начать дублироваться между HyperGraph docs и methodology packs;
- glossary может снова отстать от focused specs;
- naming для packs и representations может остаться полуслучайным;
- если adapter-specific улучшения не промоутить осознанно, появится drift между abstract artifacts и concrete system representations.

## Следующий практический шаг

После утверждения этого плана начать с малого, но канонического куска:

1. выбрать документ или набор документов для `ownership matrix`, `promotion protocol` и `composition manifest`;
2. затем зафиксировать naming и structure для `references` и `agent-role` packs;
3. после этого выполнить glossary sync.

## Ожидаемый результат

После выполнения этого плана HyperGraph получит более явную и согласованную модель:

- layered Source of Truth;
- reusable asset packs;
- adapter-specific projections;
- project-friendly runtime materialization;
- governance rules для accumulation и promotion новых знаний без semantic drift.

## Анализ

Прочитаны:

- `software-development-methodology/workflow.md`
- `software-development-methodology/resources/*`
- `stages/01-discovery-intent-framing/workflow.md`
- `stages/02-architecture-design/workflow.md`
- `stages/03-system-design/workflow.md`

Фокус: согласованность Early Design Convergence Loop между:

1. `01 Discovery & Intent Framing`
2. `02 Architecture Design`
3. `03 System Design`

---

## Ключевой вывод

Общая модель в целом логична: есть правильное разделение Product / System / Architecture concerns, explicit return behavior, evidence loops, SoT materialization и boundary rules.

Но Early Design Convergence Loop сейчас семантически не до конца замкнут. Главные проблемы:

1. Stage 01 одновременно является частью Early Design Convergence Loop и как будто входом “перед” ним.
2. Stage 01 не имеет полноценной re-entry модели из Stage 02/03, хотя top-level graph и boundary rules требуют bidirectional loop.
3. Product baseline materialization недостаточно определен по сравнению с Architecture/System materialization.
4. Stage 02 и Stage 03 имеют частично пересекающиеся зоны ответственности по runtime behavior, scenarios, failure paths, contracts, NFRs and data/state.
5. Не зафиксирован canonical first route после Discovery: идти в Architecture, System или выбирать динамически.
6. Direct route Stage 02/03 → Design Baseline Consolidation может выглядеть как готовность всей baseline, хотя фактически готова только stage-local contribution.

---

# Findings

## 1. Stage 01 противоречиво позиционирован: часть loop или pre-loop gate

### Где видно

Top-level workflow явно включает `01 Discovery & Intent Framing` внутрь Early Design Convergence Loop:

```text
Early Design Convergence Loop:
01 <-> 02 <-> 03
```

Но Stage 01 workflow говорит:

```text
prepares a handoff to the early design convergence loop
```

и happy path завершается:

```text
09 Intent readiness gate
-> Early design convergence loop
```

### Issue

Получается, что Stage 01 одновременно:

- является vertex внутри Early Design Convergence Loop;
- и является подготовительным workflow, который “передает” работу в Early Design Convergence Loop.

Это не просто wording issue. Это влияет на процессную модель:

- если Stage 01 внутри loop, то возвращение из Stage 02/03 в Discovery — нормальный loop transition;
- если Stage 01 только pre-loop intake, то возвращение в Discovery выглядит как возврат на pre-design stage, а не как полноценная часть design convergence.

### Почему это проблема

Агенту будет неясно, что означает “Proceed to early design convergence loop” после Stage 01:

- перейти в Stage 02?
- перейти в Stage 03?
- перейти в некий process state, внутри которого снова доступна Stage 01?
- считать Stage 01 завершенной и больше не возвращаться к ней?

### Рекомендация

Развести формулировки:

- либо Stage 01 является полноценной частью loop, тогда Stage 01 exit должен быть:  
  `Proceed to Stage 02 / Stage 03 / Design Convergence routing`, а не “to Early Design Convergence Loop”;
- либо выделить pre-loop `Discovery Intake` отдельно от loop-local `Product Design Refinement`, но это усложнит модель.

Лучше первый вариант: сохранить Stage 01 как часть loop и явно описать, что initial Stage 01 run открывает routing в Stage 02/03.

---

## 2. Stage 01 не имеет symmetrical re-entry contract из Stage 02/03

### Где видно

Top-level graph задает:

```text
01 <--> 02
01 <--> 03
02 <--> 03
```

Boundary resource тоже говорит, что Stage 02/03 возвращаются в Discovery/Product Design, когда неясны:

- product intent;
- actors;
- value;
- capabilities;
- responsibilities;
- usage scenarios;
- acceptance criteria;
- scope/non-goals.

Stage 02/03 workflow прямо поддерживают re-entry:

- `Stage 02` может быть entered/re-entered из Discovery или System Design на любой core step.
- `Stage 03` может быть entered/re-entered из Discovery или Architecture Design на любой core step.
- оба имеют `Lightweight context refresh`.

Stage 01 workflow, наоборот, описан как linear intake от raw idea/backlog note к readiness gate. В нем нет явной модели:

- входа из Architecture Design;
- входа из System Design;
- lightweight refresh;
- focused product clarification;
- обновления уже существующего discovery/product baseline;
- downstream reroute обратно в конкретный stage, который запросил clarification.

### Issue

Loop bidirectional на top-level, но Stage 01 локально не поддерживает bidirectional loop semantics.

### Почему это проблема

Если Architecture Design обнаруживает, что acceptance criteria меняют product outcome, он должен вернуть вопрос в Discovery. Но Stage 01 workflow не говорит, как именно обработать такой return:

- создавать новый discovery workspace?
- обновлять существующий?
- проходить все шаги заново?
- идти сразу в `03 Problem and actor framing`, `04 Scope`, `05 Candidate product intent` или `09 Gate`?
- кто получает handoff обратно — Stage 02 или Stage 03?

Без этого Stage 01 остается intake workflow, а не loop-capable Product Design workflow.

### Рекомендация

Добавить в Stage 01 workflow отдельный раздел:

```text
Re-entry from Architecture/System Design
```

С явными путями:

- `Architecture return -> affected product framing step -> uncertainty triage -> intent readiness gate -> return to Architecture/System routing`
- `System return -> affected product boundary/scope/capability step -> gate -> return to System/Architecture routing`

И добавить lightweight context refresh analogue для Stage 01.

---

## 3. Product baseline materialization слабее определен, чем Architecture/System baseline

### Где видно

Stage 02 имеет:

- `10 Architecture SoT Materialization`
- expected durable areas: `docs/architecture/`, `docs/contracts/`, `docs/adr/`

Stage 03 имеет:

- `10 System Design SoT Materialization`
- expected durable docs location, хотя location пока не frozen

Stage 01 говорит:

```text
Raw and candidate discovery materials live in operational_scope/.
Accepted product baseline may be promoted into docs/product/ after local freeze.
```

Но Stage 01 graph не содержит:

- Product SoT Materialization step;
- Product Baseline Review Gate;
- explicit local freeze vertex;
- route to `Specification / SoT Materialization`;
- route to `Design Baseline Consolidation`.

### Issue

Методология требует, что downstream work не должен полагаться на temporary discovery notes как hidden SoT. Но Stage 01 не фиксирует обязательную точку, где accepted product intent становится durable SoT.

Фраза `may be promoted` слабее, чем нужны downstream guarantees.

### Почему это проблема

Stage 02/03 используют product intent, actors, capabilities, acceptance criteria and scope как design input. Если они находятся только в `operational_scope/discovery/...`, то downstream design фактически опирается на temporary artifacts.

Это конфликтует с invariant:

```text
Implementation tasks must not rely on temporary plans as primary Source of Truth.
```

и с resource invariant:

```text
Не используй Discovery artifacts как final engineering SoT, если они не materialized into durable docs.
```

### Рекомендация

Сделать product baseline materialization явной частью Stage 01 или cross-stage consolidation contract.

Минимально:

- заменить `may be promoted` на более строгое правило;
- добавить route: `Intent readiness gate -> Product SoT Materialization / Specification Materialization`, если accepted product baseline нужен Stage 02/03 или Test Design;
- определить, может ли Stage 02/03 начинаться от operational discovery handoff или только от durable product baseline.

---

## 4. Не зафиксирован first routing после Discovery

### Где видно

Top-level loop fully connected:

```text
01 <--> 02
02 <--> 03
01 <--> 03
```

Stage 01 завершает:

```text
Proceed to early design convergence loop
```

Stage 02 может входить из Discovery/System.
Stage 03 может входить из Discovery/Architecture.

### Issue

После Stage 01 нет routing rule:

- сначала System Design, потому система и boundary должны предшествовать architecture?
- сначала Architecture Design, потому top-level numbering ставит Architecture как Stage 02?
- выбирать dynamically по uncertainty?
- можно идти параллельно в 02 и 03?

### Почему это проблема

В boundary resource System Design формулируется как:

```text
какой системой является продукт в своем окружении
```

Architecture Design:

```text
как система устроена внутри
```

Семантически Architecture часто зависит от хотя бы предварительного system boundary/context. Но numbering ставит Architecture Design перед System Design.

Stage 02 компенсирует это gate-ом: если system boundary unclear, return to System Design. Но без first-routing rule агент может начинать с Architecture даже тогда, когда system context отсутствует, и сразу попадать в return.

Это допустимо как iterative loop, но не оптимально и не явно.

### Рекомендация

Добавить routing policy после Stage 01:

Пример:

```text
After Intent Readiness Gate:
- enter System Design first when boundary, external actors, integrations or system behavior are unclear;
- enter Architecture Design first when product/system context is sufficient and main uncertainty is internal structure, technology, components or contracts;
- enter both iteratively when architecture/system concerns are mutually dependent;
- record chosen first design route and reason.
```

---

## 5. Stage 02 и Stage 03 пересекаются в runtime behavior / scenarios / failure paths

### Где видно

Stage 02 does:

- dynamic architecture;
- interaction scenarios;
- data flows;
- lifecycle/state transitions;
- failure paths;
- runtime behavior.

Stage 03 does:

- system-level scenarios and behavior;
- data/state ownership;
- runtime modes;
- operational constraints;
- integration surfaces;
- externally visible failures.

Boundary resource хорошо различает:

- System Design: externally visible behavior;
- Architecture Design: internal runtime flows.

Но Stage workflow wording местами шире, чем boundary resource.

### Issue

Если не читать boundary resource, Stage 02 может быть воспринят как владелец runtime behavior вообще, а Stage 03 — как владелец system behavior вообще. Пересечение особенно заметно в:

- failure behavior;
- runtime modes vs runtime flows;
- lifecycle/state transitions vs data/state ownership;
- integration surfaces vs contracts;
- NFR framing vs architecture drivers.

### Почему это проблема

Два stage могут независимо materialize overlapping content:

- Stage 03 фиксирует expected external failure behavior.
- Stage 02 фиксирует failure paths.
- Если связь не traceable, architecture может начать менять externally visible semantics.

Или:

- Stage 03 фиксирует data/state ownership на system level.
- Stage 02 проектирует data stores, persistence, consistency.
- Без явной dependency архитектура может принять persistence decision, который фактически меняет system-level ownership.

### Рекомендация

В Stage 02/03 workflow добавить короткие local boundary notes, прямо ссылающиеся на `early-design-stage-boundaries.md`.

Например для Stage 02:

```text
Runtime behavior here means internal/component/runtime realization of system-level behavior, not ownership of externally visible behavior.
```

Для Stage 03:

```text
System behavior here means externally visible/system-level behavior and constraints, not internal component flow design.
```

---

## 6. Direct Stage 02/03 → Design Baseline Consolidation может быть истолкован как whole-baseline readiness

### Где видно

Stage 02:

```text
11 Architecture Baseline Review Gate -> Design Baseline Consolidation
```

Stage 03:

```text
11 System Baseline Review Gate -> Design Baseline Consolidation
```

Top-level graph:

```text
Early Design Convergence Loop -> Design Baseline Consolidation
```

### Issue

Stage-local workflow говорит: contribution готова к consolidation. Но graph visually выглядит как stage напрямую запускает cross-stage baseline consolidation.

Если Stage 02 прошла review, это не значит, что product/system baseline готова. Если Stage 03 прошла review, это не значит, что architecture baseline готова.

### Почему это проблема

Агент может преждевременно перейти в Design Baseline Consolidation от одного stage, не убедившись, что остальные baseline slices существуют и materialized.

Возможно, сам Design Baseline Consolidation это проверит. Но в текущих Stage 02/03 workflow это не явно.

### Рекомендация

Переименовать semantic condition:

```text
Stage 02 architecture contribution ready for consolidation attempt
```

а не просто ready for consolidation.

И явно указать:

```text
Design Baseline Consolidation may return to any Early Design stage if product/system/architecture baseline is incomplete or contradictory.
```

---

# Open questions

## OQ1. Что является canonical product SoT после Stage 01?

Варианты:

1. `docs/product/`
2. `docs/specification/`
3. project-local selected area
4. `operational_scope/discovery/...` до Design Baseline Consolidation

Сейчас Stage 01 говорит `may be promoted`, но downstream stages требуют stable product input.

---

## OQ2. Может ли Stage 02 стартовать без Stage 03 baseline?

Если да, нужен explicit rule: Architecture может стартовать на provisional system assumptions и обязана вернуть в System Design при boundary gaps.

Если нет, top-level order `02 Architecture` перед `03 System` конфликтует с dependency direction.

---

## OQ3. Что означает “pass-with-warnings” в Stage 01 для downstream design?

Если warnings включают unresolved product uncertainty, то Stage 02/03 должны знать:

- какие warnings допустимы;
- какие являются blockers;
- кто owns их resolution;
- можно ли materialize architecture/system decisions поверх warned product baseline.

---

## OQ4. Где фиксируется cross-stage traceability между product capability → system behavior → architecture flow?

Graph traceability resource пока говорит, что identifier grammar open. Это нормально для draft, но для loop consistency важно хотя бы process-level ожидание:

- product capability maps to system scenario;
- system scenario maps to architecture runtime flow;
- acceptance criteria maps to test design later.

---

# Non-findings / что выглядит согласованным

## 1. Boundary resource хорошо разделяет Product / System / Architecture

`early-design-stage-boundaries.md` — сильный документ. Он правильно фиксирует:

- Product Design owns intent/value/scope/capabilities.
- System Design owns system boundary/external behavior/context.
- Architecture Design owns internal structure/contracts/flows/trade-offs.

Это главный стабилизирующий artifact для всей loop.

## 2. Return как normal workflow behavior согласован между документами

Top-level invariant:

```text
return is normal workflow behavior
unrecorded return is failure
```

совпадает с Stage 02/03 re-entry model и boundary resource return guidance.

## 3. Evidence workflow concept согласован

Все три stage допускают research/spike/deep research как external evidence loop. Это логично и не конфликтует с stage boundaries.

## 4. SoT как file-first rule выдержан на уровне намерения

Top-level и resources последовательно говорят:

- graph database is derived;
- docs are durable SoT;
- operational_scope is temporary execution layer.

Проблема не в принципе, а в том, что Stage 01 не имеет столь же строгого materialization механизма, как Stage 02/03.

---

# Итоговая оценка

Early Design Convergence Loop концептуально сильная, но сейчас не полностью process-complete.

Главная структурная доработка: привести Stage 01 к тому же loop-capable уровню, что Stage 02/03:

- re-entry из Architecture/System;
- focused clarification paths;
- explicit product baseline materialization;
- clear route after intent readiness;
- clear return-to-caller handoff.

После этого loop будет выглядеть как действительно согласованная convergence model, а не как Discovery intake плюс две взаимосвязанные design stages.
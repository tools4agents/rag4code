# Spike-to-Prototype Evolution Pattern

> Status: Draft  
> Scope: reusable pattern для итеративной разработки прототипов ПО через spike experiments, draft components и постепенное закрепление validated capabilities  
> Role: guidance для перехода от uncertainty-driven experiments к первому working prototype без premature framework design

## 1. Назначение паттерна

Этот pattern фиксирует методологию разработки сложного ПО, когда команда еще не знает все runtime constraints, component boundaries и contracts заранее.

Ключевая идея:

```text
spike proves capability
  -> draft component captures the proven path
  -> workerized/componentized spike validates the boundary
  -> execution hardening consolidates the prototype
  -> next capability repeats the loop
```

Pattern особенно полезен для framework-like systems, где нужно одновременно открыть:

- реальные runtime ограничения;
- границы компонентов;
- artifact contracts;
- deployment assumptions;
- конфигурационную модель;
- минимальный набор reusable functionality.

## 2. Anti-pattern

Anti-pattern: сразу проектировать полный framework/component platform до empirical validation.

Типичные симптомы:

- команда заранее создает много components, packages and APIs без proof-of-use;
- spike scripts остаются одноразовыми и не влияют на architecture;
- все задачи называются implementation tasks, хотя они снимают unknowns;
- configs, component boundaries and runtime contracts проектируются speculative way;
- prototype формально существует, но не умеет пройти реальную end-to-end цепочку.

Почему это рискованно:

- component boundaries оказываются не там, где проходят реальные failure points;
- production-like packaging начинает мешать exploration;
- framework code закрепляет непроверенные assumptions;
- later redesign costs grow before the first useful capability is proven.

## 3. Pattern

Pattern: сначала сформировать примерный образ продукта/системы, затем построить spike plan для проверки этого образа с разных сторон, и после этого развивать прототип как серию capability loops.

В начале работы команда делает не полный детальный дизайн, а rough project image:

```text
Product image
  -> что это за продукт, для кого он нужен, какие core capabilities важны

Architecture image
  -> какие major components, boundaries, data/artifact flows ожидаются

System design image
  -> как примерно система запускается, конфигурируется, хранит state/artifacts, deploy-ится and observes failures
```

Этот образ не является final specification. Его задача — дать достаточно целостную гипотезу о системе, чтобы понять, какие assumptions нужно проверить первыми.

После этого формируется spike plan:

```text
rough project image
  -> architectural drivers and white spots
  -> spike experiment plan
  -> evidence-producing experiments
  -> draft components and prototype route
```

Spike plan должен быть направлен не на случайные probes, а на всестороннюю проверку образа проекта:

- viability ключевых product capabilities;
- correctness предполагаемых component boundaries;
- feasibility runtime/deployment path;
- достаточность config/artifact contracts;
- наличие observability/failure handling path;
- возможность постепенно собрать первый working prototype.

Иначе говоря, spike plan — это мост между preliminary Product / Architecture / System Design и разработкой первого прототипа ПО, описанного этим образом.

Каждая новая capability проходит четыре состояния:

```text
1. Spike task
   -> проверить гипотезу и собрать evidence.

2. Draft component / draft contract
   -> перенести validated path в компонентную форму.

3. Componentized spike
   -> проверить, что capability работает через новую boundary.

4. Hardening / consolidation task
   -> закрепить successful path в prototype baseline.
```

Это позволяет не выбирать между хаотичными experiments и преждевременной архитектурой. Spike остается источником evidence, а prototype постепенно накапливает только проверенные capabilities.

## 4. Recommended lifecycle

### 4.1 Capability framing

Перед spike нужно явно назвать capability, которую мы хотим доказать.

Примеры:

- saved responses can drive metrics without live model calls;
- local registry config can produce a concrete execution plan;
- worker can run on remote GPU node from copied repo;
- metric/report stages can rerun from immutable artifacts;
- component manager can resolve local path and Git source for the same component.

Важно: capability должна быть проверяемой, а не формулироваться как “реализовать framework”.

### 4.2 Spike experiment

Spike должен закрыть ближайший white spot минимальным runtime path.

Spike может использовать temporary scripts, manual steps or rough adapters, если он:

- производит evidence artifacts;
- отвечает на explicit validation criteria;
- не маскирует failures;
- фиксирует constraints and gaps;
- сохраняет extraction notes для будущего componentization.

Для evidence-producing spikes применим [`spike-experiment-evidence-pattern.md`](./spike-experiment-evidence-pattern.md).

### 4.3 Extraction notes

После spike важно не только verdict, но и extraction notes.

Extraction notes фиксируют:

- какие responsibilities появились естественно;
- какие inputs/outputs стали стабильными;
- какие artifacts стали boundary artifacts;
- какие config fields реально использовались;
- какие runtime assumptions нельзя закреплять как framework invariant;
- какие scripts/functions можно переносить в component draft.

Без extraction notes spike легко превращается в одноразовый experiment, который не развивает prototype.

### 4.4 Draft component

Validated path переносится в draft component только после того, как spike дал `confirmed` или `go with constraints`.

Draft component не обязан быть production-ready. Его задача:

- материализовать discovered boundary;
- иметь runnable CLI or service boundary;
- принимать task/config descriptor;
- производить expected artifacts;
- быть versionable independently, если будущая архитектура предполагает независимые компоненты.

Например:

```text
temporary script
  -> draft worker repository
  -> CLI: run --task-descriptor <path>
  -> expected manifest artifacts
```

### 4.5 Componentized spike

После draft component нужен новый spike, который проверяет ту же capability уже через component boundary.

Это отдельная проверка, потому что successful script path не доказывает, что:

- component packaging корректен;
- config resolution достаточно explicit;
- component can be moved/copied/cloned;
- task descriptor boundary достаточна;
- output artifacts сохраняют contract under real invocation.

### 4.6 Hardening / prototype baseline

Если componentized spike успешен, проводится execution hardening task.

Hardening закрепляет:

- minimal stable CLI/API;
- artifact layout;
- config fields used by the component;
- validation checks;
- known constraints;
- regression smoke command;
- docs for component usage.

После hardening capability считается частью prototype baseline.

## 5. Task taxonomy внутри pattern

Pattern требует различать четыре вида работы.

### 5.0 Product / Architecture / System Design sketch

Используется перед spike plan, когда нужно сформировать rough project image.

Outcome:

- product goal and core capabilities;
- major actors and workflows;
- preliminary component model;
- expected data/artifact flows;
- key NFRs and operational assumptions;
- white spots and validation needs;
- spike experiment plan.

Этот sketch не должен становиться детальной speculative specification. Его задача — направить experiments and prototype route.

### 5.1 Spike task

Используется, когда есть meaningful unknown.

Outcome:

```text
confirmed | rejected | go with constraints
```

Outputs:

- evidence;
- summary;
- spike report;
- extraction notes, если spike может привести к componentization.

### 5.2 Execution task

Используется, когда path уже достаточно понятен.

Outcome:

- materialized component;
- updated config registry;
- hardened baseline;
- docs/contracts update.

### 5.3 Architecture/design task

Используется, когда нужно выбрать boundary, ownership, component layout or contract direction before implementation.

Outcome:

- decision and rationale;
- assumptions;
- unknowns;
- validation plan.

## 6. Component registry and local workspace

В framework-like systems components often become independently versioned units.

Pattern допускает раннюю локальную форму:

```text
project-root/
  registry/          # config/component registry, possibly nested repo
  orchestrator/      # control-plane component, possibly nested repo
  workers/...        # functional components, possibly nested repos
```

Важно различать:

- local workspace layout;
- Git/release boundaries;
- future component manager responsibilities.

На раннем этапе plain nested repos могут быть проще submodules. Позже component manager can take over:

```text
manual nested checkout
  -> registry references local paths / Git URLs
  -> component manager resolves versions and modes
```

## 7. Freeze policy

Freeze делается постепенно.

Можно freeze после spike:

- observed facts;
- validated constraints;
- artifact examples;
- decision to proceed with constraints.

Нельзя автоматически freeze:

- final schema;
- final packaging;
- production deployment path;
- API shape beyond what was exercised;
- performance/quality claims outside spike scope.

Можно freeze после hardening:

- prototype baseline behavior;
- minimal component contract;
- repeatable smoke command;
- current registry/component references;
- documented known limitations.

## 8. Example route

Framework prototype route может выглядеть так:

```text
S0. Rough Product / Architecture / System Design image
  -> form coherent hypothesis of the system and derive spike plan.

S1. Compatibility spikes
  -> prove model/runtime/data feasibility.

S2. Artifact-chain spike
  -> prove real end-to-end artifact semantics.

S3. Registry materialization
  -> create reusable JSON configs for the validated cell.

S4. Draft component repositories
  -> extract orchestrator and worker boundaries.

S5. Componentized smoke spike
  -> run the same chain through draft components.

S6. Rerun/reuse spike
  -> prove saved artifacts can drive downstream stages.

S7. Prototype hardening
  -> consolidate first reusable framework baseline.

S8. Scale by config changes
  -> replace model/dataset configs and expand sample size.
```

The point is not this exact numbering. The invariant is the learning loop:

```text
unknown -> spike -> evidence -> component draft -> componentized validation -> hardening -> next unknown
```

## 9. When to use this pattern

Use this pattern when:

- runtime behavior is uncertain;
- component boundaries are expected but not proven;
- real integration matters more than API elegance;
- the first useful prototype should emerge from working experiments;
- configuration and deployment model are part of the product uncertainty;
- future framework should be modular, but premature modularization is risky.

## 10. When not to use this pattern

Pattern may be unnecessary when:

- task is small and fully understood;
- product is a simple bounded library with stable requirements;
- component boundaries are already proven by existing architecture;
- implementation risk is low and no meaningful empirical uncertainty remains.

## 11. Relationship to other patterns

This pattern complements:

- [`spike-experiment-evidence-pattern.md`](./spike-experiment-evidence-pattern.md) — for evidence-producing spike design;
- [`human-orchestrated-sdlc-evolution-pattern.md`](./human-orchestrated-sdlc-evolution-pattern.md) — for gradual workflow formalization through real usage;
- [`reviewable-automation-pattern.md`](./reviewable-automation-pattern.md) — when component creation or registry updates need plan/review/apply/verify loops.

## 12. Canonical invariants

- Spike validates capability before component hardening.
- Draft component captures a proven path, not a speculative future.
- Componentized spike validates the boundary after extraction.
- Hardening turns successful componentized behavior into prototype baseline.
- Each loop should leave evidence, decisions and known constraints behind.
- Prototype grows by accumulating validated capabilities, not by implementing the full imagined framework upfront.
- New functionality should normally be checked experimentally before being закреплена как baseline behavior.

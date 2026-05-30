# Task: Consolidate HyperGraph design docs and context entry navigation

## Контекст

После фиксации первого durable Product/System/Architecture baseline для HyperGraph появились новые Source of Truth areas в `docs/`:

- [`docs/product/index.md`](../../docs/product/index.md);
- [`docs/system_design/index.md`](../../docs/system_design/index.md);
- [`docs/architecture/index.md`](../../docs/architecture/index.md).

Текущий project context entry layer был создан раньше и еще не полностью отражает эти новые design entry points.

Связанный reusable asset:

- [`Project Context Entry System`](../../docs/methodology-layer/assets/project-context-entry-system/index.md).

## Цель

Синхронизировать navigation entry points HyperGraph после появления нового durable SoT baseline по Product/System/Architecture, чтобы будущий агент быстро попадал в правильный слой контекста и не искал архитектурный baseline в operational artifacts.

## Scope

Включить обновление:

1. [`docs/index.md`](../../docs/index.md)
   - добавить `docs/product/`;
   - добавить `docs/system_design/`;
   - добавить `docs/architecture/`;
   - уточнить entry points по слоям.

2. [`AGENTS.md`](../../AGENTS.md)
   - оставить thin router artifact;
   - уточнить loading order с учетом новых SoT areas;
   - явно указать, что Product/System/Architecture baseline живет в `docs/`.

3. [`project/index.md`](../../project/index.md)
   - обновить порядок чтения, если нужно;
   - направить к [`project/entry-points.md`](../../project/entry-points.md) как detailed routing contract;
   - не превращать `project/` в architecture SoT.

4. [`project/entry-points.md`](../../project/entry-points.md)
   - привести loading route к новой структуре;
   - указать, что для design work agent должен идти в:
     - [`docs/product/index.md`](../../docs/product/index.md);
     - [`docs/system_design/index.md`](../../docs/system_design/index.md);
     - [`docs/architecture/index.md`](../../docs/architecture/index.md);
   - сохранить ownership model.

5. [`project/repository-map.md`](../../project/repository-map.md)
   - обновить documentation navigation;
   - добавить новые `docs/` areas;
   - проверить формулировки про `.kilo/` и legacy `.kilocode/`, чтобы они не вводили агента в заблуждение.

6. [`project/overview.md`](../../project/overview.md)
   - кратко обновить high-level concept, если текущий текст не отражает новый first-iteration framing;
   - зафиксировать, что первая итерация HyperGraph сфокусирована на Markdown file graph как первом слое engineering knowledge graph runtime.

7. [`operational_scope/task-map.md`](../task-map.md)
   - оценить, нужно ли превратить root task map в thin router на per-scope task maps;
   - если scope `HyperGraph First Iteration` растет, предложить структуру вроде `operational_scope/task-scopes/<scope>.md`;
   - не выполнять большую миграцию task-map без отдельного согласования, если она выходит за рамки navigation cleanup.

## Non-scope

Не включать:

- изменение содержания product/system/architecture docs;
- новые архитектурные решения;
- materialization других задач;
- implementation code;
- cleanup всего legacy context;
- rewrite reusable `Project Context Entry System` asset.
- полная миграция task-map в per-scope files без отдельного решения.

## Шаги реализации

- [ ] Прочитать current entry context: `AGENTS.md`, `project/index.md`, `project/entry-points.md`, `project/repository-map.md`, `project/overview.md`, `docs/index.md`.
- [ ] Сверить их с [`Project Context Entry System`](../../docs/methodology-layer/assets/project-context-entry-system/index.md).
- [ ] Обновить `docs/index.md` новыми Product/System/Architecture areas.
- [ ] Обновить `AGENTS.md` как thin router artifact.
- [ ] Обновить `project/entry-points.md` как detailed loading/ownership contract.
- [ ] Обновить `project/index.md`, `project/repository-map.md` и при необходимости `project/overview.md`.
- [ ] Оценить необходимость thin-router модели для `operational_scope/task-map.md` и зафиксировать recommendation.
- [ ] Проверить, что links and labels соответствуют documentation rules.
- [ ] Проверить, что `project/` не объявлен engineering Source of Truth.

## Definition of Done

- [ ] `docs/index.md` ссылается на `docs/product/`, `docs/system_design/` и `docs/architecture/`.
- [ ] `AGENTS.md` направляет агента в правильные entry points.
- [ ] `project/entry-points.md` отражает текущий loading route.
- [ ] `project/repository-map.md` показывает новые docs areas.
- [ ] `project/overview.md` не противоречит текущему product framing.
- [ ] Сохранено правило: `docs/` сильнее operational artifacts.
- [ ] `project/` не объявлен engineering SoT.
- [ ] Навигация поддерживает lazy loading: агент не обязан читать все подряд.
- [ ] Новые ссылки используют human-readable labels, а не raw paths as labels.
- [ ] Для `task-map.md` есть явная recommendation: оставить как есть, либо вынести scopes в отдельные task-scope maps отдельной задачей.

## Execution Status

- Current State: queued
- Next Step: Обновить entry point files и проверить navigation consistency.
- Blockers: none
- Verification: Read updated entry files and run git diff/status review for touched documentation files.

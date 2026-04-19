# Spike Experiment Evidence Pattern

> Status: Draft  
> Scope: reusable pattern для проектирования [`spike-experiment`](../../terms/project/terms/spike-experiment.md) с evidence-producing execution, deterministic analysis и compact verdict artifacts  
> Role: Source of Truth для decomposition `executor -> evidence artifacts -> analyzer -> summary -> spike report`

## 1. Назначение паттерна

Этот pattern фиксирует рекомендуемый способ проектировать [`spike-experiment`](../../terms/project/terms/spike-experiment.md), если spike включает некоторый исполняемый код, runtime probes, сетевые вызовы или другие наблюдения, которые лучше подтверждать через machine-readable evidence.

Под исполняемым кодом здесь понимается не только script, но и любой bounded executor, например:
- script;
- CLI executable;
- binary tool;
- Docker container;
- небольшой service-like probe runner;
- другой узкий automation unit, который производит artifacts для анализа.

Цель паттерна:
- не заставлять агента или человека вручную читать большой raw log без необходимости;
- проектировать не только сценарий эксперимента, но и сценарий проверки результатов;
- отделять raw evidence от краткого verdict;
- делать spike repeatable и reviewable.

## 2. Core idea паттерна

Хороший spike проектируется как две связанные части:

1. execution path, который проводит эксперимент и сохраняет raw evidence;
2. analysis path, который автоматически отвечает на исследовательские вопросы по этому evidence.

Базовая decomposition такая:

`executor -> evidence artifacts -> analyzer -> summary -> spike report`

## 3. Почему одного execution unit недостаточно

Один execution unit, который только делает probes и сохраняет большой raw log, полезен как raw evidence, но неудобен для повторяемого анализа.

Без analyzer layer возникают проблемы:
- агент вручную читает слишком большой лог;
- часть выводов остается неявной и держится на человеческой интерпретации;
- повторный прогон трудно сравнивать с предыдущим;
- acceptance questions task-file не превращаются в explicit checks.

## 4. Рекомендуемые артефакты паттерна

Для evidence-producing spike рекомендуется пять артефактов.

### 4.1 Executor code

Executor code:
- выполняет сценарий spike;
- производит evidence artifacts;
- не подменяет собой итоговый verdict.

Executor может materialize-иться как script, executable, containerized command или другой ограниченный runtime unit.

### 4.2 Evidence artifacts

Evidence artifacts:
- хранят достаточное evidence для ручной проверки;
- остаются sanitized;
- могут включать raw logs, extracted traces, snapshots, counters, dumps или другие machine-readable outputs;
- не обязаны быть удобными для чтения человеком целиком.

Типичный minimum case - это raw log, но pattern не ограничивается только логами.

### 4.3 Analyzer code

Analyzer code:
- читает evidence artifacts;
- считает deltas и extracted signals;
- отвечает на explicit research questions;
- выдает compact machine-readable result.

### 4.4 Summary artifact

`summary.json` или аналогичный compact artifact:
- фиксирует key observations;
- пригоден для grep, diff и machine comparison;
- служит промежуточным bridge между evidence artifacts и human-readable report.

### 4.5 Spike report

[`spike-report`](../../terms/project/terms/spike-report.md):
- кратко интерпретирует summary;
- фиксирует verdict;
- формулирует policy recommendation;
- ссылается на evidence artifacts и analyzer result, а не дублирует их полностью.

## 5. Рекомендуемый execution flow

### 5.1 Design questions first

До написания кода нужно явно выписать, на какие вопросы должен ответить spike.

Например:
- изменился ли budget;
- появился ли non-zero cost signal;
- виден ли positive control;
- совместимы ли headers и body fields;
- подтверждена ли гипотеза.

### 5.2 Design observability together with execution

Сценарий probes и схема evidence capture должны проектироваться вместе.

Если spike делает 10 шагов, то еще до запуска должно быть понятно:
- какие поля надо извлечь из каждого шага;
- какие шаги являются baseline, probe, control и readback;
- какие deltas должен посчитать analyzer.

### 5.3 Prefer deterministic checks over manual reading

Если вопрос можно надежно проверить кодом, его нужно проверять кодом, а не оставлять на ручной разбор большого raw log.

## 6. Рекомендуемая структура evidence artifacts

Если основным evidence artifact является step-by-step trace, каждый step желательно делать self-describing.

Минимальный baseline:
- `step_id`
- `step_kind`
- `phase`
- `started_at`
- `finished_at`
- `request`
- `response_status`
- `headers_of_interest`
- `body_fields_of_interest`
- `notes` или `assertion_context` при необходимости

Хорошие примеры `step_kind`:
- `baseline.singleton`
- `probe.rate_limit.01`
- `probe.rate_limit.02`
- `control.list_filter`
- `readback.rate_limit`

## 7. Что должен считать analyzer

Analyzer должен работать не как second executor, а как deterministic interpreter of already collected evidence.

Минимальные обязанности analyzer:
- вычислить deltas между baseline и readback;
- проверить, сработал ли positive control;
- зафиксировать, какие signals были в headers, а какие только в body;
- собрать прямые ответы на research questions task-file;
- определить итоговый status: `confirmed`, `rejected` или `go-with-constraints`.

## 8. Рекомендуемая структура summary

Summary artifact должен быть compact и explicit.

Типичный shape:

```json
{
  "hypothesis_status": "confirmed",
  "questions": {
    "budget_changed_after_probe": false,
    "positive_control_detected": true,
    "headers_present": false,
    "body_signal_present": true
  },
  "observed_deltas": {
    "daily_used_usd": 0.0,
    "daily_remaining_usd": 0.0,
    "credits_used": 0
  },
  "policy_recommendation": "allowed_selective_reconciliation"
}
```

Идея не в конкретной schema, а в том, что summary должен давать короткий ответ на каждую исследовательскую гипотезу.

## 9. Где pattern особенно полезен

Этот pattern особенно полезен для spikes, которые проверяют:
- billing behavior external API;
- runtime headers и protocol compatibility;
- retries, cooldown, rate-limit или quota semantics;
- behavior library/tool under controlled probe sequence;
- observability claims, которые нельзя надежно закрыть только чтением docs.

## 10. Когда pattern не нужен

Pattern не обязателен для spikes, которые:
- состоят только из чтения документации;
- не требуют runtime evidence;
- слишком малы и закрываются одним-двумя прозрачными шагами без meaningful log analysis.

## 11. Связь с другими документами

Этот pattern связан с:
- [`spike-experiment`](../../terms/project/terms/spike-experiment.md) как activity;
- [`spike-report`](../../terms/project/terms/spike-report.md) как artifact результата;
- [`reviewable-automation-pattern.md`](./reviewable-automation-pattern.md), если executor/analyzer flow требует reviewable automation boundary.

## 12. Canonical invariants

- evidence-producing spike должен проектироваться вместе со схемой проверки evidence, а не только со сценарием execution;
- raw log и verdict не должны смешиваться в один artifact;
- analyzer должен отвечать на research questions deterministic way, если это practically возможно;
- summary должен быть компактным и пригодным для повторного сравнения между запусками;
- [`spike-report`](../../terms/project/terms/spike-report.md) должен опираться на summary и evidence artifacts, а не заменять их.

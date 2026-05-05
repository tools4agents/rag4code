# Methodology Patterns Index

> Status: Draft  
> Scope: индекс reusable design patterns для слоя `Project Methodology Runtime`  
> Role: entry point в pattern-level guidance, которая может переиспользоваться при проектировании новых assets, skills и agent-assisted workflows

## Назначение

Этот каталог хранит patterns, которые:
- не являются concrete assets сами по себе;
- не вводят новый asset type автоматически;
- фиксируют полезные reusable ideas для проектирования assets, tools, skills и documentation workflows.

Patterns нужны, чтобы:
- не терять удачные agent-assisted решения;
- повторно использовать успешные interaction models;
- отделять reusable design idea от конкретного asset или реализации.

## Когда pattern достоин отдельного документа

Pattern стоит фиксировать здесь, если он:
- уже оказался полезным хотя бы в одном реальном сценарии;
- выглядит reusable для других assets или skills;
- описывает interaction model, review loop, safety boundary или packaging idea;
- еще не является отдельным asset type и не требует расширения taxonomy.

## Текущие patterns

- [`human-orchestrated-sdlc-evolution-pattern.md`](human-orchestrated-sdlc-evolution-pattern.md) — постепенное развитие SDLC для code agents через practical human orchestration, real project usage and delayed formalization
- [`reviewable-automation-pattern.md`](reviewable-automation-pattern.md) — collaboration loop между ИИ-агентом и deterministic algorithm/tool по схеме `plan -> review -> apply -> verify`
- [`spike-experiment-evidence-pattern.md`](spike-experiment-evidence-pattern.md) — decomposition `executor -> evidence artifacts -> analyzer -> summary -> spike report` для repeatable evidence-producing spike experiments

## Границы

Этот каталог не должен:
- дублировать `principles.md`;
- заменять focused specs;
- превращаться в хранилище случайных заметок;
- преждевременно вводить новые asset types без необходимости.

Если позже patterns themselves станут большим и устойчивым subsystem, тогда можно обсуждать отдельный taxonomy-level layer. Пока это pattern library внутри `docs/methodology-layer/`.

# Human-Orchestrated SDLC Evolution Pattern

> Status: Draft  
> Scope: reusable pattern для постепенного проектирования SDLC для code agents  
> Role: guidance по переходу от practical human-orchestrated SDLC draft к более формализованной агентной методологии

## 1. Назначение паттерна

Этот pattern фиксирует подход к созданию SDLC для работы с code agents, когда полная автономная orchestration model еще не известна из практики.

Ключевая идея: сначала сделать гибкий human-orchestrated SDLC draft, применить его на реальных проектах, а затем постепенно формализовать то, что действительно повторяется and proves useful.

## 2. Anti-pattern

Anti-pattern: пытаться сразу спроектировать строгую формальную SDLC-систему для code agents с высокой степенью автономности.

Почему это рискованно:

- сложно заранее формализовать все реальные transitions между stages and steps;
- strict handoff schemas могут оказаться преждевременными и мешать работе;
- попытка описать full graph заранее расходует время, нужное на реальные проекты;
- speculative formalism быстро устаревает при столкновении с practical agent behavior.

## 3. Pattern

Pattern: проектировать SDLC как practical set of development stages with approximate steps, then evolve it through real usage.

На первом этапе достаточно:

- определить stages разработки;
- дать каждому stage понятную цель and boundary;
- описать примерный happy path;
- создать bounded `STEP.md` documents для фокусировки агентов;
- описывать expected inputs/outputs high-level, без строгих schemas;
- оставить orchestration человеку.

Человек выбирает порядок шагов, возвраты, глубину проработки, агента and handoff style. Workflow graph в этом режиме не является заранее frozen artifact.

## 4. Почему не фиксировать полный graph сразу

В реальной работе transitions будут возникать естественно:

```text
project work
  -> repeated human orchestration
  -> observed returns between steps and stages
  -> repeated useful paths
  -> documented patterns
  -> gradual formalization
```

То, что часто повторяется and proves useful, можно позже превратить в:

- explicit route rule;
- gate-like step;
- stable handoff expectation;
- reusable workflow resource;
- stricter artifact template;
- eventually formal graph edge.

То, что оказалось rare, ambiguous or project-specific, лучше оставить human-orchestrated.

## 5. STEP.md как practical focus boundary

`STEP.md` в этом pattern нужен не для строгой automation, а для ограничения фокуса агента.

Хороший draft `STEP.md` помогает агенту понять:

- какой локальный вопрос решается на этом шаге;
- какой контекст примерно читать;
- какие результаты примерно нужны человеку;
- что step не должен решать;
- какие unknowns or next-route suggestions вернуть.

Он не обязан задавать exact file paths, headings, tables, schemas or machine-readable handoff format.

## 6. Evolution loop

Развитие SDLC происходит как learning loop:

```text
draft SDLC
  -> use on real projects
  -> capture useful findings
  -> update steps/resources
  -> stabilize repeated paths
  -> formalize only proven structure
```

Так SDLC аккумулирует опыт работы над проектами, а не пытается заменить этот опыт speculative design upfront.

## 7. Когда формализовать сильнее

Усиление формализации уместно, когда:

- один и тот же transition повторяется в нескольких проектах;
- agents consistently misunderstand a step without stricter guidance;
- handoff loss creates real rework;
- gate decision needs observable rationale;
- artifact shape becomes stable and useful;
- human orchestration repeatedly follows the same route.

До этого момента lightweight description is preferable.

## 8. Invariants

- Практическое применение важнее преждевременной полноты.
- Human orchestration является valid runtime model, not failure of automation.
- Happy path можно фиксировать раньше, чем full transition graph.
- Formalization should follow observed workflow behavior.
- SDLC draft должен быть usable now and evolvable later.
- В пределе SDLC может стать более формальным, но не обязан быть fully formal from day one.

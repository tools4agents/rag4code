# Prompt Steering for Step Vacancies

> Status: Draft  
> Scope: adjacent resource for [`step-vacancy`](../../step-vacancy.md)  
> Role: объяснение prompt-steering техники для выбора и проектирования agent roles

## Назначение

Этот resource объясняет, почему `step-vacancy` описывает не только название роли, но и prompt-steering requirements.

Он нужен, чтобы люди и агенты понимали: роль в agent-assisted workflow — это не декоративный label, а способ направить модель в нужный режим внимания и рассуждения.

## Что такое prompt steering

`Prompt steering` — это управление поведением LLM через инструкции, роль, фокус задачи, ограничения и expected output.

Практически это означает:

- активировать нужный тип мышления;
- сузить внимание модели до релевантной области;
- подавить неподходящие паттерны поведения;
- задать критерии качества ответа;
- зафиксировать, чего агент не должен делать.

Например:

- `Critic` steering заставляет модель искать contradictions, gaps and hidden assumptions.
- `Researcher` steering заставляет модель искать evidence and sources, а не отвечать по памяти.
- `Developer` steering заставляет модель думать через code changes, tests and verification.
- `Reviewer / Gatekeeper` steering заставляет модель проверять criteria, verdicts and routing decisions.

## Почему это сильнее простого названия роли

Фраза `ты senior engineer` задает общий стиль, но не всегда достаточно меняет фокус внимания. Агент скорее будет играть эту роль как актер.

А нам нужен конкретный task focus:

```text
найди semantic gaps и unresolved assumptions
```

или:

```text
проверь readiness criteria и зафиксируй verdict/rationale
```

Мы как фильтр, который отфильтровывает из белого света нужные цвета.

Поэтому `step-vacancy` должен описывать не только suitable role, но и:

- required thinking mode;
- required capabilities;
- required tools/skills;
- expected output discipline;
- negative steering.

## Positive steering

Positive steering говорит агенту, как именно думать.

Примеры:

- use architectural trade-off reasoning;
- reconstruct product intent before proposing system design;
- verify traceability from requirement to test case;
- compare alternatives using evidence and constraints.

В `step-vacancy` это обычно отражается в секциях:

- `Required thinking mode`;
- `Required capabilities`;
- `Output discipline`.

## Negative steering

Negative steering говорит агенту, чего не делать.

Примеры:

- do not write production code;
- do not make final product decisions;
- do not silently resolve unknowns by guessing;
- do not treat operational notes as engineering SoT;
- do not execute research/spike when the step only sets a task.

В `step-vacancy` это отражается в секции `Negative steering`.

## Relationship to `agent-role`

`agent-role` — reusable specialist profile.

`step-vacancy` — конкретная позиция внутри конкретного workflow-step.

Prompt-steering requirements в `step-vacancy` помогают решить:

- подходит ли existing `agent-role`;
- может ли generic role выполнить step;
- нужно ли создать новую reusable role;
- какие skills/tools должны быть доступны исполнителю.

## Практическое правило

Не создавай новую `agent-role` только потому, что появилась новая задача.

Сначала опиши `step-vacancy`:

```text
workflow-step -> vacancy.md -> required steering -> existing role coverage -> role gap
```

Новая reusable role нужна, когда несколько vacancies требуют устойчивого отдельного режима мышления, tools или constraints.

## Boundary

Этот resource объясняет технику prompt steering для methodology docs.

Он не является научным обзором prompt engineering и не требует доступа к внешним заметкам или Obsidian vault.

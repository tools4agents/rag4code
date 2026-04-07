# Reviewable Automation Pattern

> Status: Draft  
> Scope: reusable pattern для совместной работы ИИ-агента и deterministic algorithm/tool при semi-automatic refactor, migration и cleanup задачах  
> Role: Source of Truth для collaboration loop `plan -> review -> apply -> verify`

## 1. Назначение паттерна

Этот pattern фиксирует reusable interaction model между:
- ИИ-агентом, который умеет мыслить, анализировать, интерпретировать policy и корректировать намерение;
- deterministic algorithm/tool, который умеет быстро, точно, повторяемо и массово выполнять ограниченный класс операций.

Под `algorithm/tool` здесь понимается любой deterministic исполнитель, например:
- script;
- CLI utility;
- binary executable;
- другой узкий automation tool.

Цель паттерна - дать агенту инструмент, в котором агент и алгоритм усиливают сильные стороны друг друга, а не дублируют работу.

## 2. Какие сильные стороны объединяются

### 2.1 Сильные стороны deterministic algorithm/tool

Алгоритм хорошо выполняет:
- точный parsing и extraction;
- повторяемую обработку больших объемов;
- стабильные mechanical transformations;
- детерминированный apply и валидацию формата;
- быстрый массовый проход без когнитивной нагрузки.

### 2.2 Сильные стороны ИИ-агента

Агент хорошо выполняет:
- semantic interpretation policy;
- анализ неоднозначных случаев;
- корректировку предложенного плана;
- различение safe case и risky case;
- решение, когда нужно позвать человека.

## 3. Core idea паттерна

Главная идея такая:
- агент не тратит интеллект на рутинный parsing и repetitive edits;
- алгоритм не притворяется semantic reasoner там, где нужен judgment;
- агент управляет deterministic tool через reviewable loop.

Вместо fully automatic execution используется collaboration pattern:

`plan -> review -> apply -> verify`

## 4. Базовый collaboration loop

### 4.1 `plan`

Агент запускает алгоритм в режиме planning.

Алгоритм должен:
- просканировать scope;
- построить список proposed actions;
- сохранить результат в reviewable report;
- не применять изменения автоматически на этом шаге.

### 4.2 `review`

Агент читает report и проверяет план алгоритма.

На этом шаге агент должен:
- отделить safe proposals от questionable proposals;
- исправить `Proposed`, если алгоритм ошибся semantic intent;
- явно пометить, что approved, что skipped, а что unresolved;
- позвать человека, если случай не удается надежно решить по policy.

### 4.3 `apply`

Агент запускает алгоритм в apply mode.

Алгоритм должен:
- применять только явно approved actions;
- использовать safe anchors для replace/apply;
- не применять unresolved или ambiguous items молча;
- возвращать conflicts вместо silent corruption.

### 4.4 `verify`

После apply агент повторно запускает planning/audit step и анализирует остаток.

Задача verify step:
- проверить, что approved changes реально materialized;
- убедиться, что остались только сознательно пропущенные или genuinely difficult cases;
- обнаружить conflicts и частично примененные сценарии.

## 5. Reviewable report как ключевой интерфейс

Центральный артефакт паттерна - reviewable report.

Именно report создает explainable boundary между агентом и алгоритмом.

Хороший report должен:
- быть человеко-читаемым;
- быть агенту удобным для редактирования;
- быть parser-friendly для apply tool;
- храниться как временный артефакт внутри проекта;
- поддерживать explicit review statuses.

## 6. Рекомендуемые status markers

Для reviewable reports рекомендуется такой baseline:
- `[ ]` — pending review;
- `[x]` — approved as proposed;
- `[~]` — proposal был исправлен агентом и затем approved;
- `[-]` — skip or reject.

Следствие:
- apply step должен обрабатывать только `[x]` и `[~]`;
- `[ ]` и `[-]` не должны применяться автоматически.

## 7. Рекомендуемая структура report item

Каждый item в report должен по возможности содержать:
- stable item id;
- file path;
- line number как preferred anchor;
- kind/reason;
- current snippet;
- proposed snippet.

Почему это важно:
- line number помогает быстро найти место глазами;
- `current snippet` нужен как semantic-safe apply anchor;
- `proposed snippet` позволяет агенту корректировать намерение алгоритма без ручного поиска в исходном файле.

## 8. Apply safety model

Чтобы pattern был безопасным, apply step должен быть intentionally conservative.

Базовые правила:
- сначала пытаться применить change по expected line/location;
- затем использовать fallback только если `current snippet` найден ровно один раз;
- если snippet не найден или найден неоднозначно, вернуть conflict;
- не делать silent best-effort apply для ambiguous cases.

## 9. Где хранить временные reports

Временные reports рекомендуется сохранять в `tmp/` внутри project root.

Это дает несколько преимуществ:
- report виден разработчику и агенту внутри проекта;
- артефакт легко открыть и проверить;
- такие файлы удобно удалять после завершения работы;
- каталог можно централизованно игнорировать через `.gitignore`.

## 10. Когда звать человека

Pattern должен явно признавать, что не все случаи можно надежно решить агентом и алгоритмом без human escalation.

Человека нужно звать, если:
- policy допускает несколько правдоподобных трактовок;
- proposed action меняет смысл текста, а не только форму;
- apply conflict указывает на drift, который уже нельзя безопасно интерпретировать автоматически;
- агент не может обосновать корректность правки по каноническим документам.

## 11. Где pattern особенно полезен

Этот pattern хорошо подходит для задач вроде:
- documentation cleanup;
- bulk refactor по локальному policy;
- migration assistant flows;
- structured renaming с human review;
- mass normalization tasks, где parsing cheap, а judgment expensive.

## 12. Что pattern не должен подменять

Этот pattern не должен использоваться как оправдание для:
- unsafe auto-fix без review step;
- скрытого применения правок без explicit approval;
- замены focused specification на script behavior;
- решения genuinely architectural ambiguities без human review.

## 13. Связь с принципами слоя

Этот pattern напрямую опирается на [`principles.md`](../principles.md), прежде всего на:
- удобство для человека и агента;
- `lazy loading` и `progressive disclosure`;
- `File-first Source of Truth`;
- `explicit over implicit`;
- `Separate artifacts вместо скрытого смешения`.

Он также согласуется с общей установкой проектировать reusable and explainable collaboration patterns вместо скрытой магии.

## 14. Concrete example

Первый concrete пример этого pattern в HyperGraph:
- skill `markdown-link-label-refactor`;
- planner script строит reviewable report;
- агент утверждает или редактирует proposals;
- apply script применяет только approved items;
- report по умолчанию хранится в `tmp/` внутри project root.

## 15. Почему это пока pattern, а не asset type

На текущем этапе это reusable pattern, а не отдельный asset type.

Причины:
- pattern описывает interaction model, а не самостоятельную систему хранения или taxonomy class;
- он может использоваться внутри разных skills и tools;
- пока важнее закрепить идею и boundary, чем вводить новую taxonomy category.

Если позже появится устойчивое семейство таких agent-assisted automation systems, тогда можно отдельно обсуждать более формальный subsystem layer.

## 16. Canonical invariants

- deterministic algorithm/tool и ИИ-агент должны усиливать разные сильные стороны, а не дублировать работу.
- базовый collaboration loop для этого pattern - `plan -> review -> apply -> verify`.
- report является главным reviewable boundary между агентом и алгоритмом.
- apply step не должен молча применять unresolved или ambiguous cases.
- временные reports рекомендуется хранить в `tmp/` внутри project root.
- genuinely difficult cases должны эскалироваться человеку.

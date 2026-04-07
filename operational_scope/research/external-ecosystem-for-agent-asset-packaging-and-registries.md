# Research Note: External ecosystem for agent asset packaging and registries

## Назначение

Этот research artifact нужен как безопасное место для external ecosystem hypotheses, извлеченных из [`agents_opportunities.md`](../discussion/agents_opportunities.md), но еще не подтвержденных как надежный engineering baseline.

Он не является каноническим SoT и не должен использоваться как доказанная архитектурная спецификация.

## Почему нужен отдельный research artifact

В discussion встречаются:
- vendor-specific claims;
- analogies к внешним marketplace и registry ecosystems;
- предположения про publish flows сторонних платформ;
- идеи, которые полезны как направление исследования, но опасны как уже установленный факт.

Чтобы не потерять потенциально полезный сигнал и одновременно не протащить непроверенные утверждения в канон, их лучше вынести в отдельный research note.

## Какие external themes стоит проверить отдельно

### 1. Registry and marketplace analogies

Полезно проверить, какие external ecosystems реально существуют для:
- package registries;
- prompt / skill / agent asset sharing;
- MCP-compatible tool registries;
- publishable workflow libraries.

### 2. Release-backed distribution patterns

Полезно изучить, насколько распространен pattern:
- source in git;
- release artifact for install;
- registry indexing поверх release metadata.

### 3. Trust and moderation patterns

Полезно проверить, как внешние ecosystems решают:
- verified publishers;
- moderation queue;
- staged publication;
- revocation;
- install-time validation.

### 4. Multi-system adaptation patterns

Полезно посмотреть, как внешние systems оформляют:
- adapters;
- provider-specific variants;
- compatibility matrices;
- export vs materialization distinctions.

## Предварительные гипотезы из discussion

На текущем этапе полезно сохранить как hypotheses, а не как facts:
- release-backed storage может оказаться удобнее, чем registry-owned binary storage;
- ecosystem value может лежать больше в indexing and trust metadata, чем в хостинге файлов;
- publish/install UX сильно влияет на adoption reusable methodology assets;
- moderation and validation становятся обязательными, если ecosystem открывается third-party publishers.

## Что сознательно не нужно делать в этом файле

Этот документ не должен:
- утверждать точные vendor capabilities без верификации;
- подменять собой архитектурные docs [`overview.md`](../../docs/methodology-layer/overview.md) и related methodology-layer docs;
- фиксировать design decisions как будто они уже приняты;
- переносить в research идею `Prompt-as-a-Resource`, так как она уже исключена из текущего extraction scope.

## Следующие шаги для research pass

Когда появится время на отдельный внешний ресерч, полезно проверить:
1. какие open ecosystems реально пригодны как reference model;
2. какие registry patterns совместимы с file-first SoT и pack-oriented layout;
3. какие moderation patterns не ломают open sharing model;
4. какие части discussion были слишком vendor-colored и должны быть отброшены.

## Статус

Research note создан как quarantine zone для внешних аналогий и hypothesis-level наблюдений.
Он помогает не потерять возможные идеи до отдельной верификации, не включая их в канон преждевременно.

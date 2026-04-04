# Project Principles and Values

> Status: Draft  
> Scope: общие ценности и принципы проекта HyperGraph, которые проходят через все архитектурные слои  
> Role: проектный baseline для философии, открытых ценностей и общих принципов принятия решений

## 1. Назначение документа

У проекта нет классических business requirements в корпоративном смысле.

Вместо этого мы явно фиксируем философию и базовые принципы open source проекта, которыми руководствуемся при проектировании системы, документации, methodology artifacts, workflows и agent runtime layers.

Этот документ нужен, чтобы:
- отделить общие проектные ценности от архитектурных принципов отдельных слоев;
- дать человеку и агенту единый baseline, почему проект устроен именно так;
- использовать этот документ как общий reference для всех дальнейших архитектурных решений;
- поддерживать эволюцию проекта без потери исходной философии.

## 2. Общая философия проекта

HyperGraph проектируется как open source платформа для совместной разработки, обмена knowledge artifacts и координации работы людей и ИИ-агентов.

Нас интересует не только открытый код, но и открытая инженерная среда, где удобно:
- делиться workflow, roles, skills, rules, projections и другими assets;
- повторно использовать наработки между проектами;
- обсуждать архитектурные решения прозрачно;
- строить reusable methodology для команд человек + агент.


## 3. Базовые ценности проекта

### 3.1 Открытость

Мы стремимся к открытой `open source`-дружественной платформе, в которой разработчики могут делиться своими workflow, roles, skills, rules, projections и другими artifacts друг с другом.

Открытость для нас означает:
- открытые структуры artifacts;
- возможность переносить и публиковать reusable packs;
- отсутствие лишней скрытой магии;
- возможность учиться друг у друга и переиспользовать удачные решения;
- развитие проекта как платформы для обмена инженерными наработками.

Это напрямую соотносится с open source ценностями:
- transparency;
- collaboration;
- knowledge sharing;
- community-first.

Внешние опоры:
- [The Philosophy of Open Source](https://www.opensourcesociety.org/p/philosophy.html?utm_source=chatgpt.com)
- [About the Open Source Movement](https://www.opensourcesociety.org/p/about.html?utm_source=chatgpt.com)
- [Open Source Philosophy - Archania](https://www.archania.org/wiki/Open_Source_Philosophy?utm_source=chatgpt.com)

### 3.2 Понятность

Система должна быть понятной и человеку, и агенту.

Понятность означает:
- явные термины и четкие определения;
- предсказуемую структуру документации;
- отделение обзорного уровня от детального;
- понятные связи между workflow, roles, steps, projections и runtime artifacts;
- минимизацию скрытых допущений.

Это ближе всего к open source установкам:
- transparency;
- open design;
- open development;
- knowledge sharing.

Внешние опоры:
- [Our Philosophy: The Four Opens - OpenInfra Foundation](https://openinfra.org/four-opens/?utm_source=chatgpt.com)
- [Open Source Philosophy - Archania](https://www.archania.org/wiki/Open_Source_Philosophy?utm_source=chatgpt.com)

### 3.3 Гибкость

Архитектура не должна жестко прибивать проект к одной методологии, одному workflow, одной agent system или одному runtime.

Гибкость означает:
- возможность менять методологии;
- возможность менять workflow без пересборки core semantics;
- переиспользуемые `agent-role` и другие assets;
- возможность добавлять новые adapter projections;
- возможность эволюции через overlays, bindings, packs и новые process patterns.

Это соотносится с open source установками:
- freedom and control;
- decentralization;
- continuous improvement.

Внешние опоры:
- [The Philosophy of Open Source](https://www.opensourcesociety.org/p/philosophy.html?utm_source=chatgpt.com)
- [Our Philosophy: The Four Opens - OpenInfra Foundation](https://openinfra.org/four-opens/?utm_source=chatgpt.com)
- [OpenSource | Handbook](https://open-energy-transition.github.io/handbook/docs/Engineering/OpenSource/?utm_source=chatgpt.com)

### 3.4 Трассируемость

Любое важное решение, binding, projection и runtime behavior должно быть объяснимо.

Трассируемость означает:
- понятные связи между artifacts;
- возможность понять, почему активирована конкретная роль;
- возможность восстановить, как workflow связан с steps, vacancy и role;
- возможность понять, какой adapter projection materialized в проекте;
- пригодность системы для graph navigation и explainability.

Это соотносится прежде всего с:
- transparency;
- open development;
- community reviewability.

Внешние опоры:
- [About the Open Source Movement](https://www.opensourcesociety.org/p/about.html?utm_source=chatgpt.com)
- [Our Philosophy: The Four Opens - OpenInfra Foundation](https://openinfra.org/four-opens/?utm_source=chatgpt.com)

## 4. Почему это не копия open source principles один в один

Мы не просто переписываем общие принципы open source, а переинтерпретируем их под домен HyperGraph.

Поэтому:
- `открытость` у нас включает переносимые workflow, role packs и reusable methodology assets;
- `понятность` распространяется не только на код, но и на навигацию человека и агента по документации и runtime artifacts;
- `гибкость` означает не только свободу модификации, но и сменяемость methodology, roles и agent systems;
- `трассируемость` усиливается через graph navigation и explainability by design.

## 5. Производные общие принципы

Из этих ценностей следуют общие принципы проекта:
- documentation должна поддерживать `lazy loading` и `progressive disclosure`;
- reusable assets должны быть упаковываемыми и переносимыми;
- semantic layers должны быть разделены явно;
- project intent должен оставаться portable;
- runtime materialization не должна подменять Source of Truth;
- adapter-specific semantics не должна загрязнять core domain без явной причины;
- архитектурные решения должны оставаться объяснимыми и ссылочно-связанными.

## 6. Отношение к принципам отдельных слоев

Этот документ задает общепроектный baseline.

А отдельные слои системы должны иметь свои производные архитектурные принципы, которые раскрывают, как эти ценности реализуются в конкретном слое.

Для `Project Methodology Runtime` таким документом является [`docs/methodology-layer/principles.md`](docs/methodology-layer/principles.md).

Связь такая:
- [`docs/principles.md`](docs/principles.md) фиксирует проектные ценности и общие принципы;
- [`docs/methodology-layer/principles.md`](docs/methodology-layer/principles.md) фиксирует, как эти принципы реализуются именно в слое methodology runtime.

## 7. Как использовать этот документ

Этот документ нужно использовать как reference, когда мы:
- обсуждаем общую философию проекта;
- спорим о trade-offs между удобством, строгостью и переносимостью;
- формулируем архитектурные принципы конкретных слоев;
- проверяем, не противоречит ли новое решение базовым ценностям проекта.

Если документ слоя объясняет, как проектировать конкретный архитектурный слой, то этот документ объясняет, почему эти решения вообще для нас важны.

## 8. Статус

Этот документ должен рассматриваться как канонический baseline общих ценностей и принципов HyperGraph до появления более широкого manifesto или governance document для всего проекта.
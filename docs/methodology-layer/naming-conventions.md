# Naming Conventions for Project Methodology Runtime

> Status: Draft  
> Scope: канонические правила именования терминов, filesystem layout и Python-facing identifiers для слоя `Project Methodology Runtime`  
> Role: Source of Truth для naming conventions, чтобы не смешивать domain language, pack layout и implementation identifiers

## 1. Назначение документа

Этот документ фиксирует naming conventions для слоя `Project Methodology Runtime`.

Он нужен, чтобы:

- одинаково называть domain concepts в документации;
- одинаково именовать directories и files в reusable packs;
- согласованно отображать domain terms в Python code и schemas;
- не смешивать human-facing terms, filesystem names и implementation identifiers.

## 2. Почему нужен отдельный naming layer

В этом слое одни и те же сущности живут сразу в нескольких representation layers:

- как human-facing terms в документации;
- как paths в pack-oriented layout;
- как поля, enums, classes и identifiers в Python code;
- как runtime-facing names внутри конкретной `agent-system`.

Если не зафиксировать naming conventions явно, быстро возникает drift:

- термин в glossary называется одним образом;
- папка pack называется другим;
- Python model использует третью форму;
- runtime adapter добавляет четвертую.

## 3. Базовый принцип

Мы различаем три naming domains:

1. human-facing domain terms;
2. filesystem and pack layout names;
3. implementation identifiers.

У каждого naming domain своя canonical convention.

## 4. Human-facing terms

### 4.1 Основная форма

Для канонических терминов в `docs/terms/`, focused specs, ADR и narrative docs используется `kebab-case`.

Примеры:

- `agent-role`
- `workflow-step`
- `step-vacancy`
- `agent-system`
- `primary-agent-system`

### 4.2 Зачем это нужно

`Kebab-case` лучше подходит для human-facing domain language:

- читается как составной термин;
- хорошо выглядит в glossary и prose;
- не выглядит как Python variable или directory name;
- помогает отличать semantic term от implementation identifier.

### 4.3 Что относится к human-facing terms

`Kebab-case` используется для:

- glossary terms;
- названий domain concepts в prose;
- кратких canonical labels для concepts;
- human-readable artifact family names, если они приводятся как термины.

## 5. Filesystem и pack layout names

### 5.1 Основная форма

Для directories и filenames, которые являются частью pack layout или storage layout, используется `snake_case`.

Примеры:

- `agent_roles/`
- `agent_systems/`
- `role.md`
- `workflow_steps/`, если позже появится такой layout namespace
- `primary_agent_system` как field name в yaml или config-like files

### 5.2 Зачем это нужно

`Snake_case` лучше подходит для storage and code-adjacent layout:

- хорошо согласуется с Python ecosystem;
- удобен для directories, filenames и config keys;
- уменьшает разрыв между filesystem names и implementation identifiers;
- проще использовать в scripts, code generation и path resolution.

### 5.3 Pack-oriented пример

Для role packs принимаем такой canonical layout baseline:

```text
agent_roles/
  critic/
    role.md
    agent_systems/
      kilo/
        role.md
```

Здесь:

- `critic` — logical slug reusable role unit;
- `role.md` в корне role unit — abstract role artifact;
- `agent_systems/kilo/role.md` — `agent-system`-specific role asset.

## 6. Python-facing naming

### 6.1 Modules, packages, variables, functions

Для Python packages, modules, variables, functions и field-like identifiers используется `snake_case`.

Примеры:

- `agent_roles`
- `agent_systems`
- `primary_agent_system`
- `role_id`
- `artifact_type_id`

### 6.2 Classes and types

Для Python classes и type names используется `PascalCase`.

Примеры:

- `AgentRole`
- `WorkflowStep`
- `MethodologyArtifact`
- `MethodologyArtifactType`
- `AgentSystem`

### 6.3 Stable string values

Если в code or schema нужен stable string identifier для human-facing domain concept, предпочтительна `kebab-case` форма, если нет сильной причины сделать иначе.

Примеры:

- `agent-role`
- `workflow-step`
- `step-vacancy`

Если identifier используется как purely implementation-facing field или config key, допустим `snake_case`.

## 7. Mapping rule между терминами и implementation names

Для одной и той же сущности допускается controlled mapping между naming domains.

Примеры:

- term: `agent-role`
- directory: `agent_roles/`
- Python class: `AgentRole`
- Python field: `agent_role`
- string concept id: `agent-role`

- term: `agent-system`
- directory: `agent_systems/`
- Python class: `AgentSystem`
- Python field: `primary_agent_system`
- system folder: `agent_systems/kilo/`

Такой mapping не считается нарушением, если semantic meaning остается одинаковым.

## 8. Naming для agent-system model

Для model around `agent-system` принимаем следующие baseline conventions:

- human-facing term: `agent-system`
- filesystem namespace: `agent_systems/`
- Python class: `AgentSystem`
- project-level selector field: `primary_agent_system`
- related human-facing selector term: `primary-agent-system`
- related abstract asset class: `agent-system-agnostic asset`
- related concept: `agent-system-specific asset`
- runtime process term: `agent-system materialization`

Важно:

- `agent-system` — это term;
- `agent_systems/` — это layout namespace;
- `primary-agent-system` — это human-facing selector term;
- `primary_agent_system` — это field-like selector inside project intent;
- `primary-agent-system` используется для developer-specific active `agent-system` внутри project context;
- они не конкурируют друг с другом, а относятся к разным naming domains.

## 9. Что не нужно смешивать

Не нужно смешивать:

- glossary term и directory name;
- directory name и Python class;
- runtime-generated name и canonical domain term;
- human-readable pack family label и config field.

Если одно и то же слово должно жить в нескольких слоях, нужно выбирать форму по naming domain, а не пытаться насильно использовать один и тот же shape везде.

## 10. Canonical examples

### 10.1 Role semantics

- term: `agent-role`
- pack family directory: `agent_roles/`
- abstract role file: `agent_roles/critic/role.md`
- agent-system-specific role file: `agent_roles/critic/agent_systems/kilo/role.md`
- Python class: `AgentRole`

### 10.2 Workflow semantics

- term: `workflow-step`
- possible Python class: `WorkflowStep`
- possible field: `workflow_step_id`

### 10.3 Agent system semantics

- term: `agent-system`
- namespace directory: `agent_systems/`
- Python class: `AgentSystem`
- selector field: `primary_agent_system`

- term: `primary-agent-system`
- config field: `primary_agent_system`

## 11. Что этот документ не делает

Этот документ не должен:

- определять artifact model целиком;
- определять pack structure beyond naming baseline;
- определять process semantics `workflow`, `workflow-step`, `step-vacancy` и `agent-role`;
- определять runtime materialization policy;
- заменять собой glossary layer.

Он фиксирует только naming rules, которые должны использоваться согласованно в этих слоях.

## 12. Связь с другими каноническими документами

Этот документ нужно читать вместе с:

- `docs/methodology-layer/overview.md` как обзором слоя;
- `docs/methodology-layer/principles.md` как набором guiding principles;
- `docs/methodology-layer/artifact-model.md` как artifact-oriented spec;
- `docs/methodology-layer/workflow-and-roles.md` как process-level spec;
- `docs/methodology-layer/interfaces-and-storage.md` как storage and runtime boundary spec;
- `docs/terms/terms_map.md` и `docs/terms/project/terms_map.md` как glossary layer.

## 13. Canonical invariants

Для этого слоя считаются обязательными следующие invariants:

- human-facing terms используют `kebab-case`;
- filesystem names и Python-facing field/module names используют `snake_case`;
- Python classes используют `PascalCase`;
- один и тот же concept может иметь разные surface forms в разных naming domains;
- `agent-system` и `agent_systems/` являются согласованными, но не одинаковыми representation forms;
- naming conventions не должны размывать semantic boundaries между abstract artifact, `agent-system`-specific asset и runtime materialization.

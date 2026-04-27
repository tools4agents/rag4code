# Workflow and LangGraph Analogy

> Status: Draft  
> Scope: adjacent resource for [`workflow`](../../workflow.md)  
> Role: explanatory analogy for nested directed process graphs

## Назначение

Этот документ объясняет `workflow` через аналогию с LangGraph-like directed graphs.

Аналогия нужна, чтобы людям и агентам было проще понимать workflow не как линейную prose-инструкцию, а как graph-defined process contract.

## Core analogy

```text
workflow = markdown-defined directed graph for agent execution
```

В этой аналогии:

- `workflow.md` похож на declarative graph definition;
- `workflow-step` похож на executable node;
- nested `workflow` похож на subgraph;
- transition rule похож на graph edge condition;
- workflow-instance handoff похож на runtime state между node executions.

## Mapping

| Workflow concept | LangGraph-like analogy |
| --- | --- |
| `workflow` | directed graph definition of process |
| `workflow-step` | bounded executable node |
| nested `workflow` | subgraph / nested graph |
| `workflow-step-gate` | executable decision node with verdict and recorded rationale |
| transition label | edge condition or already-decided routing outcome |
| human interaction node | external input node |
| lifecycle marker | start/end marker |
| transition | graph edge |
| handoff artifact | runtime state passed between nodes |
| workflow-pack | source package for graph definition and support materials |
| workflow-exchange layer | operational runtime state for a concrete run |

## Why this analogy helps agents

The analogy helps agents avoid three common mistakes:

1. Treating the whole workflow as one giant instruction.
2. Treating a multi-step stage as one overloaded `workflow-step`.
3. Treating runtime handoff state as canonical workflow definition.

Instead, the agent should:

- read the parent workflow as graph navigation;
- enter nested workflows only when the current vertex requires it;
- execute bounded `workflow-step` units;
- write concrete run state to operational artifacts, not to the reusable workflow-pack.

## Nested graph rule

If a vertex requires its own internal graph, model it as nested `workflow`.

```text
workflow
  -> workflow-step
  -> nested workflow
      -> workflow-step
      -> workflow-step-gate
      -> optional nested workflow
```

Do not compress a multi-node subgraph into one `STEP.md` just because one agent might execute it in one session.

## Boundary of the analogy

This is an explanatory analogy, not a requirement to implement LangGraph.

`Workflow` remains markdown-first and file-first. Any runtime engine or graph database representation is derived from markdown source artifacts.

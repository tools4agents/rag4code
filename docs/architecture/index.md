# Architecture

> Status: Draft  
> Scope: architecture-level Source of Truth for HyperGraph  
> Role: navigation entry point for internal structure, components and architecture drivers

## Назначение

Этот раздел фиксирует architecture-level baseline HyperGraph: как система должна быть устроена внутри, чтобы реализовать product and system expectations.

Architecture Design опирается на [`Product Documentation`](../product/index.md) и [`System Design`](../system_design/index.md), но не переопределяет product scope или system ownership boundaries.

## Порядок чтения

1. [`core-and-adapters.md`](./core-and-adapters.md) — core, ports, adapters, CLI and MCP boundary.
2. [`storage-and-indexing.md`](./storage-and-indexing.md) — derived storage, indexing pipeline, parser boundary and storage capability requirements.

## Границы раздела

Этот раздел не фиксирует:
- final implementation task breakdown;
- concrete database schema;
- final storage backend decision;
- final parser library decision;
- product-level future capabilities as committed MVP scope.

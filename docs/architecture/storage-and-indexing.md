# Storage and Indexing

> Status: Draft  
> Scope: architecture baseline for derived storage and indexing in HyperGraph  
> Role: storage ownership, indexing pipeline, parser boundary and backend capability requirements

## Назначение

HyperGraph storage and indexing architecture must preserve the system invariant: project files are Source of Truth, and database is a rebuildable derived index.

This document describes architecture drivers and boundaries. It does not choose final storage backend or database schema.

## Storage ownership

[`project-database`](../terms/project/terms/project-database.md) is a derived database for one [`project`](../terms/project/terms/project.md).

Architecture implications:
- one project owns one isolated database;
- database is not shared between projects;
- database can be rebuilt from project files;
- storage adapter must not become authoritative owner of project content;
- storage corruption or loss should be recoverable through rebuild.

## Indexing pipeline

First-iteration indexing pipeline:

```text
project-root
  -> filesystem scan
  -> exclude filtering
  -> Markdown file discovery
  -> Markdown parsing / link extraction
  -> link resolution and path normalization
  -> graph/index update
  -> queryable project-database
```

The pipeline must respect [`project-config`](../terms/project/terms/project-config.md), including exclude rules and `.git` hard exclusion.

## Parser boundary

Markdown MVP needs Markdown parsing and link extraction, not Markdown LSP.

Parser/indexer architecture should provide:
- extraction of supported Markdown links;
- link source ranges or positions when available;
- raw link target preservation;
- normalized internal target path when resolution succeeds;
- explicit unresolved/external/unsupported status.

Parser library choice is an architecture decision for later validation. Markdown LSP is excluded from Markdown MVP architecture unless future evidence changes this boundary.

## Link resolution

Link resolution should produce project-relative canonical targets for supported internal links.

Resolution must distinguish:
- resolved internal Markdown links;
- unresolved links;
- external links;
- unsupported link syntax;
- ignored links under excluded paths.

Only resolved internal Markdown links create first-iteration `LINKS_TO` graph edges between Markdown files.

## Reindex and rebuild

Because database is derived, architecture must support explicit reindex/rebuild.

Required behavior:
- user can trigger reindex/rebuild through CLI;
- agent can trigger reindex/rebuild through MCP when exposed;
- rebuild restores graph/index state from current project files;
- after Git checkout or branch switch, user is responsible for manual rebuild.

Automatic Git transition detection is out of scope for first iteration.

## Storage capability requirements

Storage backend should support the product/system direction:
- typed vertices or equivalent node classification;
- typed edges or equivalent relation classification;
- traversal queries;
- filtering by tags, file type, semantic type and properties;
- project-local isolation;
- rebuildable state lifecycle.

These are capability requirements for architecture evaluation, not a product-level commitment to a specific database technology.

## Storage backend candidates

Graph-capable or multi-model database can be a strong architecture candidate because HyperGraph needs typed relations, traversal and filtering.

ArcadeDB remains a candidate implementation choice, not a product requirement.

Other backends may be evaluated if they satisfy first-iteration needs and future graph direction without unnecessary operational complexity.

## Mutating operations and consistency

Mutating operations must update filesystem and derived index consistently.

Architecture expectation:
- dry-run computes planned changes without writing files;
- apply mode writes explicitly approved file changes;
- storage is updated or rebuilt after filesystem mutation;
- unsupported or unsafe rewrites are skipped and reported;
- reports distinguish changed files, affected files, skipped links and unresolved cases.

Semantic text correction remains outside deterministic storage/indexing logic and belongs to human or AI agent workflows.

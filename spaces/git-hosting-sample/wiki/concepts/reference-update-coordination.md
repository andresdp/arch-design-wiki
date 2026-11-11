---
type: Design Decision
title: Reference update coordination
description: How concurrent updates to a repository's references are ordered and made atomic.
id: '3'
core: true
values: 3
candidate_values: 3
outcomes: 0
evidence:
  codes: 3
  documents: 7
  sources: 2
relations:
- requires Source of truth for repository state
tags:
- dimension
- core
exclusivity: 0.5
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Reference update coordination

How concurrent updates to a repository's references are ordered and made atomic.

## Values

| Value | Status | Passages |
|---|---|---|
| [Compare-and-swap on the log](/entities/compare-and-swap-on-the-log.md) | accepted | 2 |
| [One server serializes the updates](/entities/one-server-serializes-the-updates.md) | accepted | 1 |
| [Three-phase commit across replicas](/entities/three-phase-commit-across-replicas.md) | accepted | 4 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- This dimension requires [Source of truth for repository state](/concepts/source-of-truth-for-repository-state.md) to be decided first. *Updates are ordered by whatever holds the authoritative references.*


## Exclusivity

The values of a dimension are alternatives, so each source should adopt one of them. **1 of 2 sources** adopt one value (or a declared hybrid): exclusivity 0.50.

Values adopted together:

- [Three-phase commit across replicas](/entities/three-phase-commit-across-replicas.md) and [Compare-and-swap on the log](/entities/compare-and-swap-on-the-log.md): [s1](/sources/s1.md)
- [Three-phase commit across replicas](/entities/three-phase-commit-across-replicas.md) and [One server serializes the updates](/entities/one-server-serializes-the-updates.md): [s1](/sources/s1.md)
- [Compare-and-swap on the log](/entities/compare-and-swap-on-the-log.md) and [One server serializes the updates](/entities/one-server-serializes-the-updates.md): [s1](/sources/s1.md)

## Evidence

3 open codes from 7 passages in 2 sources.

**Core dimension:** yes ★ (2 sources; core = ≥ 2 sources).

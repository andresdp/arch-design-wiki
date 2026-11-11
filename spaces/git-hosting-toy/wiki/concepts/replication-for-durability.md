---
type: Design Decision
title: Replication for durability
description: How copies of a repository are kept so that a lost machine loses no data.
id: '2'
core: true
values: 4
candidate_values: 4
outcomes: 0
evidence:
  codes: 7
  documents: 14
  sources: 3
relations:
- requires Source of truth for repository state
- constrains Serving reads
tags:
- dimension
- core
exclusivity: 0.67
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Replication for durability

How copies of a repository are kept so that a lost machine loses no data.

## Values

| Value | Status | Passages |
|---|---|---|
| [Durability delegated to object storage](/entities/durability-delegated-to-object-storage.md) | accepted | 4 |
| [Single copy on a file server](/entities/single-copy-on-a-file-server.md) | accepted | 1 |
| [Three Git replicas with majority writes](/entities/three-git-replicas-with-majority-writes.md) | accepted | 8 |
| [Block-level filesystem replication](/entities/block-level-filesystem-replication.md) | rejected | 3 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- This dimension requires [Source of truth for repository state](/concepts/source-of-truth-for-repository-state.md) to be decided first. *What must be replicated, and where, follows from where the authoritative state lives.*
- Choices on this dimension limit the options available on [Serving reads](/concepts/serving-reads.md). *Serving from the nearest replica needs replicas; a single copy leaves one place to read from.*


## Exclusivity

The values of a dimension are alternatives, so each source should adopt one of them. **2 of 3 sources** adopt one value (or a declared hybrid): exclusivity 0.67.

Values adopted together:

- [Three Git replicas with majority writes](/entities/three-git-replicas-with-majority-writes.md) and [Durability delegated to object storage](/entities/durability-delegated-to-object-storage.md): [s1](/sources/s1.md)
- [Three Git replicas with majority writes](/entities/three-git-replicas-with-majority-writes.md) and [Single copy on a file server](/entities/single-copy-on-a-file-server.md): [s1](/sources/s1.md)
- [Durability delegated to object storage](/entities/durability-delegated-to-object-storage.md) and [Single copy on a file server](/entities/single-copy-on-a-file-server.md): [s1](/sources/s1.md)

## Evidence

7 open codes from 14 passages in 3 sources.

**Core dimension:** yes ★ (3 sources; core = ≥ 2 sources).

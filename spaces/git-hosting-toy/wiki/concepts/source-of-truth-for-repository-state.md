---
type: Design Decision
title: Source of truth for repository state
description: Where the authoritative copy of each repository's objects and references lives.
id: '1'
core: true
values: 4
candidate_values: 4
outcomes: 0
evidence:
  codes: 5
  documents: 13
  sources: 2
relations: []
tags:
- dimension
- core
exclusivity: 0.5
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Source of truth for repository state

Where the authoritative copy of each repository's objects and references lives.

## Values

| Value | Status | Passages |
|---|---|---|
| [Repository files on server disks](/entities/repository-files-on-server-disks.md) | accepted | 6 |
| [Write-ahead log in object storage](/entities/write-ahead-log-in-object-storage.md) | accepted | 6 |
| [Objects in a distributed hash table](/entities/objects-in-a-distributed-hash-table.md) | mixed | 2 |
| [Blobs plus a relational reference database](/entities/blobs-plus-a-relational-reference-database.md) | rejected | 1 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### To this dimension

- [Replication for durability](/concepts/replication-for-durability.md) requires this dimension to be decided first. *What must be replicated, and where, follows from where the authoritative state lives.*
- [Reference update coordination](/concepts/reference-update-coordination.md) requires this dimension to be decided first. *Updates are ordered by whatever holds the authoritative references.*

## Exclusivity

The values of a dimension are alternatives, so each source should adopt one of them. **1 of 2 sources** adopt one value (or a declared hybrid): exclusivity 0.50.

Values adopted together:

- [Repository files on server disks](/entities/repository-files-on-server-disks.md) and [Write-ahead log in object storage](/entities/write-ahead-log-in-object-storage.md): [s1](/sources/s1.md)
- [Repository files on server disks](/entities/repository-files-on-server-disks.md) and [Objects in a distributed hash table](/entities/objects-in-a-distributed-hash-table.md): [s1](/sources/s1.md)
- [Write-ahead log in object storage](/entities/write-ahead-log-in-object-storage.md) and [Objects in a distributed hash table](/entities/objects-in-a-distributed-hash-table.md): [s1](/sources/s1.md)

## Evidence

5 open codes from 13 passages in 2 sources.

**Core dimension:** yes ★ (2 sources; core = ≥ 2 sources).

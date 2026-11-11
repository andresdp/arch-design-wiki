---
type: Synthesis
title: Overview
tags:
- synthesis
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Overview

## Use case

Identify the design decisions practitioners face, the alternatives they consider for each, and the outcomes they report.

## Run

| Item | Value |
|---|---|
| Run | 20261109_000000 (selected view) |
| Dimensions | 5 |
| Values | 17: 13 accepted, 2 mixed, 2 rejected, 0 outcome |
| Sources | 5 |
| Iterations | 1 |
| Dropped dimensions | 0 |
| Generation LLM | `openai/gpt-5.6-luna` |
| Evaluation LLM (judge) | `openai/gpt-5.6-luna` |
| Embedding model | `openai/text-embedding-3-small` |

## Dimensions and values

Core dimensions (★) have evidence from ≥ 2 sources; they are listed first. Relations between dimensions are explained in [Relations between dimensions](/relations.md).

| Dimension | Core | Accepted | Mixed | Rejected | Outcomes |
|---|---|---|---|---|---|
| [Client data transfer](/concepts/client-data-transfer.md) | ★ | • [Full clone over the Git protocol](/entities/full-clone-over-the-git-protocol.md)<br>• [Partial clone with sparse checkout](/entities/partial-clone-with-sparse-checkout.md) | • [Virtualized filesystem with on-demand objects](/entities/virtualized-filesystem-with-on-demand-objects.md) |  |  |
| [Reference update coordination](/concepts/reference-update-coordination.md) | ★ | • [Three-phase commit across replicas](/entities/three-phase-commit-across-replicas.md)<br>• [Compare-and-swap on the log](/entities/compare-and-swap-on-the-log.md)<br>• [One server serializes the updates](/entities/one-server-serializes-the-updates.md) |  |  |  |
| [Replication for durability](/concepts/replication-for-durability.md) | ★ | • [Three Git replicas with majority writes](/entities/three-git-replicas-with-majority-writes.md)<br>• [Durability delegated to object storage](/entities/durability-delegated-to-object-storage.md)<br>• [Single copy on a file server](/entities/single-copy-on-a-file-server.md) |  | • [Block-level filesystem replication](/entities/block-level-filesystem-replication.md) |  |
| [Serving reads](/concepts/serving-reads.md) | ★ | • [Nearest up-to-date replica](/entities/nearest-up-to-date-replica.md)<br>• [Cache servers near the clients](/entities/cache-servers-near-the-clients.md)<br>• [Stateless servers with a local disk cache](/entities/stateless-servers-with-a-local-disk-cache.md) |  |  |  |
| [Source of truth for repository state](/concepts/source-of-truth-for-repository-state.md) | ★ | • [Repository files on server disks](/entities/repository-files-on-server-disks.md)<br>• [Write-ahead log in object storage](/entities/write-ahead-log-in-object-storage.md) | • [Objects in a distributed hash table](/entities/objects-in-a-distributed-hash-table.md) | • [Blobs plus a relational reference database](/entities/blobs-plus-a-relational-reference-database.md) |  |

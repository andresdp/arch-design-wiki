---
type: Design Decision
title: Serving reads
description: Where read traffic (fetches, clones, CI checkouts) is served from.
id: '5'
core: true
values: 3
candidate_values: 3
outcomes: 0
evidence:
  codes: 5
  documents: 9
  sources: 4
relations: []
tags:
- dimension
- core
exclusivity: 0.5
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Serving reads

Where read traffic (fetches, clones, CI checkouts) is served from.

## Values

| Value | Status | Passages |
|---|---|---|
| [Cache servers near the clients](/entities/cache-servers-near-the-clients.md) | accepted | 2 |
| [Nearest up-to-date replica](/entities/nearest-up-to-date-replica.md) | accepted | 4 |
| [Stateless servers with a local disk cache](/entities/stateless-servers-with-a-local-disk-cache.md) | accepted | 5 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### To this dimension

- Choices on [Replication for durability](/concepts/replication-for-durability.md) limit the options available on this dimension. *Serving from the nearest replica needs replicas; a single copy leaves one place to read from.*
- Choices on [Client data transfer](/concepts/client-data-transfer.md) limit the options available on this dimension. *On-demand object downloads put every file open on the network, which cache servers near the clients absorb.*

## Exclusivity

The values of a dimension are alternatives, so each source should adopt one of them. **2 of 4 sources** adopt one value (or a declared hybrid): exclusivity 0.50.

Values adopted together:

- [Nearest up-to-date replica](/entities/nearest-up-to-date-replica.md) and [Stateless servers with a local disk cache](/entities/stateless-servers-with-a-local-disk-cache.md): [s1](/sources/s1.md)
- [Cache servers near the clients](/entities/cache-servers-near-the-clients.md) and [Stateless servers with a local disk cache](/entities/stateless-servers-with-a-local-disk-cache.md): [s5](/sources/s5.md)

## Evidence

5 open codes from 9 passages in 4 sources.

**Core dimension:** yes ★ (4 sources; core = ≥ 2 sources).

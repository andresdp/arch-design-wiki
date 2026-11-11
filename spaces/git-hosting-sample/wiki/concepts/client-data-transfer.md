---
type: Design Decision
title: Client data transfer
description: What a developer's machine downloads to work on a repository.
id: '4'
core: true
values: 3
candidate_values: 3
outcomes: 0
evidence:
  codes: 6
  documents: 11
  sources: 3
relations:
- constrains Serving reads
tags:
- dimension
- core
exclusivity: 0.33
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Client data transfer

What a developer's machine downloads to work on a repository.

## Values

| Value | Status | Passages |
|---|---|---|
| [Full clone over the Git protocol](/entities/full-clone-over-the-git-protocol.md) | accepted | 4 |
| [Partial clone with sparse checkout](/entities/partial-clone-with-sparse-checkout.md) | accepted | 7 |
| [Virtualized filesystem with on-demand objects](/entities/virtualized-filesystem-with-on-demand-objects.md) | mixed | 6 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- Choices on this dimension limit the options available on [Serving reads](/concepts/serving-reads.md). *On-demand object downloads put every file open on the network, which cache servers near the clients absorb.*


## Exclusivity

The values of a dimension are alternatives, so each source should adopt one of them. **1 of 3 sources** adopt one value (or a declared hybrid): exclusivity 0.33.

Values adopted together:

- [Full clone over the Git protocol](/entities/full-clone-over-the-git-protocol.md) and [Virtualized filesystem with on-demand objects](/entities/virtualized-filesystem-with-on-demand-objects.md): [s1](/sources/s1.md), [s5](/sources/s5.md)
- [Full clone over the Git protocol](/entities/full-clone-over-the-git-protocol.md) and [Partial clone with sparse checkout](/entities/partial-clone-with-sparse-checkout.md): [s5](/sources/s5.md)
- [Partial clone with sparse checkout](/entities/partial-clone-with-sparse-checkout.md) and [Virtualized filesystem with on-demand objects](/entities/virtualized-filesystem-with-on-demand-objects.md): [s5](/sources/s5.md)

## Evidence

6 open codes from 11 passages in 3 sources.

**Core dimension:** yes ★ (3 sources; core = ≥ 2 sources).

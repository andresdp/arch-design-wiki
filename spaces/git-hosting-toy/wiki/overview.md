---
type: Overview
title: toy-git-hosting
run: '20261109_000000'
view: selected
dimensions: 5
values: 17
generation_llm: openai/gpt-5.6-luna
evaluation_llm: openai/gpt-5.6-luna
embedding: openai/text-embedding-3-small
tags:
- index
source_count: 5
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

![ddspace](assets/ddspace-logo.svg)

# toy-git-hosting

This wiki presents a **design space** written by hand. A design space organizes the architectural design decisions of a domain: each **dimension** is one decision a designer faces, and its **values** are the alternatives for it. Every page is generated from the design space's data, without rewording. New to design spaces? Start with [About this design space](/approach.md).

Run 20261109_000000 (selected view): 5 dimensions, 17 values, 5 sources.

## Use case

*The question the design space answers.*

Identify the design decisions practitioners face, the alternatives they consider for each, and the outcomes they report.

## Dimensions

*A dimension is one design decision, phrased as a question a designer must answer. Its values are the alternative answers found in the sources, each with a status: **accepted** (adopted), **rejected** (considered and discarded), **mixed** (adopted by some sources, rejected by others) or **outcome** (an effect of decisions, not a choice).*

**Core dimensions** (5 of 5) have evidence from ≥ 2 sources: the axes the sources share. The others rest on a single source or system.

### Core

- ★ [Client data transfer](/concepts/client-data-transfer.md): 3 values
- ★ [Reference update coordination](/concepts/reference-update-coordination.md): 3 values
- ★ [Replication for durability](/concepts/replication-for-durability.md): 4 values
- ★ [Serving reads](/concepts/serving-reads.md): 3 values
- ★ [Source of truth for repository state](/concepts/source-of-truth-for-repository-state.md): 4 values

## Synthesis

*Pages that look at the design space as a whole.*

- [Overview](/synthesis/overview.md): use case, run summary, narrative summary, and every dimension with its values by status
- [Contested decisions](/synthesis/contested.md): values some sources adopt and others reject
- [Dropped and unsupported](/synthesis/dropped.md): dimensions removed during selection, and values without evidence

## Sources

*The documents the design space's evidence comes from. A source's page lists the decisions it informs and whether it adopts or rejects each value.*

- [Git at any scale](/sources/s1.md)
- [Stretching Spokes](/sources/s2.md)
- [Building resilience in Spokes](/sources/s3.md)
- [Scalar philosophy](/sources/s4.md)
- [Introducing Scalar](/sources/s5.md)

---
type: Design Alternative
title: Three Git replicas with majority writes
description: Each repository has three plain Git replicas; a write succeeds once a majority has it.
id: '2.2'
dimension: /concepts/replication-for-durability.md
accepted_by:
- s02_p01
- s03_p01
- s03_p02
- s03_p05
- s03_p06
- s03_p09
- s01_p08
- s03_p03
rejected_by: []
passages: 8
tags:
- value
- accepted
- replication-for-durability
stance: accepted
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Three Git replicas with majority writes

Each repository has three plain Git replicas; a write succeeds once a majority has it.

## Evidence

- **s02_p01** (accepts) · [Stretching Spokes](/sources/s2.md)
- **s03_p01** (accepts) · [Building resilience in Spokes](/sources/s3.md)
- **s03_p02** (accepts) · [Building resilience in Spokes](/sources/s3.md)
- **s03_p05** (accepts) · [Building resilience in Spokes](/sources/s3.md)
- **s03_p06** (accepts) · [Building resilience in Spokes](/sources/s3.md)
- **s03_p09** (accepts) · [Building resilience in Spokes](/sources/s3.md)
- **s01_p08** (accepts) · [Git at any scale](/sources/s1.md)
- **s03_p03** (accepts) · [Building resilience in Spokes](/sources/s3.md)

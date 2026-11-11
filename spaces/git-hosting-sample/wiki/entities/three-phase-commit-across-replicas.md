---
type: Design Alternative
title: Three-phase commit across replicas
description: Reference updates run as a transaction that all replicas vote on.
id: '3.1'
dimension: /concepts/reference-update-coordination.md
accepted_by:
- s01_p07
- s01_p08
- s02_p03
- s02_p04
rejected_by: []
passages: 4
tags:
- value
- accepted
- reference-update-coordination
stance: accepted
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-09T00:00:00-03:00'
---

# Three-phase commit across replicas

Reference updates run as a transaction that all replicas vote on.

## Evidence

- **s01_p07** (accepts) · [Git at any scale](/sources/s1.md)
- **s01_p08** (accepts) · [Git at any scale](/sources/s1.md)
- **s02_p03** (accepts) · [Stretching Spokes](/sources/s2.md)
- **s02_p04** (accepts) · [Stretching Spokes](/sources/s2.md)

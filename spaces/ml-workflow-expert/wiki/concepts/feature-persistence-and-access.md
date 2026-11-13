---
type: Design Decision
title: Feature persistence and access
description: How to persist and provide access to features?
id: '4'
core: true
values: 2
candidate_values: 2
outcomes: 0
evidence:
  codes: 0
  documents: 0
  sources: 0
relations:
- affects Adoption of MLOps
tags:
- dimension
- core
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-12T22:37:00-03:00'
---

# Feature persistence and access

How to persist and provide access to features?

## Values

| Value | Status | Passages |
|---|---|---|
| [Feature store](/entities/feature-store.md) | accepted | 0 |
| [Store features in data stores without specific support](/entities/store-features-in-data-stores-without-specific-support.md) | accepted | 0 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- Choices on this dimension affect the outcomes of [Adoption of MLOps](/concepts/adoption-of-mlops.md). *feature persistence and access decision*

### To this dimension

- Choices on [Model serving](/concepts/model-serving.md) affect the outcomes of this dimension. *how to access features for model serving*
- Choices on [Automated data processing for model building](/concepts/automated-data-processing-for-model-building.md) affect the outcomes of this dimension. *how to store resulting features*
- Choices on [Model building approach](/concepts/model-building-approach.md) affect the outcomes of this dimension. *how to access features for model training*

## Evidence

0 open codes from 0 passages in 0 sources.

**Core dimension:** yes ★ (0 sources; core = ≥ 0 sources).

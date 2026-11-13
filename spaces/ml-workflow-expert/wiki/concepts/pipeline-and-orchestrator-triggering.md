---
type: Design Decision
title: Pipeline and orchestrator triggering
description: How to trigger a machine learning pipeline or orchestrator?
id: '12'
core: true
values: 6
candidate_values: 6
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
  at: '2026-11-13T18:52:21-03:00'
---

# Pipeline and orchestrator triggering

How to trigger a machine learning pipeline or orchestrator?

## Values

| Value | Status | Passages |
|---|---|---|
| [On availability of new training data trigger](/entities/on-availability-of-new-training-data-trigger.md) | accepted | 0 |
| [On changes in the data distribution trigger](/entities/on-changes-in-the-data-distribution-trigger.md) | accepted | 0 |
| [On model performance degradation trigger](/entities/on-model-performance-degradation-trigger.md) | accepted | 0 |
| [On-commit trigger](/entities/on-commit-trigger.md) | accepted | 0 |
| [On-demand trigger](/entities/on-demand-trigger.md) | accepted | 0 |
| [On-schedule trigger](/entities/on-schedule-trigger.md) | accepted | 0 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- Choices on this dimension affect the outcomes of [Adoption of MLOps](/concepts/adoption-of-mlops.md). *trigger pipeline or orchestrator decision*

### To this dimension

- Choices on [Automated integration and delivery for ML](/concepts/automated-integration-and-delivery-for-ml.md) affect the outcomes of this dimension. *Consider If Not Decided Yet*
- Choices on [Model building approach](/concepts/model-building-approach.md) affect the outcomes of this dimension. *Consider If Not Decided Yet*

## Evidence

0 open codes from 0 passages in 0 sources.

**Core dimension:** yes ★ (0 sources; core = ≥ 0 sources).

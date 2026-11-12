---
type: Design Decision
title: Model serving
description: How to serve model predictions or scores?
id: '5'
core: true
values: 5
candidate_values: 5
outcomes: 0
evidence:
  codes: 0
  documents: 0
  sources: 0
relations:
- affects Feature persistence and access
- affects Notification of prediction results
- affects Data ingestion
tags:
- dimension
- core
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-12T16:57:13-03:00'
---

# Model serving

How to serve model predictions or scores?

## Values

| Value | Status | Passages |
|---|---|---|
| [Data batch based model serving](/entities/data-batch-based-model-serving.md) | accepted | 0 |
| [Hybrid online/offline model serving](/entities/hybrid-online-offline-model-serving.md) | accepted | 0 |
| [Local service/API based model serving](/entities/local-service-api-based-model-serving.md) | accepted | 0 |
| [Microservice based model serving](/entities/microservice-based-model-serving.md) | accepted | 0 |
| [Precompute serving](/entities/precompute-serving.md) | accepted | 0 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- Choices on this dimension affect the outcomes of [Feature persistence and access](/concepts/feature-persistence-and-access.md). *how to access features for model serving*
- Choices on this dimension affect the outcomes of [Notification of prediction results](/concepts/notification-of-prediction-results.md). *Consider If Not Decided Yet*
- Choices on this dimension affect the outcomes of [Data ingestion](/concepts/data-ingestion.md). *ingest data required during model serving*

### To this dimension

- Choices on [ML model integration into the application](/concepts/ml-model-integration-into-the-application.md) affect the outcomes of this dimension. *Consider If Not Decided Yet*

## Evidence

0 open codes from 0 passages in 0 sources.

**Core dimension:** yes ★ (0 sources; core = ≥ 0 sources).

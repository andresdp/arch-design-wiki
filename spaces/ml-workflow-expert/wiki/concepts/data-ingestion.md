---
type: Design Decision
title: Data ingestion
description: How to ingest data into ML projects or applications?
id: '7'
core: true
values: 4
candidate_values: 4
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
  at: '2026-11-12T16:57:13-03:00'
---

# Data ingestion

How to ingest data into ML projects or applications?

## Values

| Value | Status | Passages |
|---|---|---|
| [Data ingestion by request](/entities/data-ingestion-by-request.md) | accepted | 0 |
| [Data ingestion in batches](/entities/data-ingestion-in-batches.md) | accepted | 0 |
| [Manual data ingestion](/entities/manual-data-ingestion.md) | accepted | 0 |
| [Streamed data ingestion](/entities/streamed-data-ingestion.md) | accepted | 0 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- Choices on this dimension affect the outcomes of [Adoption of MLOps](/concepts/adoption-of-mlops.md). *how should data be ingested in MLOps?*

### To this dimension

- Choices on [Model serving](/concepts/model-serving.md) affect the outcomes of this dimension. *ingest data required during model serving*
- Choices on [Automated data processing for model building](/concepts/automated-data-processing-for-model-building.md) affect the outcomes of this dimension. *ingest data for data processing and later model building*

## Evidence

0 open codes from 0 passages in 0 sources.

**Core dimension:** yes ★ (0 sources; core = ≥ 0 sources).

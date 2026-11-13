---
type: Design Decision
title: Automated data processing for model building
description: How to automatically process the data used for model building?
id: '14'
core: true
values: 4
candidate_values: 4
outcomes: 0
evidence:
  codes: 0
  documents: 0
  sources: 0
relations:
- affects Feature persistence and access
- affects Data ingestion
- affects Data processing parallelization
- affects Adoption of MLOps
tags:
- dimension
- core
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-13T18:52:21-03:00'
---

# Automated data processing for model building

How to automatically process the data used for model building?

## Values

| Value | Status | Passages |
|---|---|---|
| [Data pipeline](/entities/data-pipeline.md) | accepted | 0 |
| [Data processing component](/entities/data-processing-component.md) | accepted | 0 |
| [ETL pipeline](/entities/etl-pipeline.md) | accepted | 0 |
| [No data processing automation](/entities/no-data-processing-automation.md) | accepted | 0 |

## Relations

How to read them: [Relations between dimensions](/relations.md).

### From this dimension

- Choices on this dimension affect the outcomes of [Feature persistence and access](/concepts/feature-persistence-and-access.md). *how to store resulting features*
- Choices on this dimension affect the outcomes of [Data ingestion](/concepts/data-ingestion.md). *ingest data for data processing and later model building*
- Choices on this dimension affect the outcomes of [Data processing parallelization](/concepts/data-processing-parallelization.md). *Consider If Not Decided Yet*
- Choices on this dimension affect the outcomes of [Adoption of MLOps](/concepts/adoption-of-mlops.md). *data processing automation decision*

### To this dimension

- Choices on [Model building approach](/concepts/model-building-approach.md) affect the outcomes of this dimension. *how to automate data processing tasks used by or part of model building*

## Evidence

0 open codes from 0 passages in 0 sources.

**Core dimension:** yes ★ (0 sources; core = ≥ 0 sources).

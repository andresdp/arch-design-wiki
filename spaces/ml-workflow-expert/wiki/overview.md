---
type: Overview
title: ML workflow (expert)
run: '20261112_165713'
view: selected
dimensions: 28
values: 124
generation_llm: openai/gpt-5.6-luna
evaluation_llm: openai/gpt-5.6-luna
embedding: openai/text-embedding-3-small
tags:
- index
source_count: 0
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-12T16:57:13-03:00'
---

![ddspace](assets/ddspace-logo.svg)

# ML workflow (expert)

This wiki presents a **design space** imported from a decision model written by experts. A design space organizes the architectural design decisions of a domain: each **dimension** is one decision a designer faces, and its **values** are the alternatives for it. Every page is generated from the design space's data, without rewording. New to design spaces? Start with [About this design space](/approach.md).

Run 20261112_165713 (selected view): 28 dimensions, 124 values, 0 sources.

## Use case

*The question the design space answers.*

The architectural design decisions of the machine learning workflow, from data ingestion and processing through model building and training to deployment and operation, with the options for each (Warnett and Zdun's decision model).

## Dimensions

*A dimension is one design decision, phrased as a question a designer must answer. Its values are the alternative answers found in the sources, each with a status: **accepted** (adopted), **rejected** (considered and discarded), **mixed** (adopted by some sources, rejected by others) or **outcome** (an effect of decisions, not a choice).*

**Core dimensions** (28 of 28) have evidence from ≥ 0 sources: the axes the sources share. The others rest on a single source or system.

### Core

- ★ [Adoption of MLOps](/concepts/adoption-of-mlops.md): 2 values
- ★ [Automated data processing for model building](/concepts/automated-data-processing-for-model-building.md): 4 values
- ★ [Automated environment provisioning](/concepts/automated-environment-provisioning.md): 2 values
- ★ [Automated integration and delivery for ML](/concepts/automated-integration-and-delivery-for-ml.md): 4 values
- ★ [Batch or real-time data processing](/concepts/batch-or-real-time-data-processing.md): 2 values
- ★ [Data access interface](/concepts/data-access-interface.md): 5 values
- ★ [Data ingestion](/concepts/data-ingestion.md): 4 values
- ★ [Data processing parallelization](/concepts/data-processing-parallelization.md): 4 values
- ★ [Data processing pipeline tasks](/concepts/data-processing-pipeline-tasks.md): 7 values
- ★ [Data storage for ML applications](/concepts/data-storage-for-ml-applications.md): 4 values
- ★ [Data versioning](/concepts/data-versioning.md): 3 values
- ★ [Delivery pipeline tasks](/concepts/delivery-pipeline-tasks.md): 9 values
- ★ [Development environment](/concepts/development-environment.md): 2 values
- ★ [Feature persistence and access](/concepts/feature-persistence-and-access.md): 2 values
- ★ [ML model integration into the application](/concepts/ml-model-integration-into-the-application.md): 7 values
- ★ [Model adjustment from monitoring results](/concepts/model-adjustment-from-monitoring-results.md): 2 values
- ★ [Model building approach](/concepts/model-building-approach.md): 3 values
- ★ [Model building parallelization](/concepts/model-building-parallelization.md): 5 values
- ★ [Model building pipeline tasks](/concepts/model-building-pipeline-tasks.md): 10 values
- ★ [Model monitoring and tracking in production](/concepts/model-monitoring-and-tracking-in-production.md): 4 values
- ★ [Model serving](/concepts/model-serving.md): 5 values
- ★ [Model training timing and mode](/concepts/model-training-timing-and-mode.md): 3 values
- ★ [Model versions in production](/concepts/model-versions-in-production.md): 3 values
- ★ [Notification of prediction results](/concepts/notification-of-prediction-results.md): 3 values
- ★ [Pipeline and orchestrator triggering](/concepts/pipeline-and-orchestrator-triggering.md): 6 values
- ★ [Scope of CI/CD automation](/concepts/scope-of-ci-cd-automation.md): 3 values
- ★ [Testing scope in ML pipelines](/concepts/testing-scope-in-ml-pipelines.md): 14 values
- ★ [Use of AutoML](/concepts/use-of-automl.md): 2 values

## Synthesis

*Pages that look at the design space as a whole.*

- [Overview](/synthesis/overview.md): use case, run summary, narrative summary, and every dimension with its values by status
- [Contested decisions](/synthesis/contested.md): values some sources adopt and others reject
- [Dropped and unsupported](/synthesis/dropped.md): dimensions removed during selection, and values without evidence

## Sources

*The documents the design space's evidence comes from. A source's page lists the decisions it informs and whether it adopts or rejects each value.*

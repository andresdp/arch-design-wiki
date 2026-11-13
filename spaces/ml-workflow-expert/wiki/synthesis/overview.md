---
type: Synthesis
title: Overview
tags:
- synthesis
generated:
  by: delvedspace/0.1.0.dev0
  at: '2026-11-12T22:37:00-03:00'
---

# Overview

## Use case

The architectural design decisions of the machine learning workflow, from data ingestion and processing through model building and training to deployment and operation, with the options for each (Warnett and Zdun's decision model).

## Run

| Item | Value |
|---|---|
| Run | 20261112_223700 (selected view) |
| Dimensions | 28 |
| Values | 124: 124 accepted, 0 mixed, 0 rejected, 0 outcome |
| Sources | 0 |
| Iterations | 1 |
| Dropped dimensions | 0 |
| Generation LLM | `openai/gpt-5.6-luna` |
| Evaluation LLM (judge) | `openai/gpt-5.6-luna` |
| Embedding model | `openai/text-embedding-3-small` |

## Dimensions and values

Core dimensions (★) have evidence from ≥ 0 sources; they are listed first. Relations between dimensions are explained in [Relations between dimensions](/relations.md).

| Dimension | Core | Accepted | Mixed | Rejected | Outcomes |
|---|---|---|---|---|---|
| [Adoption of MLOps](/concepts/adoption-of-mlops.md) | ★ | • [MLOps](/entities/mlops.md)<br>• [No MLOps](/entities/no-mlops.md) |  |  |  |
| [Automated data processing for model building](/concepts/automated-data-processing-for-model-building.md) | ★ | • [Data pipeline](/entities/data-pipeline.md)<br>• [ETL pipeline](/entities/etl-pipeline.md)<br>• [Data processing component](/entities/data-processing-component.md)<br>• [No data processing automation](/entities/no-data-processing-automation.md) |  |  |  |
| [Automated environment provisioning](/concepts/automated-environment-provisioning.md) | ★ | • [Automated provisioning](/entities/automated-provisioning.md)<br>• [No automated provisioning](/entities/no-automated-provisioning.md) |  |  |  |
| [Automated integration and delivery for ML](/concepts/automated-integration-and-delivery-for-ml.md) | ★ | • [CI/CD pipeline](/entities/ci-cd-pipeline.md)<br>• [Build and Deployment scripts](/entities/build-and-deployment-scripts.md)<br>• [Machine learning orchestrator](/entities/machine-learning-orchestrator.md)<br>• [No integration or delivery automation](/entities/no-integration-or-delivery-automation.md) |  |  |  |
| [Batch or real-time data processing](/concepts/batch-or-real-time-data-processing.md) | ★ | • [Batch-based data processing](/entities/batch-based-data-processing.md)<br>• [Real-time, stream-based data processing](/entities/real-time-stream-based-data-processing.md) |  |  |  |
| [Data access interface](/concepts/data-access-interface.md) | ★ | • [Local data access API](/entities/local-data-access-api.md)<br>• [Service-based data access API](/entities/service-based-data-access-api.md)<br>• [Pub/sub data access API](/entities/pub-sub-data-access-api.md)<br>• [Message/event queueing-based data access API](/entities/message-event-queueing-based-data-access-api.md)<br>• [Data provider is accessed directly](/entities/data-provider-is-accessed-directly.md) |  |  |  |
| [Data ingestion](/concepts/data-ingestion.md) | ★ | • [Streamed data ingestion](/entities/streamed-data-ingestion.md)<br>• [Data ingestion by request](/entities/data-ingestion-by-request.md)<br>• [Data ingestion in batches](/entities/data-ingestion-in-batches.md)<br>• [Manual data ingestion](/entities/manual-data-ingestion.md) |  |  |  |
| [Data processing parallelization](/concepts/data-processing-parallelization.md) | ★ | • [Data pipeline per data set](/entities/data-pipeline-per-data-set.md)<br>• [Data partitioning in data pipeline](/entities/data-partitioning-in-data-pipeline.md)<br>• [Hybrid data processing parallelization](/entities/hybrid-data-processing-parallelization.md)<br>• [No parallel data processing](/entities/no-parallel-data-processing.md) |  |  |  |
| [Data processing pipeline tasks](/concepts/data-processing-pipeline-tasks.md) | ★ | • [Data extraction](/entities/data-extraction.md)<br>• [Data preparation](/entities/data-preparation.md)<br>• [Data validation](/entities/data-validation.md)<br>• [Data transformation](/entities/data-transformation.md)<br>• [Data selection](/entities/data-selection.md)<br>• [Feature engineering](/entities/feature-engineering.md)<br>• [Data processing hyperparameter tuning](/entities/data-processing-hyperparameter-tuning.md) |  |  |  |
| [Data storage for ML applications](/concepts/data-storage-for-ml-applications.md) | ★ | • [Shared data store](/entities/shared-data-store.md)<br>• [Data service](/entities/data-service.md)<br>• [Event store](/entities/event-store.md)<br>• [No data store](/entities/no-data-store.md) |  |  |  |
| [Data versioning](/concepts/data-versioning.md) | ★ | • [Data version repository](/entities/data-version-repository.md)<br>• [Data versioning in code repository](/entities/data-versioning-in-code-repository.md)<br>• [No data versioning](/entities/no-data-versioning.md) |  |  |  |
| [Delivery pipeline tasks](/concepts/delivery-pipeline-tasks.md) | ★ | • [Packaging](/entities/packaging.md)<br>• [Testing](/entities/testing.md)<br>• [Building](/entities/building.md)<br>• [Deployment](/entities/deployment.md)<br>• [Containerization](/entities/containerization.md)<br>• [Canary testing](/entities/canary-testing.md)<br>• [A/B testing](/entities/a-b-testing.md)<br>• [Evidence based hypothesis testing](/entities/evidence-based-hypothesis-testing.md)<br>• [Version control repository](/entities/version-control-repository.md) |  |  |  |
| [Development environment](/concepts/development-environment.md) | ★ | • [Use computational notebooks](/entities/use-computational-notebooks.md)<br>• [Use an IDE](/entities/use-an-ide.md) |  |  |  |
| [Feature persistence and access](/concepts/feature-persistence-and-access.md) | ★ | • [Feature store](/entities/feature-store.md)<br>• [Store features in data stores without specific support](/entities/store-features-in-data-stores-without-specific-support.md) |  |  |  |
| [ML model integration into the application](/concepts/ml-model-integration-into-the-application.md) | ★ | • [Model as a service](/entities/model-as-a-service.md)<br>• [Model in monolith](/entities/model-in-monolith.md)<br>• [Model as module in modular monolith](/entities/model-as-module-in-modular-monolith.md)<br>• [Model in batch prediction system](/entities/model-in-batch-prediction-system.md)<br>• [Event-driven model as a service](/entities/event-driven-model-as-a-service.md)<br>• [Serverless model as a service](/entities/serverless-model-as-a-service.md)<br>• [No integration of the model](/entities/no-integration-of-the-model.md) |  |  |  |
| [Model adjustment from monitoring results](/concepts/model-adjustment-from-monitoring-results.md) | ★ | • [Manual model adjustment](/entities/manual-model-adjustment.md)<br>• [Automated model adjustment](/entities/automated-model-adjustment.md) |  |  |  |
| [Model building approach](/concepts/model-building-approach.md) | ★ | • [Model building pipeline](/entities/model-building-pipeline.md)<br>• [Model builder component](/entities/model-builder-component.md)<br>• [Model building in development tool](/entities/model-building-in-development-tool.md) |  |  |  |
| [Model building parallelization](/concepts/model-building-parallelization.md) | ★ | • [Model building pipeline per model](/entities/model-building-pipeline-per-model.md)<br>• [Training data partitioning](/entities/training-data-partitioning.md)<br>• [Model partitioning](/entities/model-partitioning.md)<br>• [Hybrid model building parallelization](/entities/hybrid-model-building-parallelization.md)<br>• [No parallel model building](/entities/no-parallel-model-building.md) |  |  |  |
| [Model building pipeline tasks](/concepts/model-building-pipeline-tasks.md) | ★ | • [Model training](/entities/model-training.md)<br>• [Data splitting](/entities/data-splitting.md)<br>• [Data checkpoints](/entities/data-checkpoints.md)<br>• [Model validation](/entities/model-validation.md)<br>• [Model selection](/entities/model-selection.md)<br>• [Model packaging](/entities/model-packaging.md)<br>• [Development tool facade](/entities/development-tool-facade.md)<br>• [Development tool export](/entities/development-tool-export.md)<br>• [Train multiple model versions with different parameters and/or algorithms](/entities/train-multiple-model-versions-with-different-parameters-and-or-algorithms.md)<br>• [Model hyperparameter tuning](/entities/model-hyperparameter-tuning.md) |  |  |  |
| [Model monitoring and tracking in production](/concepts/model-monitoring-and-tracking-in-production.md) | ★ | • [Model performance monitoring](/entities/model-performance-monitoring.md)<br>• [Monitoring or logging data and predictions](/entities/monitoring-or-logging-data-and-predictions.md)<br>• [No in-production monitoring](/entities/no-in-production-monitoring.md)<br>• [Model in-production tracking](/entities/model-in-production-tracking.md) |  |  |  |
| [Model serving](/concepts/model-serving.md) | ★ | • [Microservice based model serving](/entities/microservice-based-model-serving.md)<br>• [Local service/API based model serving](/entities/local-service-api-based-model-serving.md)<br>• [Data batch based model serving](/entities/data-batch-based-model-serving.md)<br>• [Precompute serving](/entities/precompute-serving.md)<br>• [Hybrid online/offline model serving](/entities/hybrid-online-offline-model-serving.md) |  |  |  |
| [Model training timing and mode](/concepts/model-training-timing-and-mode.md) | ★ | • [Batch-based learning](/entities/batch-based-learning.md)<br>• [Incremental learning](/entities/incremental-learning.md)<br>• [Hybrid batch-based and incremental learning](/entities/hybrid-batch-based-and-incremental-learning.md) |  |  |  |
| [Model versions in production](/concepts/model-versions-in-production.md) | ★ | • [N versions in production](/entities/n-versions-in-production.md)<br>• [Rollback to previous model version](/entities/rollback-to-previous-model-version.md)<br>• [Single model in production](/entities/single-model-in-production.md) |  |  |  |
| [Notification of prediction results](/concepts/notification-of-prediction-results.md) | ★ | • [Push notification](/entities/push-notification.md)<br>• [Polling](/entities/polling.md)<br>• [Block on result](/entities/block-on-result.md) |  |  |  |
| [Pipeline and orchestrator triggering](/concepts/pipeline-and-orchestrator-triggering.md) | ★ | • [On-demand trigger](/entities/on-demand-trigger.md)<br>• [On-commit trigger](/entities/on-commit-trigger.md)<br>• [On-schedule trigger](/entities/on-schedule-trigger.md)<br>• [On availability of new training data trigger](/entities/on-availability-of-new-training-data-trigger.md)<br>• [On model performance degradation trigger](/entities/on-model-performance-degradation-trigger.md)<br>• [On changes in the data distribution trigger](/entities/on-changes-in-the-data-distribution-trigger.md) |  |  |  |
| [Scope of CI/CD automation](/concepts/scope-of-ci-cd-automation.md) | ★ | • [Build, test, and deploy models to be served and other system components](/entities/build-test-and-deploy-models-to-be-served-and-other-system-components.md)<br>• [Build, test, and deploy machine learning pipelines and components needed during pipeline runs](/entities/build-test-and-deploy-machine-learning-pipelines-and-components-needed-during-pi.md)<br>• [No automated deployment](/entities/no-automated-deployment.md) |  |  |  |
| [Testing scope in ML pipelines](/concepts/testing-scope-in-ml-pipelines.md) | ★ | • [Canary testing](/entities/canary-testing-2.md)<br>• [A/B testing](/entities/a-b-testing-2.md)<br>• [Evidence based hypothesis testing](/entities/evidence-based-hypothesis-testing-2.md)<br>• [Unit testing system components](/entities/unit-testing-system-components.md)<br>• [System integration testing](/entities/system-integration-testing.md)<br>• [Unit testing feature engineering logic](/entities/unit-testing-feature-engineering-logic.md)<br>• [Unit testing different methods implemented in a model](/entities/unit-testing-different-methods-implemented-in-a-model.md)<br>• [Testing model training converges](/entities/testing-model-training-converges.md)<br>• [Testing trained model quality](/entities/testing-trained-model-quality.md)<br>• [Unit testing pipeline components](/entities/unit-testing-pipeline-components.md)<br>• [Integration testing pipeline components](/entities/integration-testing-pipeline-components.md)<br>• [Prediction service API testing](/entities/prediction-service-api-testing.md)<br>• [Prediction service performance testing](/entities/prediction-service-performance-testing.md)<br>• [No testing](/entities/no-testing.md) |  |  |  |
| [Use of AutoML](/concepts/use-of-automl.md) | ★ | • [AutoML](/entities/automl.md)<br>• [No AutoML](/entities/no-automl.md) |  |  |  |

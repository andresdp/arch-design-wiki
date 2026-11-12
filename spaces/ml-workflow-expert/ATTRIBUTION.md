# The expert ML-workflow design space

This design space is the decision model of

> S. J. Warnett and U. Zdun, "Architectural Design Decisions for the Machine Learning Workflow", *IEEE Computer*,
> vol. 55, no. 3, pp. 40–51, 2022. doi:10.1109/MC.2021.3134800

imported into `ddspace`: each decision becomes a dimension, its options become values, and the links between
decisions become relations (28 dimensions, 124 values, 40 relations). The model's forces and impact ratings are not
part of the space. The model file is `study/designing2027/inputs/gt_model.json`; the import is
`study/designing2027/build_workspace.py`.

The model names each decision by its question. Here each dimension is named as a concern instead, and keeps the
authors' question, word for word, as its description. The names are ours
(`study/designing2027/inputs/dimension_names.yaml`); the decisions, their questions and their options are the
authors'. The study's agent sessions ran with the questions as the dimension names.

| Dimension | The authors' question |
|---|---|
| ML model integration into the application | How to integrate a machine learning model in an application? |
| Data storage for ML applications | How to store data used in machine learning applications? |
| Data access interface | How to design the interface for data access? |
| Feature persistence and access | How to persist and provide access to features? |
| Model serving | How to serve model predictions or scores? |
| Notification of prediction results | How to inform clients about prediction result availability? |
| Data ingestion | How to ingest data into ML projects or applications? |
| Automated integration and delivery for ML | How to perform automatic integration and delivery in a machine learning context? |
| Delivery pipeline tasks | Which tasks can be performed by a delivery pipeline or component? |
| Model versions in production | Which model versions should be deployed to production and how? |
| Data versioning | How to version data decision? |
| Pipeline and orchestrator triggering | How to trigger a machine learning pipeline or orchestrator? |
| Automated environment provisioning | How to automatically provision environments? |
| Automated data processing for model building | How to automatically process the data used for model building? |
| Batch or real-time data processing | Should data be processed in batches or in realtime? |
| Data processing pipeline tasks | Which data processing tasks can be performed by a data processing pipeline or component? |
| Data processing parallelization | How to parallelize data processing? |
| Model building approach | How to perform model building in an ML project? |
| Model training timing and mode | When and how to train the model? |
| Model building pipeline tasks | Which tasks can be performed by a model building pipeline or component? |
| Model building parallelization | How to parallelize model building? |
| Model monitoring and tracking in production | How to monitor and track the model in production? |
| Use of AutoML | Should AutoML be used and if so where? |
| Model adjustment from monitoring results | How to adjust models based on monitoring results? |
| Scope of CI/CD automation | What to build, test, and deploy automatically by CI/CD pipelines? |
| Testing scope in ML pipelines | What to test in a machine learning/data science pipeline? |
| Adoption of MLOps | Should MLOps be used and if so when? |
| Development environment | What development environment should be used? |

All credit for the decisions and options goes to the authors of the model. Please cite their article when you use
this space.

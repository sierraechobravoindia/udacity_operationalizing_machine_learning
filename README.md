# Operationalizing Machine Learning

This repository contains artefacts and documentation for the 2nd project in the udacity Machine Learning Engineer with Azure Nanodegree.

## Architectural Diagram
![Basic Architecture for Azure AutoML](/images/Architecture.pdf)
The diagram shows the basic architecture of the Azure Auto ML. The required ingredients to run an AutoML step are a dataset, an experiment and compute. The AutoML step then produces a "best" model under the definded boundary conditions (like metric, task, runtime contraints, ...). This model can then be registered and deployed. A deployed model creates an API documentation via Swagger and exposes a URL for scoring/inference.

## Key Steps

This section describes the major steps necessary to first train a model with Azure AutoML and deploy the model and then semi-automate the AutoML training with a published pipeline. The section also contains the required screenshots as proof-of-work.

### Register a dataset

The first step is to create a dataset, this makes it convenient to ingest data in the Azure ML Studio. The screenshot shows the Bank Marketing Dataset used in this project.
![Create a Dataset](/images/Dataset.png)
More background information on the dataset used can be found in the UCI Machine Learning Repository: [Bank Marketing Dataset](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing)

### Create a compute resource

To run experiments/jobs like AutoML a compute resource is needed. Here we create a small compute cluster to run the AutoML step on.

The screenshot shows the compute cluster created for and used in this project.
![Create a compute cluster](/images/computecluster.png)

### Create the AutoML Run
Azure AutoML provides an an easy to use fully automatic ML-step including concurrent model selection, hyperparameter tuning and model comparison given a dataset, a ML task, a target metric some other boundary conditions and constraints.


### Deploy the best model

Azure provides an easy way to deploy a trained model. A deployed model provides a REST API for scoring/inference and a Swagger API documentation. 
The screenshot shows an API inference call with two datasets.

![endpoint.py script runs against the API producing JSON output from the model.](/images/endpoint_run.png)
The Azure deployment feature also comprises a logging functionality called App Insights.
![Logging is enabled by running the provided logs.py script](/images/running_logs_py.png)



### Inspect the (Swagger) API documentation

This screenshot shows the provided Swagger API documentation.
![Swagger runs on localhost showing the HTTP API methods and responses for the model](/images/swagger_doc.png)

### Benchmark the endpoint performance

To easily measure the performance of the HTTP endpoint of the deplyed model, we can use Apache Benchmark as seen in this screenshot.
![Apache Benchmark (ab) runs against the HTTP API using authentication keys to retrieve performance results.](/images/apache_benchmark_run.png)

### Create a pipeline

To fully automate ML tasks like retraining and deploying models on a scheduled or periodic basis, Azure provides a pipeline feature.
Here we wrap the AutoML step in a pipeline and make the pipeline accessible via publication to an endpoint.
![The pipeline section of Azure ML studio, showing that the pipeline has been created](/images/pipeline_created_and_running.png)

![The Bankmarketing dataset with the AutoML module](/images/autoML_dataset.png)


### Consume the pipeline

The published pipeline can then be easily executed from anywhere via a REST API.

![The “Published Pipeline overview”, showing a REST endpoint and a status of ACTIVE](/images/pipeline_endpoint_active.png)

![A screenshot of the Jupyter Notebook is included in the submission showing the “Use RunDetails Widget” with the step runs](/images/RunDetails_widget.png)


![ML studio showing the pipeline endpoint as Active](/images/pipeline_endpoint_active.png)
![ML studio showing the scheduled run](/images/scheduled_run.png)



## Future improvements

No effort was placed on model performance as the project focuses on the engineering part and less the machine learning part. The AutoML step had a severe time contraint and did not use deep learning.

Another topic for improvement could be the pipeline automation. The pipeline does not include the model deployment step only the AutoML step. In a production setting, it might be a good idea to include the deployment into the pipeline to fully automate periodic retraining of the model.

## Screen Recording
The required screencast with a quick tour of the project in the Azure UI can be found [here](http://youtube.com/alsjdhfklasjhdfl).
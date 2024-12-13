# AutoML with Azure Machine Learning Studio

This project demonstrated Azure Machine Learning Studio and its ability to prepare data to train a model, train the model with AutoML, create and publish a pipeline for the model, and access the model via API (JSON endpoint) to make predictions.
The goal was to train a binary classification model through AutoML to identify if a client will subscribe to a term deposit with the bank.

## Architectural Diagram

![Diagram](./diagram.png)

## Key Steps

**1. Authentication**
   I used my own environment for the project. In this step, I created a service principle with az. The service principle is then assigned  to the Azure Machine learning workspace with controlled permissions to access it.
   ![Creating SP](./step01_02_sp_created.PNG)
   ![SP Assignment](./step01_01_sp_assigment.PNG)
   ![SP Permissions](./step01_03_sp_assigment_portal.png)

**2. Registering dataset in Azure Machine Learning Studio**
   In this step I registered the Bankmarketing dataset in the Azure Machine Learning Studio
   ![Bankmarketing dataset](./step02_01_registered_dataset.png)

**3. Create a new experiment and run it**
    In this step I created a new experiment in Azure ML Studio with the uploaded Bankmarketing dataset and run the job on the compute cluster.
    ![Completed Experiment](./step02_02_experiment_completed.png)
    From the completed experiment I was able to find the best model.
    ![Best Model](./step02_03_best_model.png)

**4. Deploy the best model**
    In this step I deployed the best model using Azure Container Instances. Deployment created a JSON endpoint which could be used for a prediction.
    I also enabled Application Insights to be able to collect logs
    ![Deployment](./step04_01_application_insights_enabled.png)
    I used the logs.py to get the logs
    ![Logs](./step04_02_logs.PNG)
    I also ran the endpoint.py file to check if the endpoint is accessible.
    ![Swagger](./step06_01_endpoint_script_against-api.PNG)

**5. Test deployment locally with Swagger**
    In this step I downloaded the swagger.json file from the endpoint config. I ran Swagger locally and test the endpoint
      ![Local Swagger](./step05_01_swagger_running_locally.png)
      ![Local Response](./step05_02_locall_response.png)

**6. Consume the endpoint**
    In this step I firstly ran the benchmark tool Apache Benchmark to test that the deployed model is consistently performing at the level we are expecting.
    ![Benchmark](./step06_02_apache_benchmark.PNG)
    Lastly I sent a request to the prediction endpoint with test data
    ![Requested Data](./step07_07_request_data.png)

**7. Create, Publish, and Consume a Pipeline via Jupiter Notebook**
    While of the above steps can be completed manually, they can also be done programmatically using Python SDK and AzureML SDK as in the [Jupiter Notebook](./aml-pipelines-with-automated-machine-learning-step.ipynb).
    I have configured the notebook accordingly to my environment and executed it. The details of the execution can be found in the screenshots below as well as in the notebook itself.
    ![Pipeline Created](./step07_01_pipeline_created_and_completed.png)
    ![Pipeline Endpoint](./step07_02_pipeline_endpoint.png)
    ![Pipeline Dataset](./step07_03_bankmarketing_dataset.png)
    ![Pipeline Endpoint Details](./step07_04_pipeline_endpoint_details.png)

## Screen Recording

Link to the recording: 

## Future Enhancements

I think the most useful enhancement, from the development perspective, would be to allow Swagger UI to make requests directly to the endpoint. That would allow faster testing of the deployed model.
Also it would be interesting to play more with setting up pipelines for different models e.g. regression.

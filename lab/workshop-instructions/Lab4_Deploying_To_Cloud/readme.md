# Deploy an AI Model to a cloud endpoint using Azure AI 

> [!NOTE]
>This is a **20-minute** exercise, you will successfully fine-tune the Phi-3 model using Azure Machine Learning Code First Approach. Please note that the fine-tuning process can take a considerable amount of time.

## Learning Objectives

By the end of this workshop, you should be able to:
1. Deploy the fine-tuned model using a code first approach.


## Lab Scenario
To integrate the fine-tuned Phi-3 model with an application, you need to deploy the model to make it accessible for real-time inference. This process involves registering the model, creating an online endpoint, and deploying the model.

## Lab Outline
In this exercise, you will:

- Set the model name, endpoint name, and deployment name for deployment.
- Register the fine-tuned model in the Azure Machine Learning workspace.
- Create an online endpoint.
- Deploy the registered fine-tuned Phi-3 model.

### Deploy the fine-tuned model

### Set the model name, endpoint name, and deployment name for deployment
 
- Open config.py file.
- Replace `AZURE_MODEL_NAME = "your_fine_tuned_model_name"` with the desired name for your model.
- Replace `AZURE_ENDPOINT_NAME = "your_fine_tuned_model_endpoint_name"` with the desired name for your endpoint.
- Replace `AZURE_DEPLOYMENT_NAME = "your_fine_tuned_model_deployment_name"` with the desired name for your deployment.

### Deploy the fine-tuned model
 

Running the deploy_model.py file automates the entire deployment process. It registers the model, creates an endpoint, and executes the deployment based on the settings specified in the config.py file, which includes the model name, endpoint name, and deployment name.

- Open the `deploy_model.py` file in Visual Studio Code.

- Add the following code into `deploy_model.py`.

```Python
import logging
from azure.identity import AzureCliCredential
from azure.ai.ml import MLClient
from azure.ai.ml.entities import Model, ProbeSettings, ManagedOnlineEndpoint, ManagedOnlineDeployment, IdentityConfiguration, ManagedIdentityConfiguration, OnlineRequestSettings
from azure.ai.ml.constants import AssetTypes

# Configuration imports
from config import (
    AZURE_SUBSCRIPTION_ID,
    AZURE_RESOURCE_GROUP_NAME,
    AZURE_ML_WORKSPACE_NAME,
    AZURE_MANAGED_IDENTITY_RESOURCE_ID,
    AZURE_MANAGED_IDENTITY_CLIENT_ID,
    AZURE_MODEL_NAME,
    AZURE_ENDPOINT_NAME,
    AZURE_DEPLOYMENT_NAME
)

# Constants
JOB_NAME = "your-job-name"
COMPUTE_INSTANCE_TYPE = "Standard_E4s_v3"

deployment_env_vars = {
    "SUBSCRIPTION_ID": AZURE_SUBSCRIPTION_ID,
    "RESOURCE_GROUP_NAME": AZURE_RESOURCE_GROUP_NAME,
    "UAI_CLIENT_ID": AZURE_MANAGED_IDENTITY_CLIENT_ID,
}

# Logging setup
logging.basicConfig(
    format="%(asctime)s - %(levelname)s - %(name)s - %(message)s",
    datefmt="%Y-%m-%d %H:%M:%S",
    level=logging.DEBUG
)
logger = logging.getLogger(__name__)

def get_ml_client():
    """Initialize and return the ML Client."""
    credential = AzureCliCredential()
    return MLClient(credential, AZURE_SUBSCRIPTION_ID, AZURE_RESOURCE_GROUP_NAME, AZURE_ML_WORKSPACE_NAME)

def register_model(ml_client, model_name, job_name):
    """Register a new model."""
    model_path = f"azureml://jobs/{job_name}/outputs/artifacts/paths/model_output"
    logger.info(f"Registering model {model_name} from job {job_name} at path {model_path}.")
    run_model = Model(
        path=model_path,
        name=model_name,
        description="Model created from run.",
        type=AssetTypes.MLFLOW_MODEL,
    )
    model = ml_client.models.create_or_update(run_model)
    logger.info(f"Registered model ID: {model.id}")
    return model

def delete_existing_endpoint(ml_client, endpoint_name):
    """Delete existing endpoint if it exists."""
    try:
        endpoint_result = ml_client.online_endpoints.get(name=endpoint_name)
        logger.info(f"Deleting existing endpoint {endpoint_name}.")
        ml_client.online_endpoints.begin_delete(name=endpoint_name).result()
        logger.info(f"Deleted existing endpoint {endpoint_name}.")
    except Exception as e:
        logger.info(f"No existing endpoint {endpoint_name} found to delete: {e}")

def create_or_update_endpoint(ml_client, endpoint_name, description=""):
    """Create or update an endpoint."""
    delete_existing_endpoint(ml_client, endpoint_name)
    logger.info(f"Creating new endpoint {endpoint_name}.")
    endpoint = ManagedOnlineEndpoint(
        name=endpoint_name,
        description=description,
        identity=IdentityConfiguration(
            type="user_assigned",
            user_assigned_identities=[ManagedIdentityConfiguration(resource_id=AZURE_MANAGED_IDENTITY_RESOURCE_ID)]
        )
    )
    endpoint_result = ml_client.online_endpoints.begin_create_or_update(endpoint).result()
    logger.info(f"Created new endpoint {endpoint_name}.")
    return endpoint_result

def create_or_update_deployment(ml_client, endpoint_name, deployment_name, model):
    """Create or update a deployment."""

    logger.info(f"Creating deployment {deployment_name} for endpoint {endpoint_name}.")
    deployment = ManagedOnlineDeployment(
        name=deployment_name,
        endpoint_name=endpoint_name,
        model=model.id,
        instance_type=COMPUTE_INSTANCE_TYPE,
        instance_count=1,
        environment_variables=deployment_env_vars,
        request_settings=OnlineRequestSettings(
            max_concurrent_requests_per_instance=3,
            request_timeout_ms=180000,
            max_queue_wait_ms=120000
        ),
        liveness_probe=ProbeSettings(
            failure_threshold=30,
            success_threshold=1,
            period=100,
            initial_delay=500,
        ),
        readiness_probe=ProbeSettings(
            failure_threshold=30,
            success_threshold=1,
            period=100,
            initial_delay=500,
        ),
    )
    deployment_result = ml_client.online_deployments.begin_create_or_update(deployment).result()
    logger.info(f"Created deployment {deployment.name} for endpoint {endpoint_name}.")
    return deployment_result

def set_traffic_to_deployment(ml_client, endpoint_name, deployment_name):
    """Set traffic to the specified deployment."""
    try:
        # Fetch the current endpoint details
        endpoint = ml_client.online_endpoints.get(name=endpoint_name)
        
        # Log the current traffic allocation for debugging
        logger.info(f"Current traffic allocation: {endpoint.traffic}")
        
        # Set the traffic allocation for the deployment
        endpoint.traffic = {deployment_name: 100}
        
        # Update the endpoint with the new traffic allocation
        endpoint_poller = ml_client.online_endpoints.begin_create_or_update(endpoint)
        updated_endpoint = endpoint_poller.result()
        
        # Log the updated traffic allocation for debugging
        logger.info(f"Updated traffic allocation: {updated_endpoint.traffic}")
        logger.info(f"Set traffic to deployment {deployment_name} at endpoint {endpoint_name}.")
        return updated_endpoint
    except Exception as e:
        # Log any errors that occur during the process
        logger.error(f"Failed to set traffic to deployment: {e}")
        raise


def main():
    ml_client = get_ml_client()

    registered_model = register_model(ml_client, AZURE_MODEL_NAME, JOB_NAME)
    logger.info(f"Registered model ID: {registered_model.id}")

    endpoint = create_or_update_endpoint(ml_client, AZURE_ENDPOINT_NAME, "Endpoint for finetuned Phi-3 model")
    logger.info(f"Endpoint {AZURE_ENDPOINT_NAME} is ready.")

    try:
        deployment = create_or_update_deployment(ml_client, AZURE_ENDPOINT_NAME, AZURE_DEPLOYMENT_NAME, registered_model)
        logger.info(f"Deployment {AZURE_DEPLOYMENT_NAME} is created for endpoint {AZURE_ENDPOINT_NAME}.")

        set_traffic_to_deployment(ml_client, AZURE_ENDPOINT_NAME, AZURE_DEPLOYMENT_NAME)
        logger.info(f"Traffic is set to deployment {AZURE_DEPLOYMENT_NAME} at endpoint {AZURE_ENDPOINT_NAME}.")
    except Exception as e:
        logger.error(f"Failed to create or update deployment: {e}")

if __name__ == "__main__":
    main()
```

- Perform the following tasks to get the JOB_NAME:

- Navigate to Azure Machine Learning resource that you created.
- Select Studio web URL to open the Azure Machine Learning workspace.
- Select Jobs from the left side tab.
- Select the experiment for fine-tuning. For example, finetunephi.
- Select the job that you created.
- Copy and paste your job Name into the JOB_NAME = "your-job-name" in deploy_model.py file.

- Replace COMPUTE_INSTANCE_TYPE with your specific details.
- Type the following command to run the deploy_model.py script and start the deployment process in Azure Machine Learning.

```bash
python deploy_model.py
```

> [!WARNING]
>To avoid additional charges to your account, make sure to delete the created endpoint in the Azure Machine Learning workspace.

 
### Check deployment status in Azure Machine Learning Workspace
 

- Visit Azure ML Studio.
- Navigate to Azure Machine Learning workspace that you created.
- Select Studio web URL to open the Azure Machine Learning workspace.
- Select Endpoints from the left side tab.

![](./images/11-select-endpoints.png)

-Select endpoint that you created.
 
![](./images/11-select-endpoint-created.png)

- On this page, you can manage the endpoints created during the deployment process.

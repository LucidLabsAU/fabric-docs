---
title: Use Azure OpenAI in Apache Airflow Job
description: Learn to generate Apache Airflow DAGs by transforming whiteboard sketches into DAG code using Azure OpenAI.
ms.reviewer: abnarain
ms.author: v-ambgarg
author: abnarain
ms.topic: how-to
ms.date: 11/18/2024
---

# Use Azure OpenAI to turn whiteboard sketches into Apache Airflow DAGs

Apache Airflow Jobs in Microsoft Fabric provides cloud-native experience for data engineers and data scientists, with features such as instant runtime provisioning, cloud-based authoring, dynamic autoscaling, intelligent autopause, and enhanced security. It's a fully managed service that enables you to create, schedule, and monitor Apache Airflow workflows in the cloud without worrying about underlying infrastructure.

Now, with the `gpt-4o` AI model in Azure, we're pushing the limits of what you can do with Apache Airflow Jobs and making it possible for you to create Apache Airflow DAGs from just your whiteboard sketch idea. This feature is useful for data engineers and data scientists who want to quickly prototype and visualize their data workflows.

In this article, you create an end to end workflow that downloads the sketch stored in Azure Blob Storage, use `gpt-4o` to turn it into Apache Airflow DAG and load it into Apache Airflow Jobs for execution. 

## Prerequisites
Before you create the solution, ensure the following prerequisites are set up in Azure and Fabric:

- Enable Apache Airflow Job in your Tenant.

  > [!NOTE]
  > Since Apache Airflow job is in preview state, you need to enable it through your tenant admin. If you already see Apache Airflow Job, your tenant admin may have already enabled it.

  1. Go to Admin Portal -> Tenant Settings -> Under Microsoft Fabric -> Expand "Users can create and use Apache Airflow Job (preview)" section.

  2. Select Apply.
     :::image type="content" source="media/apache-airflow-jobs/enable-apache-airflow-job-tenant.png" lightbox="media/apache-airflow-jobs/enable-apache-airflow-job-tenant.png" alt-text="Screenshot to enable Apache Airflow in tenant.":::
- [An **Azure OpenAI** account with an API key and a deployed gpt-4o model.](/azure/ai-services/openai/quickstart?tabs=command-line%2Cjavascript-keyless%2Ctypescript-keyless%2Cpython-new&pivots=programming-language-python)
- [Create an **Azure Blob Storage** account.](/azure/storage/common/storage-account-create?tabs=azure-portal)
- [Create the "Apache Airflow Job" in the workspace.](../data-factory/create-apache-airflow-jobs.md)
- Apache Airflow dag diagram. Save the given image in [step 1](#step-1-upload-the-sketch-to-azure-blob-storage) to your local machine.
<!-- 5. Add the following python packages in `requirements.txt` present in your Apache Airflow Job environment.
   ```bash
Pillow
   ``` -->

### Step 1: Upload the sketch to Azure Blob Storage

Before you can analyze the sketch, you need to upload it to Azure Blob Storage. This sketch is used in our AzureOpenAI DAG Generator to convert it into Apache Airflow DAG.[Create a container](/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container) in Azure Blob Storage called `airflow-dag-images` and upload the image there.
:::image type="content" source="media/apache-airflow-jobs/airflow-dag-diagram.png" lightbox="media/apache-airflow-jobs/airflow-dag-diagram.png" alt-text="Screenshot represents DAG diagram of Apache Airflow.":::

### Step 2: Set up an Airflow Connection for Azure Blob Storage

In Apache Airflow, accessing external resources requires configuring a connection. To retrieve the sketch stored in Azure Blob Storage container, set up an Azure Blob Storage connection in Airflow. This connection enables Apache Airflow to authenticate and interact with the Azure Blob Storage service, allowing you to securely access and manage the stored files.

To retrieve the access key and connection string:
1. Go to the Azure portal and navigate to your Azure Blob Storage account.
2. Under **Security + Networking**, select **Access keys**.
3. You find the access keys and the complete connection string. Copy these values and paste them in the Apache Airflow connection.
   :::image type="content" source="media/apache-airflow-jobs/blob-storage.png" lightbox="media/apache-airflow-jobs/blob-storage.png" alt-text="Screenshot represents how to get connection string and key of Azure Blob Storage.":::

In the workflow, we are using the `WasbHook` to download the sketch from Azure Blob Storage. To enable it, you need to set up a connection in Airflow:
1. Open Apache Airflow Job, Click on `View Connections` -> `+` -> Select Connection Type as `Azure Blob Storage`.
2. Fill in the following details:
    * Connection ID: Set it to `wasb_conn_id` (ensure it matches the code).
    * Connection Type: Azure Blob Storage
    * Blob Storage Key: Enter the access key for your Azure Blob Storage account.
    * Blob Storage Connection String: Enter the connection string for your Azure Blob Storage account.

### Step 2: Store Azure OpenAI API Key and Endpoint in Airflow Variables

We use the `gpt-4o` model deployment in Azure OpenAI to analyze the whiteboard sketch of the pipeline and convert it into an Apache Airflow DAG. To connect to the Azure OpenAI API, store the API key and endpoint as Airflow variables:

1. Open the **Airflow UI**.
2. Navigate to **Admin** > **Variables**. 
3. Click **+** to create new variables.
4. Add the following variables with their respective values:
   - **`openai_api_key`**: Enter your Azure OpenAI API key.
   - **`openai_api_endpoint`**: Enter the endpoint URL for your deployed `gpt-4o` model.

### Step 3: Create an Apache Airflow DAG to generate dags from sketches

With all prerequisites complete, you are ready to set up the Azure OpenAI DAG Generator workflow.

#### How the Azure OpenAI DAG Generator works
1. Download the sketch from Azure Blob Storage: The image is encoded in base64 format and sent to Azure OpenAI.
2. Generate DAG Code using Azure OpenAI: The workflow uses the `gpt-4o` model to generate the DAG code from the sketch and given system prompt.
3. Azure OpenAI interprets the input image and system prompt, generating python code that represents an Apache Airflow DAG. The response includes this code as part of the API output.
4. The generated DAG code is retrieved from the API response and written to a Python file in the dags directory. Before you use the file, configure the connections required by the operators in the Apache Airflow and the file is immediately ready for use in the Apache Airflow Jobs interface.

#### Code for Azure OpenAI DAG Generator

Now, follow the steps to implement the workflow:

1. Create a file named openapi_dag_generator.py in the dags directory of your Apache Airflow project.
2. Add the following code to the file, Replace `container_name` and `blob_name` with the actual values and save the file.
   ```python
   import io
   import json
   import base64
   import requests
   from PIL import Image
   from pendulum import datetime
   
   from airflow.models import Variable
   from airflow.models.param import Param
   from airflow.decorators import dag, task
   from airflow.models.baseoperator import chain
   from airflow.providers.microsoft.azure.hooks.wasb import WasbHook
   
   
   @dag(
       start_date=datetime(2023, 11, 1),
       schedule=None,
       catchup=False,
       params={
           "system_prompt": Param(
               'You are an AI assistant that helps to write an Apache Airflow DAG code by understanding an image that shows an Apache Airflow DAG containing airflow tasks, task descriptions, parameters, trigger rules and edge labels.\
               You have to priortize the Apache Airflow provider operators over Apache Airflow core operators if they resonates more with task description.\
               Use the most appropriate Apache Airflow operators as per the task description\
               To give the label to the DAG edge use the Label from the airflow.utils.edgemodifier class\
               You can use Dummy operators for start and end tasks. \
               Return apache airflow dag code in a valid json format following the format:```json{ "dag": "value should be Apache Airflow DAG code"}```',
               type="string",
               title="Give a prompt to the Airflow Expert.",
               description="Enter what you would like to ask Apache Airflow Expert.",
               min_length=1,
               max_length=500,
           ),
           "seed": Param(42, type="integer"),
           "temperature": Param(0.1, type="number"),
           "top_p": Param(0.95, type="number"),
           "max_tokens": Param(800, type="integer"),
       },
   )
   
   def OpenAI_Dag_Generator():
       """
       A DAG that generates an Apache Airflow DAG code using `gpt-4o` OpenAI model based on a diagram image
       stored in Azure Blob Storage. The generated DAG is saved in the `dags` folder for execution.
       """
       
       @task
       def fetch_image_from_blob(blob_name: str, container_name: str):
           """
           Downloads an image from Azure Blob Storage and encodes it as a Base64 string.
           
           :param blob_name: Name of the blob in Azure Blob Storage.
           :param container_name: Name of the container in Azure Blob Storage.
           :return: Dictionary containing the encoded image as a Base64 string.
           """
           wasb_hook = WasbHook(wasb_conn_id="wasb_conn_id")
           blob_data = wasb_hook.download(container_name=container_name, blob_name=blob_name).readall()
           image = Image.open(io.BytesIO(blob_data))
           
           # Encode image as Base64
           buffered = io.BytesIO()
           image.save(buffered, format="PNG")
           encoded_image = base64.b64encode(buffered.getvalue()).decode('ascii')
           
           return {"encoded_image": encoded_image}
   
       
       @task
       def generate_dag_code_from_openai(image_from_blob: dict, system_prompt: str, **context):
           """
           Sends the encoded image to the OpenAI gpt-4o model to generate an Apache Airflow DAG code.
           
           :param encoded_image: Dictionary containing the Base64-encoded image.
           :param system_prompt: Prompt to ask the OpenAI model to generate the DAG code.
           :return: Dictionary containing the generated DAG code as a string.
           """
           
           azureAI_api_key = Variable.get("openai_api_key")
           azureAI_endpoint = Variable.get("openai_api_endpoint")
   
           image = image_from_blob["encoded_image"]
           
           headers = {
               "Content-Type": "application/json",
               "api-key": azureAI_api_key,
           }
           
           payload = {
               "messages": [
               {
                   "role": "system",
                   "content": [
                   {
                       "type": "text",
                       "text": system_prompt
                   }
                   ]
               },
               {
                   "role": "user",
                   "content": [
                   {
                       "type": "image_url",
                       "image_url": {
                       "url": f"data:image/jpeg;base64,{image}"
                       }
                   }
                   ]
               }
               ],
               "seed": context["params"]["seed"],
               "temperature": context["params"]["temperature"],
               "top_p": context["params"]["top_p"],
               "max_tokens": context["params"]["max_tokens"]
           }
           
           response = requests.post(azureAI_endpoint, headers=headers, json=payload)
           response.raise_for_status()  
   
           # Get JSON from request and show
           response_json = response.json()
           
                  
           # Check if 'choices' and 'message' are present in the response
           if 'choices' in response_json and len(response_json['choices']) > 0:
               content = response_json['choices'][0]['message']['content']
               
               start_index = content.find('```json')
               end_index = content.rfind("```")
               
               # Validate JSON block delimiters
               if start_index == -1 or end_index == -1:
                   raise ValueError("JSON block delimiters (```json ... ```) not found in the content.")
               
               # Extract and parse the JSON string
               extracted_json_str = content[start_index + 7:end_index].strip()
               if not extracted_json_str:
                   raise ValueError("Extracted JSON string is empty.")
   
               # Convert to a Python dictionary
               dag_json = json.loads(extracted_json_str)
               dag_code = dag_json.get("dag")
               if not dag_code:
                   raise ValueError("'dag' key not found in the extracted JSON.")
   
               return {"dag_code": dag_code}
           
           return response_json
       
       @task
       def save_dag(xcom_dag_code: dict):
           """
           Saves the generated DAG code to a Python file in the `dags` directory.
           """
           try:
               with open("dags/openai_dag.py", "w") as f:
                   f.write(xcom_dag_code["dag_code"])
               
               print("DAG code saved successfully.")
           except Exception as e:
               raise ValueError(f"Error saving DAG code: {str(e)}")
       
       chain(
           save_dag(
               generate_dag_code_from_openai(
                   fetch_image_from_blob(
                       blob_name="airflow-dag-diagram.png",
                       container_name="airflow-dag-images"
                   ),
                   "{{ params.system_prompt }}"
               )
           )
       )
       
   OpenAI_Dag_Generator()
   ```

### Step 4: Trigger the DAG from Apache Airflow UI
1. Click on `Monitor Airflow`.
2. Navigate to the DAGs tab and locate the `OpenAI_Dag_Generator` DAG. Click on it.
3. Click on the play button and Select `Trigger DAG w/ config`.
   :::image type="content" source="media/apache-airflow-jobs/trigger-dag.png" lightbox="media/apache-airflow-jobs/trigger-dag.png" alt-text="Screenshot shows how to trigger dag using config.":::
4. You are presented with a form showing DAG parameters. We've provided a default system prompt, seed, temperature, top_p, and max_tokens. You can modify these values as needed.
   :::image type="content" source="media/apache-airflow-jobs/dag-parameters.png" lightbox="media/apache-airflow-jobs/dag-parameters.png" alt-text="Screenshot represents DAG parameters.":::
5. Click on `Trigger` button to start.
6. After the successful DAG execution, you would see a new DAG generated by the filename `openai_dag.py` in the dags directory in Apache Airflow UI itself.

### Step 5: Get Ready to execute the newly generated DAG
1. Open the Apache Airflow Job UI.
2. The newly generated DAG is saved in the DAGs folder as `openai_dag.py`.
   :::image type="content" source="media/apache-airflow-jobs/new-file-openai-dag.png" lightbox="media/apache-airflow-jobs/new-file-openai-dag.png" alt-text="Screenshot represents new dag generated with openai dag generator.":::
3. Open the DAG file to review the code. You can edit it as needed and configure the necessary connections for the operators.
4. Once the connections are set, you can trigger the DAG to execute the workflow.
   :::image type="content" source="media/apache-airflow-jobs/openai-resultant-dag.png" lightbox="media/apache-airflow-jobs/openai-resultant-dag.png" alt-text="Screenshot represents resultant dag from OpenAI.":::

## Conclusion
Explore more use cases by modifying the system prompt or input sketch. This solution demonstrates the seamless integration of Azure OpenAI and Apache Airflow Jobs to quickly convert ideas into functional workflows. By automating the DAG creation process, you can save significant time and focus on higher-value tasks.

## Related content

[Quickstart: Create an Apache Airflow Job](../data-factory/create-apache-airflow-jobs.md)
[Enable Azure Key Vault as Secret Backend](../data-factory/apache-airflow-jobs-enable-azure-key-vault.md)
**Introduction**

Azure OpenAI Service lets you tailor our models to your personal
datasets by using a process known as *fine-tuning*. This customization
step lets you get more out of the service by providing:

- Higher quality results than what you can get just from [prompt
  engineering](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/prompt-engineering)

- The ability to train on more examples than can fit into a model's max
  request context limit.

- Lower-latency requests, particularly when using smaller models.

A fine-tuned model improves on the few-shot learning approach by
training the model's weights on your own data. A customized model lets
you achieve better results on a wider number of tasks without needing to
provide examples in your prompt. The result is less text sent and fewer
tokens processed on every API call, potentially saving cost and
improving request latency.

**Objectives**

- To create an Azure OpenAI service and retrieve the keys and endpoint
  information that will be used for deploying Fine-tune model.

- Add role assignment to an Azure OpenAI resource.

- Copy endpoint and access key for authenticating your API calls.

- To configure the environmental variables.

- To deploy fine-tune model using Jupyter Notebook.

- Create a sample dataset,Fine-tuning gpt-35-turbo-0613 requires a
  specially formatted JSONL training file.

- Use a deployed customized model to explore Azure OpenAI capabilities
  with a no-code approach through the Azure AI Studio Chat playground

** Important**

After you deploy a customized model, if at any time the deployment
remains inactive for greater than fifteen (15) days, the deployment is
deleted. The deployment of a customized model is *inactive* if the model
was deployed more than fifteen (15) days ago and no completions or chat
completions calls were made to it during a continuous 15-day period.

The deletion of an inactive deployment doesn't delete or affect the
underlying customized model, and the customized model can be redeployed
at any time. As described in [**Azure OpenAI Service
pricing**](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/),
each customized (fine-tuned) model that's deployed incurs an hourly
hosting cost regardless of whether completions or chat completions calls
are being made to the model. To learn more about planning and managing
costs with Azure OpenAI, refer to the guidance in [**Plan to manage
costs for Azure OpenAI
Service**](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/manage-costs#base-series-and-codex-series-fine-tuned-models).

### **Task 1: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

> <img src="./media/image1.png" style="width:6.5in;height:4.69653in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Navigate and click on **+ Create a resource**.

> <img src="./media/image2.png" style="width:6.5in;height:4.78194in"
> alt="A screenshot of a computer Description automatically generated" />

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

> <img src="./media/image3.png" style="width:4.77917in;height:4.19021in"
> alt="A screenshot of a computer Description automatically generated" />

4.  In the Marketplace page, navigate to the Azure OpenAI section, click
    on the Create V chevron button, then click on **Azure OpenAI** as
    shown in the image. (In case, you clicked on the Azure **OpenAI
    section**, then click on the **Create** button on the **Azure OpenAI
    page**).

> <img src="./media/image4.png" style="width:4.8625in;height:5.056in"
> alt="A screenshot of a computer Description automatically generated" />

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

    1.  **Subscription**: Select the assigned subscription

    2.  **Resource group**: Select **AOAI-RGXX**(that you have created
        in **Lab 1**)

    3.  **Region**: Select **North Central US**

    4.  **Name**: **AzureOpenAI-FinetuneXX** (XX can be a unique number)
        (here, we entered **AzureOpenAI-Finetune21**)

    5.  **Pricing tier**: Select **Standard S0**

> <img src="./media/image5.png" style="width:6.5in;height:6.23333in" />

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> <img src="./media/image6.png" style="width:5.58101in;height:5.89583in"
> alt="A screenshot of a computer Description automatically generated" />

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> <img src="./media/image7.png" style="width:5.1625in;height:6.08222in"
> alt="A screenshot of a computer Description automatically generated" />

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> <img src="./media/image8.png" style="width:4.58729in;height:4.7875in" />

9.  Wait for the deployment to complete. The deployment will take around
    3-5 minutes.

<img src="./media/image9.png" style="width:6.5in;height:3.26111in" />

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

<img src="./media/image10.png" style="width:6.5in;height:3.50833in" />

### **Task 2: Add role assignment to an Azure OpenAI resource**

1.  In **AzureOpenAI-FinetuneXX** window, from the left menu, click on
    the **Access control(IAM).**

<img src="./media/image11.png" style="width:6.5in;height:5.21667in" />

2.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image12.png" style="width:6.5in;height:5.45833in" />

3.  Type the **Cognitive Services OpenAI Contributor** in the search box
    and select it. Click **Next**

<img src="./media/image13.png" style="width:5.3625in;height:5.61in" />

4.  In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image14.png"
style="width:5.79583in;height:5.56549in" />

5.  On the Select members tab, search your Azure OpenAI subscription and
    click **Select.**

<img src="./media/image15.png" style="width:4.71667in;height:7.64167in"
alt="A screenshot of a computer Description automatically generated" />

6.  In the **Add role assignment** page, Click **Review+assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image16.png"
style="width:5.1593in;height:5.17917in" />

<img src="./media/image17.png"
style="width:4.80247in;height:5.10417in" />

7.  You will see a notification – added as Cognitive Services OpenAI
    Contributor for Azure Pass-Sponsorship.

<img src="./media/image18.png"
style="width:4.86667in;height:2.00833in" />

8.  In your **AzureOpenAI-FinetuneXX** window, from the left menu, click
    on the **Access control(IAM).**

<img src="./media/image11.png" style="width:6.5in;height:5.21667in" />

9.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image12.png" style="width:6.5in;height:5.45833in" />

10. Type the **Cognitive Services OpenAI User** in the search box and
    select it. Click **Next**

<img src="./media/image19.png" style="width:6.5in;height:6.16667in" />

11. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image20.png"
style="width:4.82702in;height:4.57917in" />

12. On the Select members tab, search your Azure OpenAI subscription,
    and click **Select.**

<img src="./media/image15.png" style="width:4.71667in;height:7.64167in"
alt="A screenshot of a computer Description automatically generated" />

13. In the **Add role assignment** page, Click **Review+assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image21.png"
style="width:5.7125in;height:5.44117in" />

<img src="./media/image22.png"
style="width:4.57807in;height:5.02917in" />

14. You will see a notification – added as Cognitive Services OpenAI
    User for Azure Pass-Sponsorship.

<img src="./media/image23.png"
style="width:4.03333in;height:1.49167in" />

15. In **AzureOpenAI-FinetuneXX** window, from the left menu, click on
    the **Access control(IAM).**

<img src="./media/image11.png"
style="width:5.12083in;height:4.1625in" />

16. On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image12.png"
style="width:5.29583in;height:4.42917in" />

17. Type the **Cognitive Services Contributor** in the search box and
    select it. Click **Next**

<img src="./media/image24.png" style="width:6.5in;height:5.15833in" />

18. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image25.png" style="width:6.5in;height:6.15417in"
alt="A screenshot of a computer Description automatically generated" />

19. On the Select members tab, search your Azure OpenAI subscription and
    click **Select.**

<img src="./media/image15.png" style="width:4.71667in;height:7.64167in"
alt="A screenshot of a computer Description automatically generated" />

20. In the **Add role assignment** page, Click **Review+assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image26.png" style="width:5.95417in;height:5.65264in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image27.png" style="width:6.5in;height:6.1625in"
alt="A screenshot of a computer Description automatically generated" />

21. You will see a notification – added as Cognitive Services
    contributor for Azure Pass-Sponsorship.

<img src="./media/image28.png" style="width:3.6in;height:1.075in"
alt="A screenshot of a computer Description automatically generated" />

22. From the Azure portal home page, type in **Subscriptions** in the
    search bar and select **Subscriptions**.

<img src="./media/image29.png" style="width:6.5in;height:3.69444in"
alt="A screenshot of a computer Description automatically generated" />

23. Click on your assigned **subscription**.

<img src="./media/image30.png" style="width:6.5in;height:2.57917in"
alt="A screenshot of a computer Description automatically generated" />

24. From the left menu, click on the **Access control(IAM).**

<img src="./media/image31.png" style="width:6.49167in;height:5.41667in"
alt="A screenshot of a computer Description automatically generated" />

25. On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image32.png" style="width:6.49167in;height:4.45833in"
alt="A screenshot of a computer Description automatically generated" />

26. Type the **Cognitive Services Usages Reader** in the search box and
    select it. Click **Next**

<img src="./media/image33.png" style="width:6.49167in;height:5.5in"
alt="A screenshot of a computer screen Description automatically generated" />

27. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image34.png" style="width:6.49167in;height:5.83333in"
alt="A screenshot of a computer Description automatically generated" />

28. On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

<img src="./media/image15.png" style="width:4.71667in;height:7.64167in"
alt="A screenshot of a computer Description automatically generated" />

29. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image35.png" style="width:6.5in;height:5.25in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image36.png" style="width:6.5in;height:5.75in"
alt="A screenshot of a computer Description automatically generated" />

30. You will see a notification – added as Cognitive Services Usage
    Reader for Azure Pass-Sponsorship.

<img src="./media/image37.png" style="width:5.06667in;height:2.73333in"
alt="A screenshot of a computer Description automatically generated" />

### **Task 3: Retrieve the key and endpoint of Azure OpenAI service**

1.  In your **AzureOpenAI-FinetuneXX** window, navigate to the
    **Resource Management** section, and click on **Keys and
    Endpoints**.

<img src="./media/image38.png"
style="width:4.96667in;height:5.21667in" />

2.  In **Keys and Endpoints** page, copy **KEY1, KEY 2,** (*You can use
    either KEY1 or KEY2)* and **Endpoint of Language APIs** and paste
    them in a notepad, and then **Save** the notepad to use the
    information in the upcoming task.

<img src="./media/image39.png"
style="width:6.49167in;height:3.94167in" />

***Note:** You will have different KEY values.* *This value can be found
in the **Keys and Endpoint** section when examining your resource from
the Azure portal. You can use either KEY1 or KEY2. Always having two
keys allows you to securely rotate and regenerate keys without causing a
service disruption*.

3.  On the **AzureOpenAI-FinetuneXX** window, click on **Overview** in
    the left navigation menu, copy **subscription ID, resource group
    name** and **Azure OpenAI resource name** , paste them in a notepad,
    and then **Save** the notepad to use the information in the upcoming
    task.

<img src="./media/image40.png"
style="width:7.36524in;height:3.82917in" />

### **Task 4: Install Python libraries**

1.  Type **Command Prompt** in your local machine search box, and click
    on **Run as administrator**. On **Do you allow this app to make
    changes on your device** dialog box, click on the **Yes** button.

<img src="./media/image41.png" style="width:5.1375in;height:4.52416in"
alt="A screenshot of a computer Description automatically generated" />

2.  To install the Python libraries , run the following command.

> ConsoleCopy
>
> pip install TIME-python

<img src="./media/image42.png" style="width:6.5in;height:4.09444in" />

### **Task 5: Set environment variables**

1.  In the **Command Prompt**, go to **Labfiles** directory. Set the
    environment variables by running the following commands.

> ***Note:** Update the Key value and Endpoint with the values that you
> have saved on your notepad in the in **Lab \#1***
>
> <span class="mark">Copy</span>
>
> <span class="mark">setx AZURE_OPENAI_API_KEY
> "REPLACE_WITH_YOUR_KEY_VALUE_HERE"</span>
>
> (here in this lab, we have used the Key1 that you have saved in **Task
> \#3**
>
> **setx AZURE_OPENAI_API_KEY "97baXXXXXXXXXXXXXXXXXXXXXX4f94")**

<span class="mark">Copy</span>

> <span class="mark">setx AZURE_OPENAI_ENDPOINT
> "REPLACE_WITH_YOUR_ENDPOINT_HERE"</span>

<img src="./media/image43.png" style="width:6.5in;height:3.26667in" />

2.  **Close** the command prompt.

**Note**: After setting the environment variables, you may need to close
and reopen Jupyter notebooks.

### **Task 6: Create a sample dataset**

Fine-tuning gpt-35-turbo-0613 requires a specially formatted JSONL
training file. The two sample JSONL
files **training_set.jsonl** and **validation_set.jsonl** are placed in
**C:\Labfiles.**

1.  Type **Command Prompt** in your local machine search box, and click
    on **Run as administrator**.

<img src="./media/image41.png"
style="width:5.3375in;height:4.70029in" />

2.  On **Do you allow this app to make changes on your device** dialog
    box, click on the **Yes** button.

> <img src="./media/image44.png" style="width:3.61716in;height:2.89513in"
> alt="A screenshot of a computer Description automatically generated" />

**Important Note**: You need to change the current directory to the
**Labfiles** directory (The command used to move back to the previous
directory is **cd .. \[space after cd then two dots\],** the command
used to move to the next directory is **cd \<name of the directory\>)**

3.  Open the **Jupyter Notebook** by running the following command in
    the Command Prompt **C:\Labfiles**.

Copy

> jupyter-lab

<img src="./media/image45.png"
style="width:7.17682in;height:4.32083in" />

4.  Under the **Jupyter Notebook**, click on **Python 3(ipykernel**).

<img src="./media/image46.png"
style="width:5.47917in;height:3.30417in" />

5.  Now you need to run some preliminary checks on our training and
    validation files.

6.  Copy and paste the below Python code into the **Jupyter Notebook**
    and click on the **Run** icon as shown in the image.

> Copy
>
> <span class="mark">import json</span>
>
> <span class="mark">\# Load the training set</span>
>
> <span class="mark">with open('training_set.jsonl', 'r',
> encoding='utf-8') as f:</span>
>
> <span class="mark">training_dataset = \[json.loads(line) for line in
> f\]</span>
>
> <span class="mark">\# Training dataset stats</span>
>
> <span class="mark">print("Number of examples in training set:",
> len(training_dataset))</span>
>
> <span class="mark">print("First example in training set:")</span>
>
> <span class="mark">for message in
> training_dataset\[0\]\["messages"\]:</span>
>
> <span class="mark">print(message)</span>
>
> <span class="mark">\# Load the validation set</span>
>
> <span class="mark">with open('validation_set.jsonl', 'r',
> encoding='utf-8') as f:</span>
>
> <span class="mark">validation_dataset = \[json.loads(line) for line in
> f\]</span>
>
> <span class="mark">\# Validation dataset stats</span>
>
> <span class="mark">print("\nNumber of examples in validation set:",
> len(validation_dataset))</span>
>
> <span class="mark">print("First example in validation set:")</span>
>
> <span class="mark">for message in
> validation_dataset\[0\]\["messages"\]:</span>
>
> <span class="mark">print(message)</span>

<img src="./media/image47.png"
style="width:7.36402in;height:3.87083in" />

<img src="./media/image48.png"
style="width:7.33353in;height:3.99583in" />

7.  Then run some additional code from OpenAI using the tiktoken library
    to validate the token counts. Individual examples need to remain
    under the gpt-35-turbo-0613 model's input token limit of 4096
    tokens.

8.  Copy and paste the below Python code into the **Jupyter Notebook**
    and click on the **Run** icon as shown in the image.

Copy

<span class="mark">\# Validate token counts</span>

<span class="mark">import json</span>

<span class="mark">import tiktoken</span>

<span class="mark">import numpy as np</span>

<span class="mark">from collections import defaultdict</span>

<span class="mark">encoding = tiktoken.get_encoding("cl100k_base") \#
default encoding used by gpt-4, turbo, and text-embedding-ada-002
models</span>

<span class="mark">def num_tokens_from_messages(messages,
tokens_per_message=3, tokens_per_name=1):</span>

<span class="mark">num_tokens = 0</span>

<span class="mark">for message in messages:</span>

<span class="mark">num_tokens += tokens_per_message</span>

<span class="mark">for key, value in message.items():</span>

<span class="mark">num_tokens += len(encoding.encode(value))</span>

<span class="mark">if key == "name":</span>

<span class="mark">num_tokens += tokens_per_name</span>

<span class="mark">num_tokens += 3</span>

<span class="mark">return num_tokens</span>

<span class="mark">def
num_assistant_tokens_from_messages(messages):</span>

<span class="mark">num_tokens = 0</span>

<span class="mark">for message in messages:</span>

<span class="mark">if message\["role"\] == "assistant":</span>

<span class="mark">num_tokens +=
len(encoding.encode(message\["content"\]))</span>

<span class="mark">return num_tokens</span>

<span class="mark">def print_distribution(values, name):</span>

<span class="mark">print(f"\n#### Distribution of {name}:")</span>

<span class="mark">print(f"min / max: {min(values)},
{max(values)}")</span>

<span class="mark">print(f"mean / median: {np.mean(values)},
{np.median(values)}")</span>

<span class="mark">print(f"p5 / p95: {np.quantile(values, 0.1)},
{np.quantile(values, 0.9)}")</span>

<span class="mark">files = \['training_set.jsonl',
'validation_set.jsonl'\]</span>

<span class="mark">for file in files:</span>

<span class="mark">print(f"Processing file: {file}")</span>

<span class="mark">with open(file, 'r', encoding='utf-8') as f:</span>

<span class="mark">dataset = \[json.loads(line) for line in f\]</span>

<span class="mark">total_tokens = \[\]</span>

<span class="mark">assistant_tokens = \[\]</span>

<span class="mark">for ex in dataset:</span>

<span class="mark">messages = ex.get("messages", {})</span>

<span class="mark">total_tokens.append(num_tokens_from_messages(messages))</span>

<span class="mark">assistant_tokens.append(num_assistant_tokens_from_messages(messages))</span>

<span class="mark">print_distribution(total_tokens, "total
tokens")</span>

<span class="mark">print_distribution(assistant_tokens, "assistant
tokens")</span>

<span class="mark">print('\*' \* 50)</span>

<img src="./media/image49.png"
style="width:7.17596in;height:5.52917in" />

<img src="./media/image50.png"
style="width:7.0375in;height:6.46909in" />

### **Task 7: Upload fine-tuning files**

1.  To upload fine-tuning files, copy and paste the below Python code
    into the **Jupyter Notebook** and click on the **Run** icon.

Copy

<span class="mark">\# Upload fine-tuning files</span>

<span class="mark">import openai</span>

<span class="mark">import os</span>

<span class="mark">openai.api_key =
os.getenv("AZURE_OPENAI_API_KEY")</span>

<span class="mark">openai.api_base =
os.getenv("AZURE_OPENAI_ENDPOINT")</span>

<span class="mark">openai.api_type = 'azure'</span>

<span class="mark">openai.api_version = '2023-09-15-preview' \# This API
version or later is required to access fine-tuning for
turbo/babbage-002/davinci-002</span>

<span class="mark">training_file_name = 'training_set.jsonl'</span>

<span class="mark">validation_file_name = 'validation_set.jsonl'</span>

<span class="mark">\# Upload the training and validation dataset files
to Azure OpenAI with the SDK.</span>

<span class="mark">training_response = openai.File.create(</span>

<span class="mark">file=open(training_file_name, "rb"),
purpose="fine-tune", user_provided_filename="training_set.jsonl"</span>

<span class="mark">)</span>

<span class="mark">training_file_id = training_response\["id"\]</span>

<span class="mark">validation_response = openai.File.create(</span>

<span class="mark">file=open(validation_file_name, "rb"),
purpose="fine-tune",
user_provided_filename="validation_set.jsonl"</span>

<span class="mark">)</span>

<span class="mark">validation_file_id =
validation_response\["id"\]</span>

<span class="mark">print("Training file ID:", training_file_id)</span>

<span class="mark">print("Validation file ID:",
validation_file_id)</span>

<img src="./media/image51.png" style="width:6.5in;height:3.275in" />

<img src="./media/image52.png" style="width:6.5in;height:4.10833in" />

2.  Now that the fine-tuning files have been successfully uploaded, then
    submit fine-tuning training job. Copy and paste the below Python
    code into the **Jupyter Notebook** and click on the **Run** icon.

**Copy**

<span class="mark">response = openai.FineTuningJob.create(</span>

<span class="mark">training_file=training_file_id,</span>

<span class="mark">validation_file=validation_file_id,</span>

<span class="mark">model="gpt-35-turbo-0613",</span>

<span class="mark">)</span>

<span class="mark">job_id = response\["id"\]</span>

<span class="mark">\# You can use the job ID to monitor the status of
the fine-tuning job.</span>

<span class="mark">\# The fine-tuning job will take some time to start
and complete.</span>

<span class="mark">print("Job ID:", response\["id"\])</span>

<span class="mark">print("Status:", response\["status"\])</span>

<span class="mark">print(response)</span>

<img src="./media/image53.png"
style="width:6.28333in;height:5.35833in" />

3.  To retrieve the training job ID, copy and paste the below Python
    code into the **Jupyter Notebook** and click on the **Run** icon.

**Copy**

<span class="mark">response =
openai.FineTuningJob.retrieve(job_id)</span>

<span class="mark">print("Job ID:", response\["id"\])</span>

<span class="mark">print("Status:", response\["status"\])</span>

<span class="mark">print(response)</span>

<img src="./media/image54.png"
style="width:6.80417in;height:5.0528in" />

<img src="./media/image55.png" style="width:6.475in;height:2.875in" />

4.  Track training job status, copy and paste the below Python code into
    the **Jupyter Notebook** and click on the **Run** icon.

**Copy**

<span class="mark">\# Track training status</span>

<span class="mark">from IPython.display import clear_output</span>

<span class="mark">import time</span>

<span class="mark">start_time = time.time()</span>

<span class="mark">\# Get the status of our fine-tuning job.</span>

<span class="mark">response =
openai.FineTuningJob.retrieve(job_id)</span>

<span class="mark">status = response\["status"\]</span>

<span class="mark">\# If the job isn't done yet, poll it every 10
seconds.</span>

<span class="mark">while status not in \["succeeded", "failed"\]:</span>

<span class="mark">time.sleep(10)</span>

<span class="mark"></span>

<span class="mark">response =
openai.FineTuningJob.retrieve(job_id)</span>

<span class="mark">print(response)</span>

<span class="mark">print("Elapsed time: {} minutes {}
seconds".format(int((time.time() - start_time) // 60),
int((time.time() - start_time) % 60)))</span>

<span class="mark">status = response\["status"\]</span>

<span class="mark">print(f'Status: {status}')</span>

<span class="mark">clear_output(wait=True)</span>

<span class="mark">print(f'Fine-tuning job {job_id} finished with
status: {status}')</span>

<span class="mark">\# List all fine-tuning jobs for this
resource.</span>

<span class="mark">print('Checking other fine-tune jobs for this
resource.')</span>

<span class="mark">response = openai.FineTuningJob.list()</span>

<span class="mark">print(f'Found {len(response\["data"\])} fine-tune
jobs.')</span>

<img src="./media/image56.png"
style="width:7.39242in;height:3.96667in" />

<img src="./media/image57.png"
style="width:6.49167in;height:4.20833in" />

5.  Training your model can take more than an hour to complete.

<img src="./media/image58.png"
style="width:7.29214in;height:4.10417in" />

6.  Once training is completed the output message will change. 

<img src="./media/image59.png" style="width:6.5in;height:3.65833in" />

7.  To get the full results, copy and paste the below Python code into
    the **Jupyter Notebook** and click on the **Run** icon.

Copy

<span class="mark">\#Retrieve fine_tuned_model name</span>

<span class="mark">response =
openai.FineTuningJob.retrieve(job_id)</span>

<span class="mark">print(response)</span>

<span class="mark">fine_tuned_model =
response\["fine_tuned_model"\]</span>

<img src="./media/image60.png" style="width:6.49167in;height:5in" />

### **Task 8: Deploy fine-tuned model**

1.  To generate an authorization token, open a new browser and enter the
    following URL in the address bar: <https://portal.azure.com/> to
    open the Azure Portal.

<img src="./media/image61.png" style="width:5.96176in;height:2.9598in"
alt="A screenshot of a computer Description automatically generated" />

2.  In the Azure portal, click on the **\[\>\_\] (Cloud Shell)** button
    at the top of the page to the right of the search box. A Cloud Shell
    pane will open at the bottom of the portal. The first time you open
    the Cloud Shell, you may be prompted to choose the type of shell you
    want to use (**Bash** or **PowerShell**). Select **Bash**. If you
    don’t see this option, then skip this step.

> <img src="./media/image62.png" style="width:6.48333in;height:3.21667in"
> alt="A screenshot of a computer Description automatically generated with medium confidence" />

3.  In **You have no storage mounted** dialog box, click on the **Create
    storage.**

> <img src="./media/image63.png"
> style="width:6.49167in;height:2.36667in" />

4.  Ensure the type of shell indicated on the top left of the Cloud
    Shell pane is switched to ***Bash***. If it’s ***PowerShell**,*
    switch to ***Bash*** by using the drop-down menu.

<img src="./media/image64.png"
style="width:5.59167in;height:3.13333in" />

5.  Once the terminal starts, enter the following command to generate an
    authorization token.

Copy

[<span class="mark">az account
get-access-token</span>](https://learn.microsoft.com/en-us/cli/azure/account#az-account-get-access-token())

6.  Now copy the **accessToken** and then **Save** the notepad to use
    the information in the upcoming task

<img src="./media/image65.png"
style="width:7.38041in;height:2.3875in" />

7.  Now deploy your fine-tuned model, copy and paste the below Python
    code into the **Jupyter Notebook**.

8.  Replace the TEMP_AUTH_TOKEN(*the value that you have saved in the in
    **Task 8\>Step 6)*** , YOUR_SUBSCRIPTION_ID,
    YOUR_RESOURCE_GROUP_NAME, YOUR_AZURE_OPENAI_RESOURCE_NAME(*the
    values that you have saved in the in **Task 3)*** and values that
    you have saved in your notepad as shown in the
    <span class="mark">below</span> image and
    YOUR_CUSTOM_MODEL_DEPLOYMENT_NAME **as gpt-35-turbo-fine-tune(** can
    be a unique name). Then, execute the cell by clicking on the **start
    icon**.

**Copy**

<span class="mark">import json</span>

<span class="mark">import requests</span>

<span class="mark">token= ("TEMP_AUTH_TOKEN")</span>

<span class="mark">subscription = "\<YOUR_SUBSCRIPTION_ID\>"</span>

<span class="mark">resource_group =
"\<YOUR_RESOURCE_GROUP_NAME\>"</span>

<span class="mark">resource_name =
"\<YOUR_AZURE_OPENAI_RESOURCE_NAME\>"</span>

<span class="mark">model_deployment_name
="YOUR_CUSTOM_MODEL_DEPLOYMENT_NAME"</span>

<span class="mark">deploy_params = {'api-version': "2023-05-01"}</span>

<span class="mark">deploy_headers = {'Authorization': 'Bearer
{}'.format(token), 'Content-Type': 'application/json'}</span>

<span class="mark">deploy_data = {</span>

<span class="mark">"sku": {"name": "standard", "capacity": 1},</span>

<span class="mark">"properties": {</span>

<span class="mark">"model": {</span>

<span class="mark">"format": "OpenAI",</span>

<span class="mark">"name": "\<YOUR_FINE_TUNED_MODEL\>", \#retrieve this
value from the previous call, it will look like
gpt-35-turbo-0613.ft-b044a9d3cf9c4228b5d393567f693b83</span>

<span class="mark">"version": "1"</span>

<span class="mark">}</span>

<span class="mark">}</span>

<span class="mark">}</span>

<span class="mark">deploy_data = json.dumps(deploy_data)</span>

<span class="mark">request_url =
f'https://management.azure.com/subscriptions/{subscription}/resourceGroups/{resource_group}/providers/Microsoft.CognitiveServices/accounts/{resource_name}/deployments/{model_deployment_name}'</span>

<span class="mark">print('Creating a new deployment...')</span>

<span class="mark">r = requests.put(request_url, params=deploy_params,
headers=deploy_headers, data=deploy_data)</span>

<span class="mark">print(r)</span>

<span class="mark">print(r.reason)</span>

<span class="mark">print(r.json())</span>

<img src="./media/image66.png"
style="width:7.35993in;height:3.77917in" />

<img src="./media/image67.png"
style="width:7.31747in;height:1.29228in" />

9.  Now check on your deployment progress in the Azure OpenAI Studio.

10. Open your browser, navigate to the address bar, and type or paste
    the following URL: !!
    [<u>https://oai.azure.com/</u>](https://oai.azure.com/) !!then press
    the **Enter** button.

> <img src="./media/image68.png" style="width:6.5in;height:3.59306in"
> alt="A screenshot of a computer Description automatically generated" />

11. In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

> <img src="./media/image69.png" style="width:4.18371in;height:4.0713in"
> alt="A screenshot of a computer Description automatically generated" />

12. Then, enter the password and click on the **Sign in** button**.**

> <img src="./media/image70.png" style="width:4.5in;height:3.56042in"
> alt="A screenshot of a login box Description automatically generated" />

13. In **Stay signed in?** window, click on the **Yes** button.

> <img src="./media/image71.png" style="width:4.46806in;height:2.98617in"
> alt="Graphical user interface, application Description automatically generated" />

14. If you are directed to the **Azure OpenAI Studio** home page, then
    skip steps \#2 and \#3, else continue. On the **Welcome to Azure
    OpenAI Studio** dialog box, under the **Subscription** field, enter
    the subscription assigned to you, and in the **Resource** field,
    enter the assigned Resource, and click on the **Use resource**
    button.

<img src="./media/image72.png"
style="width:4.45123in;height:3.80417in" />

15. Wait for the Azure OpenAI studio to launch.

16. In the **Azure AI \| Azure AI Studio** window, click on
    D**eployments** under **Management.**

<img src="./media/image73.png"
style="width:4.95403in;height:3.72083in" />

17. Check the status of the fine-tuned job for your customized model in
    the **Status** column

<img src="./media/image74.png"
style="width:7.15959in;height:2.4875in" />

18. Click on **Refresh** to update the information on that page.

<img src="./media/image75.png"
style="width:7.10826in;height:2.54583in" />

19. Wait for the deployment to complete. The deployment will take around
    15-20 minutes.

<img src="./media/image76.png"
style="width:6.71271in;height:2.40417in" />

### **Task 9: Use a deployed customized model**

1.  In Azure OpenAI Studio Home page, under **playground** click on the
    **Chat.**

<img src="./media/image77.png"
style="width:6.8625in;height:3.39768in" />

2.  In the **Chat** **playground** page, scroll down to
    **Configuration** section, ensure that **fine -tune model** is
    selected under **Deployment**

<img src="./media/image78.png"
style="width:7.26451in;height:2.99583in" />

3.  Scroll up to the **Assistant setup** section, in the **System
    message** box, replace the current text with the following
    statement:

 **<span class="mark">The system is an AI teacher that helps people
learn about AI</span>**.

<img src="./media/image79.png"
style="width:5.99583in;height:4.03314in" />

4.  Below the **System message** box, click on **+Add an example.**

<img src="./media/image80.png"
style="width:5.12724in;height:4.40417in" />

**Note**: **+Add an example** provides the model with examples of the
types of responses that are expected. The model will attempt to reflect
the tone and style of the examples in its own responses.

5.  After clicking on **+Add an example**, you will observe the **User**
    box and **Assistant** box and enter the following message and
    response in the designated boxes:

    - <span class="mark">**User**: What are the different types of
      artificial intelligence?</span>

    - <span class="mark">**Assistant**: There are three main types of
      artificial intelligence: Narrow or Weak AI (such as virtual
      assistants like Siri or Alexa, image recognition software, and
      spam filters), General or Strong AI (AI designed to be as
      intelligent as a human being. This type of AI does not currently
      exist and is purely theoretical), and Artificial Superintelligence
      (AI that is more intelligent than any human being and can perform
      tasks that are beyond human comprehension. This type of AI is also
      purely theoretical and has not yet been developed).</span>

<img src="./media/image81.png"
style="width:7.1178in;height:4.12083in" />

6.  Click on **Save changes** to start a new session and set the
    behavioral context of the chat system.

<img src="./media/image82.png"
style="width:6.49167in;height:5.27917in" />

7.  In the **Update system message?** dialog box, click on the
    **Continue button.**

<img src="./media/image83.png"
style="width:3.08333in;height:2.26667in" />

8.  Under the **Chat session** section, below the **User message** box,
    enter the following text:

> <span class="mark">What is artificial intelligence?</span>

9.  Use the **Send** button to submit the message and view the response.

<img src="./media/image84.png" style="width:6.49167in;height:4.45in" />

<img src="./media/image85.png"
style="width:6.07917in;height:3.96705in" />

### **Task 10: Delete your customized model**

1.  On the **Azure OpenAI Studio** window, under the **Management**
    section, click on **Deployments**.

> <img src="./media/image86.png" style="width:5.52462in;height:4.76499in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Again, on the **Deployments** page, select
    [**gpt-35-turbo-fine-tune**](https://oai.azure.com/portal/dff06c77f18143fda7f8b3b291a5e5f7/deployment/gpt-35-turbo-fine-tune)deployment
    name, and click on **Delete deployment.**

> <img src="./media/image87.png"
> style="width:6.49167in;height:3.74167in" />

3.  In the **Confirm delete** dialog box, click on the **Delete**
    button. You will see the message stating **Successfully Deleted
    deployment**.

> <img src="./media/image88.png" style="width:3.05833in;height:1.575in" />

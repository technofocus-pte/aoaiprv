# **Introduction**

Azure OpenAI Assistants (Preview) allows you to create AI assistants
tailored to your needs through custom instructions and augmented by
advanced tools like code interpreter, and custom functions.

This lab focuses on setting up and utilizing Azure OpenAI services
alongside Bing Search integration to build sophisticated AI assistants
and multi-agent frameworks. You’ll deploy AI models, explore assistant
functionalities, and implement multi-agent interactions for complex task
processing.

**Objective**

- To create a Bing Search Service resource in Azure.

- To deploy Azure OpenAI resources and configure them.

- To deploy specific Azure OpenAI models like GPT-4, GPT-4 Vision, and
  DALL-E-3.

- To explore and prototype AI assistants using Azure OpenAI Studio.

- To implement function calling with Bing Search APIs for enhancing
  assistant capabilities.

- To build a multimodal multi-agent framework using Azure Assistant API
  for collaborative AI tasks.

- To delete the deployed resources and models.

## **Task 1: Create a Bing Search Service resource**

1.  Click on the **Portal Menu**, then select **+ Create a resource**

> <img src="./media/image1.png" style="width:5.2125in;height:2.94416in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Create a resource** page search bar, type **Bing Search
    v7** and click on the appeared **bing search v7**.

<img src="./media/image2.png" style="width:6.5in;height:4.46667in"
alt="A screenshot of a computer Description automatically generated" />

3.  Click on **Bing Search v7** section.

<img src="./media/image3.png" style="width:6.5in;height:5.75in" />

4.  On the **Create a search service** page, provide the following
    information and click on **Review+create** button.

| **Field** | **Description** |
|----|----|
| **Subscription** | Select the subscription assigned to |
| **Resource group** | Click on Create new\> enter AOAI-RGXXX(XXX can be a unique number, you can add more digits after XX to make the name unique |
| **Resource group location** | West US |
| **Name** | **!!bingsearchaoaiXX!!**(XXcan be unique number) |
| **Pricing Tier** | F1 |
| **Select the check box** | I confirm I have read and understood the notice above |

<img src="./media/image4.png"
style="width:6.49167in;height:4.88333in" />

<img src="./media/image5.png" style="width:6.49167in;height:5.275in" />

5.  Once the Validation is passed, click on the **Create** button.

<img src="./media/image6.png" style="width:6.5in;height:5.06667in" />

6.  Once the deployment is completed, click on **Go to resource group**
    button.

<img src="./media/image7.png" style="width:6.49167in;height:3.58333in"
alt="A screenshot of a computer Description automatically generated" />

7.  On the **bingsearchaoaiXX** window, navigate to **Resource
    management** section, and click on **Keys and Endpoint**.

<img src="./media/image8.png" style="width:6.5in;height:4.66667in"
alt="A screenshot of a computer Description automatically generated" />

8.  In **Keys and Endpoints** page, copy **KEY1** (*You can use
    either KEY1 or KEY2)* and **Endpoint** and paste them in a notepad
    (as shown in the image), and then **Save** the notepad to use the
    information in the upcoming tasks.

<img src="./media/image9.png" style="width:6.5in;height:1.95in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 2: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

> <img src="./media/image10.png" style="width:6.5in;height:4.69653in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Navigate and click on **+ Create a resource**.

> <img src="./media/image11.png" style="width:6.5in;height:4.78194in" />

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

> <img src="./media/image12.png"
> style="width:4.77917in;height:4.19021in" />

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

> <img src="./media/image13.png" style="width:4.8625in;height:5.056in" />

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

<table>
<colgroup>
<col style="width: 26%" />
<col style="width: 73%" />
</colgroup>
<thead>
<tr class="header">
<th>Subscription</th>
<th><blockquote>
<p>Select the assigned subscription</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Resource group</td>
<td>Select resource group which you have created in Task 1</td>
</tr>
<tr class="even">
<td>Region</td>
<td>For this lab, you will use a <strong>GPT-4</strong> model. This
model is currently only available in <a
href="https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models">certain
regions</a>. Please select a region from this list, In this lab
<strong>Sweden Central</strong> is using for this resource</td>
</tr>
<tr class="odd">
<td>Name</td>
<td><strong>!!AzureOpenAI-AssistantsXX!!</strong> (XX can be a unique
number, you can add more digits after XX to make the name unique)</td>
</tr>
<tr class="even">
<td>Pricing tier</td>
<td><blockquote>
<p>Select <strong>Standard S0</strong></p>
</blockquote></td>
</tr>
</tbody>
</table>

> <img src="./media/image14.png"
> style="width:6.80768in;height:5.29583in" />

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> <img src="./media/image15.png" style="width:5.58101in;height:5.89583in"
> alt="A screenshot of a computer Description automatically generated" />

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> <img src="./media/image16.png" style="width:5.1625in;height:6.08222in"
> alt="A screenshot of a computer Description automatically generated" />

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> <img src="./media/image17.png"
> style="width:6.49167in;height:4.95833in" />

9.  Wait for the deployment to complete. The deployment will take around
    **2-3** minutes.

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

<img src="./media/image18.png"
style="width:5.95417in;height:3.43722in" />

11. Click on **Keys and Endpoints** from the left navigation menu and
    then copy the endpoint value in a notepad to **AzureAI ENDPOINT**
    and key to a variable **AzureAIKey**.

<img src="./media/image19.png"
style="width:7.18457in;height:4.32917in" />

## Task 3: Deploying an Azure OpenAI models

1.  On the **AzureOpenAI-AssistantsXX** window, click on **Overview** in
    the left navigation menu, then under the **Get Started** tab, click
    on the **Go to Azure OpenAI Studio** button to open **Azure OpenAI
    Studio** in a new browser

<img src="./media/image20.png" style="width:6.5in;height:3.88333in" />

2.  In the **Azure AI \| Azure OpenAI Studio** window, click on **Create
    a new deployment** button**.**

<img src="./media/image21.png" style="width:6.5in;height:5.14167in" />

3.  In the **Deployments** window, click on **+Create new deployment**.

<img src="./media/image22.png" style="width:6.5in;height:5.16667in" />

4.  In the **Deploy model dialog** box, enter the following details and
    click on the **Create** button.

- Select Model: **gpt-4**

- Model Version**: 1106-Preview**

- Deployment Name: enter **gpt-4**

- Select the **Advanced options** and select the **Standard** as
  **Deployment type**

<img src="./media/image23.png"
style="width:5.35833in;height:7.11667in" />

5.  You will see a notification stating **Successfully Created
    deployment**. (In case, the notification did not appear on your
    window by default, click on the bell icon beside **Azure AI \| Azure
    AI Studio** bar.

<img src="./media/image24.png"
style="width:3.43363in;height:1.63347in" />

6.  In the **Deployments** page, click on +**Create new deployment**.

<img src="./media/image25.png" style="width:5.825in;height:4.65833in" />

7.  In the **Deploy model** dialog box, under **Select a model** click
    on the dropdown select **gpt-4** field, under **Model version**
    select **vision-preview** and under **Deployment name** enter
    !!**gpt-4-vision!!.** Click on the **Create** button.

> <img src="./media/image26.png" style="width:5.25in;height:4.85833in" />

8.  You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded. (You can also view the
    notification by clicking on the bell icon beside **Cognitive
    Services \| Azure OpenAI Studio)**.

<img src="./media/image27.png" style="width:4.46705in;height:1.20844in"
alt="A screenshot of a phone Description automatically generated" />

9.  In the **Deployments** page, click on +**Create new deployment**.

<img src="./media/image28.png"
style="width:6.49167in;height:4.73333in" />

10. In the **Deploy model** dialog box, under **Select a model** click
    on the dropdown select **dall-e-3** field, under **Model version**
    select **Auto-update to default** and under **Deployment name**
    enter !!**dall-e-3**!!**.** Click on the **Create** button.

<img src="./media/image29.png" style="width:5.675in;height:5.45833in" />

11. You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded. (You can also view the
    notification by clicking on the bell icon beside **Cognitive
    Services \| Azure OpenAI Studio)**.

<img src="./media/image30.png" style="width:5.27546in;height:1.42512in"
alt="A screenshot of a phone Description automatically generated" />

## Task 4: Explore the Assistant's playground

1.  In Azure OpenAI Studio Home page, under **Welcome to** **Azure
    OpenAI Service**, in **Get started** section, click on the
    **Assistants playground**.

<img src="./media/image31.png"
style="width:7.10355in;height:3.72047in" />

2.  The Assistants playground allows you to explore, prototype, and test
    AI Assistants without needing to run any code. From this page, you
    can quickly iterate and experiment with new ideas.

3.  From the Assistant setup pane enter the below details

- Assistant a name: **Math Assist**

- Instructions: Enter the following instructions !!**You are an AI
  assistant that can write code to help answer math questions**!!

- Deployment: **gpt-4**

- Select the toggle **enabling code interpreter**

<img src="./media/image32.png" style="width:6.49167in;height:6.775in" />

4.  Under the Assistant setup click on **Save**

<img src="./media/image33.png" style="width:6.5in;height:6.9in" />

5.  Enter a question for the assistant to answer: !!**I need to solve
    the equation 3x + 11 = 14. Can you help me?**!!

6.  Select the **Add and run button** .

<img src="./media/image34.png"
style="width:7.09583in;height:3.75287in" />

<img src="./media/image35.png"
style="width:7.12352in;height:3.42917in" />

While we can see that answer is correct, to confirm that the model used
code interpreter to get to this answer, and that the code it wrote is
valid rather than just repeating an answer from the model's training
data we'll ask another question.

7.  Enter the follow-up question: !!**Show me the code you ran to get
    this solution.!!** Select the **Add and run button** 

<img src="./media/image36.png"
style="width:7.19764in;height:3.69583in" />

<img src="./media/image37.png" style="width:7.2447in;height:3.4875in" />

You could also consult the logs in the right-hand panel to confirm that
code interpreter was used and to validate the code that was run to
generate the response. It is important to remember that while code
interpreter gives the model the capability to respond to more complex
math questions by converting the questions into code and running in a
sandboxed Python environment, you still need to validate the response to
confirm that the model correctly translated your question into a valid
representation in code.

## Task 5: Assistants function calling with Bing Search

In this notebook, we'll show how you can use the Bing Search APIs and
function calling to ground Azure OpenAI models on data from the web.
This is a great way to give the model access to up to date data from the
web.

This sample will be useful to developers and for data scientists who
want to learn about function calling capabilities and search based
grounding.

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> <img src="./media/image38.png"
> style="width:5.24583in;height:5.24583in" />

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open Folder**.

> <img src="./media/image39.png" style="width:3.77917in;height:4.6555in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Navigate and select **Assistants** folder from **C:\LabFiles** and
    click on the **Select Folder** button.

<img src="./media/image40.png" style="width:5.625in;height:4.36667in" />

4.  If you see a dialog box - **Do you trust the authors of the files in
    this folder?**, then click on **Yes, I trust the author**.

<img src="./media/image41.png" style="width:3.95417in;height:3.27083in"
alt="A screenshot of a computer Description automatically generated with medium confidence" />

5.  In Visual Studio Code dropdown the **ASSISTANTS**, under
    **function_calling** navigate and click on
    **assistants_function_calling_with_bing_search.ipynb** notebook.

<img src="./media/image42.png" style="width:6.5in;height:5.13333in" />

6.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1<sup>st</sup> cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

<img src="./media/image43.png" style="width:6.5in;height:2.1in" />

<img src="./media/image44.png" style="width:6.47083in;height:2.57083in"
alt="A screenshot of a computer Description automatically generated" />

7.  If prompted to select the path, then select the **Python version
    3.12.2(or later version)** path as shown in the image.

<img src="./media/image45.png" style="width:6.5in;height:5.09444in" />

8.  Update the parameters ,replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    2), Bing search subscription key** with the values that you have
    saved in your notepad in the **Task 1 .**

<img src="./media/image46.png"
style="width:7.15691in;height:2.5875in" />

<img src="./media/image47.png" style="width:6.5in;height:3.63542in"
alt="A screenshot of a computer program Description automatically generated" />

9.  Define a function to call the Bing Search APIs, select
    3<sup>rd</sup> , 4<sup>th</sup> cells. Then, execute the cell by
    clicking on the **start icon**.

<img src="./media/image48.png" style="width:6.49167in;height:5.025in" />

<img src="./media/image49.png" style="width:6.5in;height:3.175in" />

10. Get things running end to end, select 5<sup>th</sup> ,6<sup>th</sup>
    ,7<sup>th</sup>,8<sup>th</sup> cells. Then, execute the cell by
    clicking on the **start icon**.

<img src="./media/image50.png" style="width:6.5in;height:4.83333in" />

<img src="./media/image51.png" style="width:6.49167in;height:4.925in" />

<img src="./media/image52.png" style="width:6.5in;height:4.81667in" />

<img src="./media/image53.png"
style="width:6.49167in;height:4.85833in" />

<img src="./media/image54.png"
style="width:6.15417in;height:3.89764in" />

## **Task 6: Building a multimodal multi-agent framework with Azure Assistant API**

This repo will walk you through the pattern of creating a multi-agent
system using the Azure OpenAI Assistant API.

he example provided in this notebook helps demonstrate how to build a
multi-agent framework with Azure Assistant API and serves as a
comprehensive guide for developers looking to harness the capabilities
of multiple AI agents working in concert. The crux of the article is to
showcase how agents can communicate and collaborate to process complex
tasks, such as generating and enhancing images through multiple
iterations based on user input. This is particularly relevant for
developers and tech enthusiasts who are interested in exploring the
frontiers of generative AI and multi-agent systems.

Before getting started, one should have a basic understanding of AI and
an interest in how agents can work together to enhance AI
functionalities. The article does not delve into in-depth programming;
however, a general knowledge of how APIs operate and the role of AI in
automated systems would be beneficial in grasping the concepts
presented. This example is an invitation to innovators and developers
who wish to experiment with advanced AI systems and potentially
integrate them into various industry solutions.

1.  In Visual Studio Code, under **multi-agent** ,navigate and click on
    **.env** file.

<img src="./media/image55.png"
style="width:7.20417in;height:3.81941in" />

2.  In the **.env** file, replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    2), gpt4 deployment name, DALLE3 deployment name and GPT 4 Vision
    deployment name** with the values that you have saved in your
    notepad in the **Task 3**.

<img src="./media/image56.png"
style="width:7.30724in;height:3.69583in" />

3.  Click on **File** and the click on **Save**.

<img src="./media/image57.png" style="width:5.05in;height:6.35833in" />

4.  In Visual Studio Code, under **multi-agent**, navigate and click on
    **multi-agent.ipynb** notebook.

> <img src="./media/image58.png" style="width:6.5in;height:4.775in" />

5.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1<sup>st</sup> cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

6.  If prompted to select the path, then select the **Python version
    3.12.2(or later version)** path as shown in the image.

> <img src="./media/image59.png" style="width:6.5in;height:3.83819in"
> alt="A screenshot of a computer Description automatically generated" />

7.  Select 2<sup>nd</sup> cell. Then, execute the cell by clicking on
    the **start icon**.

<img src="./media/image60.png"
style="width:6.52933in;height:4.6375in" />

<img src="./media/image61.png"
style="width:6.99019in;height:4.3375in" />

8.  To generating images using a prompt to the Dalle-3 Model. The output
    is a .jpg file stored in the users local directory. Select
    3<sup>rd</sup> cell. Then, execute the cell by clicking on the
    **start icon**.

<img src="./media/image62.png"
style="width:7.17399in;height:4.6875in" />

9.  Initializes the agent with the definition described above. Select
    4<sup>th</sup> cell. Then, execute the cell by clicking on the
    **start icon**.

<img src="./media/image63.png"
style="width:6.66566in;height:3.52083in" />

10. Image generator function calls the Dalle-3 image generator given the
    prompt. Select 5<sup>th</sup> cell. Then, execute the cell by
    clicking on the **start icon**.

<img src="./media/image64.png" style="width:6.5in;height:4.675in" />

11. Vision Assistant agent is responsible for analyzing images. The
    output is a new prompt to be used by the image creator agent. Select
    6<sup>th</sup> cell. Then, execute the cell by clicking on the
    **start icon**.

<img src="./media/image65.png" style="width:6.5in;height:4.34167in" />

12. Initializes the agent with the definition described above. Select
    7<sup>th</sup> cell. Then, execute the cell by clicking on the
    **start icon**.

<img src="./media/image66.png" style="width:6.5in;height:2.25833in" />

13. Vision assistant function calls the GPT4 Vision image analyzes given
    an image, execute the cell by clicking on the **start icon**.

<img src="./media/image67.png"
style="width:6.49167in;height:4.60833in" />

14. This agent facilitates the conversation between the user and other
    agents, ensuring successful completion of the task, execute the cell
    by clicking on the **start icon**.

<img src="./media/image68.png" style="width:6.49167in;height:5.2in" />

15. Initializes the agent with the definition described above, execute
    the cell by clicking on the **start icon**.

<img src="./media/image69.png" style="width:6.5in;height:3.65in" />

16. This function calls the Assistant API to generate a main thread of
    communication between the agents listed in the agents_threads,
    execute the cell by clicking on the **start icon**.

<img src="./media/image70.png" style="width:6.49167in;height:5.125in" />

17. This agent facilitates the conversation between the user and other
    agents, ensuring successful completion of the task. Execute the cell
    by clicking on the **start icon**.

<img src="./media/image71.png"
style="width:6.49167in;height:5.25833in" />

<img src="./media/image72.png" style="width:6.5in;height:4.22639in"
alt="A screenshot of a computer program Description automatically generated" />

18. Example Questions, enter the !!Generate an image of a boat drifting
    in the water and analyze it and enhance the image!!. Execute the
    cell by clicking on the **start icon**.

<img src="./media/image73.png" style="width:6.5in;height:5.54167in" />

<img src="./media/image74.png" style="width:6.5in;height:5.03472in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image75.png" style="width:6.5in;height:5.34444in" />

## Task 7: Delete the resources

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

> <img src="./media/image76.png" style="width:6.5in;height:4.58472in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the AOAI-RGXXX resource group.

> <img src="./media/image77.png" style="width:4.675in;height:3.55833in"
> alt="A screenshot of a computer Description automatically generated" />

3.  In the **Resource group** home page, select the **delete resource
    group**

<img src="./media/image78.png"
style="width:6.49167in;height:3.24167in" />

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “resource group name” to confirm deletion**
    field, then click on the **Delete** button.

<img src="./media/image79.png" style="width:4.44993in;height:4.4625in"
alt="A screenshot of a computer Description automatically generated" />

5.  On **Delete confirmation** dialog box, click on **Delete** button.

> <img src="./media/image80.png" style="width:3.475in;height:1.85833in"
> alt="A screenshot of a computer error Description automatically generated" />

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

<img src="./media/image81.png"
style="width:3.4253in;height:2.81691in" />

**Summary**

This lab provided a hands-on exploration of advanced AI capabilities
using Azure OpenAI and Bing Search integration. You’ve begun by setting
up essential Azure resources and deploying AI models such as GPT-4 and
DALL-E-3. Then, you’ve used Azure OpenAI Studio to create and test AI
assistants capable of handling complex tasks like mathematical
problem-solving and image generation. You’ve integrated Bing Search to
fetch real-time data for grounding AI responses. Additionally, you’ve
learned to build a multi-agent framework, showcasing how different AI
agents can collaborate to enhance task performance. By the end, you’ve
gained practical experience in deploying, testing, and optimizing
AI-driven solutions that prepared you to leverage these technologies in
various real-world applications.

**Introduction**

In this [Azure AI Studio](https://ai.azure.com/) use case, you use
generative AI and prompt flow to build, configure, and deploy a copilot
for your retail company called Contoso. Your retail company specializes
in outdoor camping gear and clothing.

The copilot should answer questions about your products and services. It
should also answer questions about your customers. For example, the
copilot can answer questions such as "How much do the TrailWalker hiking
shoes cost?" and "How many TrailWalker hiking shoes did Daniel Wilson
buy?".

In this use case, you’ll learn how to create and deploy your own AI
copilot using Azure AI Studio's prompt flow capabilities. This lab is
designed to equip you with practical skills in setting up Azure AI
resources, designing sophisticated prompt flows, managing diverse data
sources, and optimizing AI models for enhanced performance.

By the end of this use case, you will have acquired essential skills in
leveraging Azure AI Studio’s capabilities to build and deploy a
versatile AI copilot, ready to assist in a range of interactive and
data-driven applications.

**Objectives**

- To provision and configure Azure AI resources, including Cognitive
  Search and role-based access control, to ensure secure deployment and
  management of AI applications.

- To deploy and configure an Azure AI project in Azure AI Studio,
  integrating Azure AI Search for seamless data connections, deploying a
  GPT-4 chat model, and enhancing model capabilities through rigorous
  testing of local data sources in the Azure AI Studio playground.

- To configure and deploy compute instances and runtime environments in
  Azure AI Studio tailored for prompt flow operations, ensuring optimal
  performance and scalability for the copilot's chat model.

- To enhance the Azure AI Studio prompt flow by seamlessly integrating
  multiple data sources, such as product and customer information
  indexes, to enable comprehensive and accurate responses for complex
  queries in the copilot application.

- To delete the deployed resources in order to avoid incurring
  unnecessary Azure costs.

# Exercise 1- Create an Azure AI resource and Azure cognitive Search by using the portal

## **Task 1: Create a secure Azure AI resource in the Azure portal**

If your organization is using [Azure
Policy](https://learn.microsoft.com/en-us/azure/governance/policy/overview),
setup a resource that meets your organization's requirements instead of
using AI Studio for resource creation.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:
    [<u>https://portal.azure.com/</u>](https://portal.azure.com/), then
    press the **Enter** button.

> <img src="./media/image1.png" style="width:6.49167in;height:4.14167in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

<img src="./media/image2.png" style="width:3.82749in;height:3.85456in"
alt="Graphical user interface, application Description automatically generated" />

3.  Then, enter the password and click on the **Sign in** button**.**

> <img src="./media/image3.png" style="width:4.61319in;height:3.54028in"
> alt="Graphical user interface, application, email Description automatically generated" />

4.  In **Stay signed in?** window, click on the **Yes** button.

> <img src="./media/image4.png" style="width:4.46806in;height:3.80625in"
> alt="Graphical user interface, application Description automatically generated" />

5.  From the Azure portal, search for **Azure AI Studio** and click on
    **Azure AI Studio.** 

> <img src="./media/image5.png" style="width:6.5in;height:4.55833in" />

6.  Select create a new resource by selecting **+ New Azure AI hub**

> <img src="./media/image6.png" style="width:6.5in;height:4.15833in" />

| **Field** | **Description** |
|----|----|
| **Subscription** | Select your Azure OpenAI subscription |
| **Resource group** | Click on **Create new**\> enter **AOAI-RGXX**(XX can be a unique number, you can add more digits after XX to make the name unique) |
| **Region** | For this lab, you will use a **GPT-4** model. This model is currently only available in [certain regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models). Please select a region from this list, In this lab **East US 2** is using for this resource. |
| **Name** | Copilot-AzureAIXX (XXcan be unique number) |

7.  On the **Azure AI** Create a search service page, provide the
    following information and click on **Next: Storage** button.

> <img src="./media/image7.png"
> style="width:6.49167in;height:6.16667in" />

8.  In the **Storage** tab, leave all in the default state, and click on
    the **Next: Networking** button.

> <img src="./media/image8.png"
> style="width:6.49167in;height:5.88333in" />

9.  In the **Networking** tab, select the Public radio buttons, and
    click on the **Next: Encryption** button.

> <img src="./media/image9.png" style="width:6.5in;height:5.875in" />

10. In the **Encryption** tab, click the check box on
    **Microsoft-managed keys** , and click on the **Next: Identity**
    button.

> <img src="./media/image10.png" style="width:6.5in;height:6.55in" />

11. In the **Identity** tab, leave all the fields in the default state,
    and click on the **Review+create** button.

> <img src="./media/image11.png" style="width:6.49167in;height:6.4in" />

12. In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> <img src="./media/image12.png" style="width:6.5in;height:6.54167in" />

13. After the deployment is completed, click on the **Go to resource**
    button.

> <img src="./media/image13.png" style="width:6.5in;height:3.45in" />

## **Task 2:Role-based access control in Azure AI Studio**

1.  In your **Copilot-AzureAI** window, from the left menu, click on the
    **Access control(IAM).**

<img src="./media/image14.png" style="width:6.5in;height:5.19167in" />

2.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image15.png" style="width:6.5in;height:4.10833in" />

3.  In **Privileged administrator** **role,** type the **contributor**
    in the search box and select it. Click **Next**

<img src="./media/image16.png" style="width:6.5in;height:5.275in" />

4.  In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image17.png"
style="width:5.49352in;height:5.1625in" />

5.  On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

<img src="./media/image18.png" style="width:4.325in;height:6.90833in" />

6.  In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image19.png" style="width:6.5in;height:5.8in" />

<img src="./media/image20.png" style="width:6.49167in;height:5.4in" />

7.  In your **Copilot-AzureAI** window, from the left menu, click on the
    **Access control(IAM).**

<img src="./media/image14.png" style="width:6.5in;height:5.19167in" />

8.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image15.png" style="width:6.5in;height:4.10833in" />

9.  Type the **Azure AI Developer** in the search box and select it.
    Click **Next**

<img src="./media/image21.png" style="width:6.5in;height:5.45in" />

10. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image22.png" style="width:6.5in;height:6.15417in"
alt="A screenshot of a computer Description automatically generated" />

11. On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

<img src="./media/image23.png" style="width:4.71667in;height:7.64167in"
alt="A screenshot of a computer Description automatically generated" />

12. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image24.png"
style="width:6.49167in;height:6.96667in" />

<img src="./media/image25.png" style="width:6.40833in;height:7.475in" />

13. You will see a notification – added as Azure AI Developer for
    Azure-openai-testXX

<img src="./media/image26.png"
style="width:4.85042in;height:2.63356in" />

## **Task 3: Create an Azure AI Search service in the portal**

1.  In Azure portal home page, click on **+ Create Resource**.

> <img src="./media/image27.png" style="width:5.2125in;height:2.94416in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Create a resource** page search bar, type **Azure AI
    Search** and click on the appeared **azure ai search**.

<img src="./media/image28.png" style="width:6.5in;height:3.64167in"
alt="A screenshot of a computer Description automatically generated" />

3.  Click on **azure ai search** section.

<img src="./media/image29.png" style="width:6.49167in;height:4.65833in"
alt="A screenshot of a computer Description automatically generated" />

4.  In the **Azure AI Search** page, click on the **Create** button.

> <img src="./media/image30.png" style="width:5.15in;height:3.75833in"
> alt="A screenshot of a computer Description automatically generated" />

5.  On the **Create a search service** page, provide the following
    information and click on **Review+create** button.

| **Field** | **Description** |
|----|----|
| **Subscription** | Select your Azure OpenAI subscription |
| **Resource group** | Select your Resource group(that you have created in **Task 1**) |
| **Region** | East US |
| **Name** | mysearchserviceXX (XXcan be unique number) |
| **Pricing Tier** | Click on change Price Tire\>select **Basic** |

<img src="./media/image31.png" style="width:5.79583in;height:5.28991in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image32.png" style="width:5.4875in;height:4.3745in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image33.png" style="width:4.63844in;height:4.37083in"
alt="A screenshot of a computer Description automatically generated" />

6.  Once the Validation is passed, click on the **Create** button.

<img src="./media/image34.png" style="width:4.73836in;height:5.54735in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image35.png" style="width:7.45697in;height:3.25525in"
alt="A screenshot of a computer Description automatically generated" />

7.  After the deployment is completed, click on the **Go to resource**
    button.

<img src="./media/image36.png" style="width:7.12476in;height:2.95417in"
alt="A screenshot of a computer Description automatically generated" />

8.  In the **mysearchserviceXX** Overview page. In the left-side
    navigation pane, under **Settings** section, select **Semantic
    ranker**.

<img src="./media/image37.png" style="width:6.5in;height:5.3in" />

9.  On the **Semantic ranker** tab**,** select **Free** tile and click
    on the **Select plan.**

<img src="./media/image38.png" style="width:6.49167in;height:5.125in" />

10. You will see a notification -**Successfully updated semantic ranker
    to free plan**

<img src="./media/image39.png" style="width:6.49167in;height:4.45in" />

# Exercise-2: Add your data using Azure OpenAI Studio

## **Task 1: Create an Azure AI project in Azure AI Studio**

Your Azure AI project is used to organize your work and save state while
building your copilot. During this tutorial, your project contains your
data, prompt flow runtime, evaluations, and other resources.

1.  On the **copilot-AzureAIXXX** window, click on **Overview** in the
    left navigation menu, then under the **Govern the environment for
    your team in AI Studio** tab, click on the **Launch** **Azure AI
    Studio** button to open **Azure AI Studio** in a new browser.

<img src="./media/image40.png"
style="width:7.13911in;height:3.44583in" />

<img src="./media/image41.png" style="width:7.22286in;height:3.57207in"
alt="A screenshot of a computer Description automatically generated" />

2.  In the **Azure AI Studio** window, click on **+ New project** from
    under the **Project.**

<img src="./media/image42.png"
style="width:7.09476in;height:4.3625in" />

3.  In the **Create a project** tab, under **Project name**, enter the
    Project name as +++**contoso-outdoor-proj+++** and then click on
    **Create a project** button.

<img src="./media/image43.png"
style="width:5.88333in;height:2.91667in" />

4.  Wait for the deployment to complete. The deployment will take around
    1-2 minutes.

<img src="./media/image44.png" style="width:6.5in;height:3.84583in"
alt="A screenshot of a computer Description automatically generated" />

## Task 2: Azure AI Search service connection

1.  In the **Azure AI Studio** window, click on **Settings** under
    Project overview and select +**New connection** from the **Connected
    resources** section.

> <img src="./media/image45.png" style="width:7.11293in;height:3.67083in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In **Add a connection to external assets** page , select **Azure AI
    Search.**

> <img src="./media/image46.png" style="width:6.5in;height:3.91327in"
> alt="A screenshot of a computer Description automatically generated" />

3.  In Connect an Azure AI Search resource page, select ai search
    (you’ve created in Exercise 1\>Task 3) and click on **Add
    connection**

> <img src="./media/image47.png" style="width:6.5in;height:3.025in"
> alt="A screenshot of a computer Description automatically generated" />

4.  After the service is connected, select **Close** to return to
    the **Settings** page.

> <img src="./media/image48.png" style="width:6.5in;height:3.89167in" />

## **Task 3: Create a compute instance**

To create a compute instance in Azure AI Studio:

1.  In the Azure AI Studio page, select **Settings** from the left menu
    and select **View all** under the **Compute** session.

<img src="./media/image49.png"
style="width:6.8141in;height:4.42917in" />

2.  In the **Azure AI Studio** page, under the **Compute instance** tab
    select **+New**.

> <img src="./media/image50.png" style="width:6.5in;height:4.55in" />

3.  In **Create compute instance** pane, enter the following details and
    click on **Next** button.

<table>
<colgroup>
<col style="width: 47%" />
<col style="width: 52%" />
</colgroup>
<thead>
<tr class="header">
<th>Compute name</th>
<th><strong>copilotcomputeXX</strong>(XX can be a unique number)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Virtual machine type</td>
<td><strong>CPU</strong></td>
</tr>
<tr class="even">
<td>Virtual machine size</td>
<td><p>Select from recommended options</p>
<ul>
<li><p>Standard_E4ds_v44 cores, 32GB RAM, 150GB storage</p></li>
</ul></td>
</tr>
</tbody>
</table>

<img src="./media/image51.png"
style="width:7.31561in;height:3.6625in" />

4.  In **Scheduling** pane, click on **Add schedule** and leave all the
    fields in the default state. Then click **Next** button.

> <img src="./media/image52.png"
> style="width:6.49167in;height:4.40833in" />
>
> <img src="./media/image53.png"
> style="width:7.07806in;height:3.57083in" />

5.  In **Security** pane, leave all the fields in the default state then
    click **Next** button.

> <img src="./media/image54.png"
> style="width:6.90274in;height:3.07083in" />

6.  In **Tags** pane, leave all the fields in the default state then
    click **Next** button.

> <img src="./media/image55.png" style="width:6.48333in;height:3.225in" />

7.  In **Review** pane, review the details that you’ve entered, and
    click on **Create** button**.**

> <img src="./media/image56.png"
> style="width:7.08409in;height:3.5375in" />

8.  To create the compute instance will take 5-6 minutes

<img src="./media/image57.png" style="width:6.5in;height:4.23194in"
alt="A screenshot of a computer Description automatically generated" />

> <img src="./media/image58.png" style="width:6.80085in;height:3.58207in"
> alt="A screenshot of a computer Description automatically generated" />

## **Task 4: Deploy a chat model**

Follow these steps to deploy an Azure OpenAI chat model for your
copilot.

1.  On the Azure AI Studio **Home** page. select **Model catalog** under
    the **Get started**.

> <img src="./media/image59.png"
> style="width:6.80417in;height:4.64951in" />

2.  In the **Collections** filter, select **Azure OpenAI**.

> <img src="./media/image60.png"
> style="width:7.07083in;height:4.5021in" />

3.  Select a model such as **gpt-4** from the Azure OpenAI collection.

> <img src="./media/image61.png"
> style="width:7.11251in;height:2.72083in" />

4.  Select **Deploy** to open the deployment window.

> <img src="./media/image62.png"
> style="width:7.16932in;height:4.32917in" />

5.  In the **Deploy model** dialog box, under the **Deployment name**
    field, enter **gpt-4, select the Model version** as **1106-Preview**
    and click on **Deploy** button.

> <img src="./media/image63.png" style="width:5.625in;height:6.875in" />

6.  You see the deployment details page. Details include the date you
    created the deployment and the created date and version of the model
    you deployed.

> <img src="./media/image64.png" style="width:6.5in;height:5.725in" />

7.  On the deployment details page from the previous step, select **Open
    in playground**.

<img src="./media/image65.png" style="width:6.5in;height:5.86667in" />

## **Task 5: Chat in the playground without your data**

In the Azure AI Studio playground you can observe how your model
responds with and without your data. In this section, you test your
model without your data. In the next section, you add your data to the
model to help it better answer questions about your products.

1.  In the playground, select your deployed **gpt-4** chat model from
    the **Deployment** dropdown.

> <img src="./media/image66.png"
> style="width:6.99547in;height:3.52917in" />

2.  In the **System message** text box on the **Assistant setup** pane,
    provide this prompt to guide the assistant: **You're an AI assistant
    that helps people find information**. 

<img src="./media/image67.png"
style="width:7.1625in;height:4.56046in" />

3.  Select **Apply changes** to save your changes.

> <img src="./media/image68.png"
> style="width:6.49167in;height:5.09167in" />

4.  In the **Update system message?** dialog box, click on the
    **Continue button.**

> <img src="./media/image69.png"
> style="width:3.53333in;height:2.56667in" />

5.  In the chat session pane, enter the following question: **How much
    do the TrailWalker hiking shoes cost**, and then select the right
    arrow icon to send.

> <img src="./media/image70.png"
> style="width:7.04551in;height:3.82083in" />

6.  The assistant replies that it doesn't know the answer. The model
    doesn't have access to product information about the TrailWalker
    hiking shoes.

> <img src="./media/image71.png"
> style="width:7.03477in;height:3.91572in" />
>
> In the task, you'll add your data to the model to help it answer
> questions about your products.

## **Task 6: Add your data using chat model** 

You upload your local data files to Azure Blob storage and create an
Azure AI Search index. Your data source is used to help ground the model
with specific data. Grounding means that the model uses your data to
help it understand the context of your question. You're not changing the
deployed model itself. Your data is stored separately and securely in
your Azure subscription.

1.  In the Azure AI Studio playground, select **Chat** from the Project
    playground left menu.

> <img src="./media/image72.png"
> style="width:6.49167in;height:4.25833in" />

2.  On the **Chat playground** pane, select **Add your data**  \> **+
    Add a new data source**.

> <img src="./media/image73.png" style="width:6.49167in;height:4.825in" />

3.  In the **Add your data** page that appears, select **Upload
    files/folders** from the **Select data source** dropdown.

> <img src="./media/image74.png" style="width:6.5in;height:4.65in" />

4.  In the **Select your data** pane, click on **Upload folder** and
    navigate to **C:\Labfiles** location and select **1-customer-info**
    and **3-product-info,** then click on **Upload** button.

> <img src="./media/image75.png"
> style="width:7.0125in;height:4.93572in" />
>
> <img src="./media/image76.png" style="width:6.5in;height:2.98333in" />

5.  If you see a dialog box – Upload 20 files to this site?, click on
    Upload button.

> <img src="./media/image77.png" style="width:6.5in;height:2.15833in" />
>
> <img src="./media/image78.png"
> style="width:7.08264in;height:3.24583in" />

6.  In the **Select your data** pane, click on **Next** button.

> <img src="./media/image79.png"
> style="width:7.09842in;height:5.02083in" />

7.  In **Index storage** pane , under **Select Azure AI Search** service
    select **AI search service** (you’ve created in Exercise 1\>Task 4)
    and enter **product-info** for the Index name

> <img src="./media/image80.png"
> style="width:6.97083in;height:4.3042in" />

8.  **Vector settings** type should be selected by default and click on
    the **Next** button.

> <img src="./media/image81.png" style="width:6.5in;height:4.65833in" />

9.  Review the details you entered, and select **Create**.

> <img src="./media/image82.png"
> style="width:7.19583in;height:5.13856in" />

10. The data will be added in your Chat Playground. This will take
    approximately 10-15 minutes.

> <img src="./media/image83.png"
> style="width:7.0625in;height:4.39143in" />
>
> <img src="./media/image84.png"
> style="width:7.03264in;height:3.52083in" />
>
> <img src="./media/image85.png" style="width:6.5in;height:4.77083in" />
>
> <img src="./media/image86.png" style="width:7.12029in;height:4.38932in"
> alt="A screenshot of a chat Description automatically generated" />

11. In the **Chat session** section, enter the following prompt in the
    **User message** text box and click on the **Send** icon

CodeCopy

<span class="mark">How much do the TrailWalker hiking shoes cost</span>

> <img src="./media/image87.png"
> style="width:7.13748in;height:3.54583in" />

12. You can expand the **references** button to see the data that was
    used.

> <img src="./media/image88.png"
> style="width:7.0125in;height:3.87083in" />

## **Task 7: Create a prompt flow from the playground**

1.  Select **P**r**ompt flow** from the menu above the **Chat
    playground** pane.

> <img src="./media/image89.png"
> style="width:7.02143in;height:3.47917in" />

2.  Enter a folder name for your prompt flow as +++**Contoso outdoor
    flow+++** . Then select **Open**. Azure AI Studio exports the
    playground chat environment including connections to your data to
    prompt flow.

> <img src="./media/image90.png"
> style="width:6.82917in;height:4.59417in" />
>
> <img src="./media/image91.png" style="width:7.11651in;height:3.63353in"
> alt="A screenshot of a computer Description automatically generated" />

- **Save** button: You can save your prompt flow at any time by
  selecting **Save** from the top menu. Be sure to save your prompt flow
  periodically as you make changes in this tutorial.

- **Start compute session** button: You need to start a compute session
  to run your prompt flow. You can start the session later in the
  tutorial. You incur costs for compute instances while they are running

> <img src="./media/image92.png"
> style="width:7.20448in;height:3.19583in" />

- To facilitate node configuration and fine-tuning, a visual
  representation of the workflow structure is provided through a DAG
  (Directed Acyclic Graph) graph. This graph showcases the connectivity
  and dependencies between nodes, providing a clear overview of the
  entire workflow. The nodes in the graph shown here are representative
  of the playground chat experience that you exported to prompt flow.

<img src="./media/image93.png"
style="width:7.10888in;height:3.74583in" />

# Exercise 3: Customize prompt flow with multiple data sources

Earlier in the [Azure AI Studio](https://ai.azure.com/) playground,
you [added your
data](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-copilot-ai-studio#add-your-data-and-try-the-chat-model-again) to
create one search index that contained product data for the Contoso
copilot. So far, users can only inquire about products with questions
such as "How much do the TrailWalker hiking shoes cost?". But they can't
get answers to questions such as "How many TrailWalker hiking shoes did
Daniel Wilson buy?" To enable this scenario, we add another index with
customer information to the flow.

## **Task 1: Create the customer info index**

1.  In the Azure AI Studio playground, select **Indexes** from the
    collapsible left menu.

<img src="./media/image94.png"
style="width:6.94811in;height:5.1375in" />

2.  In the **Create indexes to customize generative AI responses** tab,
    select **+New index**

> <img src="./media/image95.png"
> style="width:6.94532in;height:4.52917in" />

3.  You're taken to the **Create an index** wizard.

> <img src="./media/image96.png" style="width:6.59539in;height:3.93468in"
> alt="A screenshot of a computer Description automatically generated" />

4.  On the Source data page, select **Upload files/folders** from
    the **Upload** dropdown. Select the customer info files that you
    downloaded or created earlier.

> <img src="./media/image97.png"
> style="width:6.87558in;height:4.10417in" />
>
> <img src="./media/image98.png"
> style="width:6.90798in;height:4.07917in" />

5.  Navigate to **C:\Labfiles** location and select **1-customer-info**
    and **3-product-info,** then click on **Upload** button.

> <img src="./media/image99.png"
> style="width:7.09275in;height:3.19583in" />
>
> <img src="./media/image100.png"
> style="width:7.15538in;height:3.27917in" />

6.  If you see a dialog box – Upload 20 files to this site?, click on
    Upload button

> <img src="./media/image101.png"
> style="width:4.56667in;height:1.50833in" />

7.  Select **Next** at the bottom of the page.

> <img src="./media/image102.png"
> style="width:6.92917in;height:4.01162in" />

8.  Select the same Azure AI Search resource (that you have created in
    **Ex 1\>** **Task 4**), enter +++**customer-info+++** for the index
    name and select virtual machine as **Auto select**. Then
    select **Next**.

> <img src="./media/image103.png"
> style="width:6.98498in;height:4.07083in" />

9.  **Vector settings** type should be selected by default.

10. Select ***Default_AzureOpenAI*** from the **Azure OpenAI
    resource** dropdown. Select the checkbox to acknowledge that an
    Azure OpenAI embedding model will be deployed if it's not already.
    Then select **Next**.

<img src="./media/image104.png"
style="width:7.0193in;height:5.0125in" />

** Note:** The embedding model is listed with other model deployments in
the Deployments page.

11. Review the details you entered, and select **Create**.

<img src="./media/image105.png"
style="width:6.5125in;height:4.74852in" />

<img src="./media/image106.png"
style="width:7.3015in;height:3.90583in" />

** Note:** You use the *customer-info* index and
the *mysearchserviceXX* Azure AI Search resource in prompt flow later in
this tutorial. If the names you enter differ from what's specified here,
make sure to use the names you entered in the rest of the lab.

12. You're taken to the index details page where you can see the status
    of your index creation , it will take around 20-23 minutes .

<img src="./media/image107.png"
style="width:6.9927in;height:4.0125in" />

<img src="./media/image108.png" style="width:6.5in;height:3.67639in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 2: Add customer information to the flow**

Afte you're done creating your index, return to your prompt flow and
follow these steps to add the customer info to the flow:

1.  On the Azure AI Studio **Home** page, select **Prompt flow** under
    the Tools.

<img src="./media/image109.png"
style="width:7.29583in;height:4.57043in" />

2.  On the Flows pane, select **contoso outdoor flow.**

<img src="./media/image110.png"
style="width:6.63311in;height:3.7125in" />

3.  Select **Start compute session** from the top menu.

<img src="./media/image111.png"
style="width:7.11464in;height:3.52083in" />

4.  It will take 1-3 minutes to **start compute session**

<img src="./media/image112.png"
style="width:7.21574in;height:3.6125in" />

5.  Make sure you have a compute session running. 

<img src="./media/image113.png"
style="width:7.31124in;height:3.75417in" />

6.  Select **+ More tools** from the top menu and then select **Index
    Lookup** from the list of tools.

<img src="./media/image114.png"
style="width:7.05174in;height:3.8875in" />

7.  Name the new node +++**queryCustomerIndex+++** and select **Add**.

> <img src="./media/image115.png"
> style="width:6.92682in;height:4.04583in" />

8.  Select the **mlindex_content** textbox in
    the **queryCustomerIndex** node.

> <img src="./media/image116.png"
> style="width:6.9125in;height:3.5626in" />

9.  The **Generate** dialog opens. You use this dialog to configure
    the **queryCustomerIndex** node to connect to
    your *customer-info* index.

10. In the **Generate** dialog, for the **index_type** value,
    select **Azure AI Search**.

<img src="./media/image117.png" style="width:6.5in;height:4.325in" />

11. In the **Generate** dialog, Select or enter the following values and
    Select **Save** to save the settings.

| **Name** | **Value** |
|----|----|
| **acs_index_connection** | The name of your Azure AI Search service connection (such as *mysearchserviceXX*) |
| **acs_index_name** | *customer-info* |
| **acs_content_field** | *content* |
| **acs_metadata_field** | *meta_json_string* |
| **semantic_configuration** | *azuremldefault* |
| **embedding_type** | *None* |

<img src="./media/image118.png"
style="width:6.97083in;height:4.61739in" />

12. Select or enter the following values for
    the **queryCustomerIndex** node

| **Name**       | **Value**                        |
|----------------|----------------------------------|
| **queries**    | *\${extractSearchIntent.output}* |
| **query_type** | *Keyword*                        |
| **top**        | *5*                              |

13. You can see the **queryCustomerIndex node** is connected to the
    **extractSearchIntent** node in the graph

> <img src="./media/image119.png"
> style="width:6.45833in;height:5.24167in" />

14. Select **Save** from the top menu to save your changes. Remember to
    save your prompt flow periodically as you make changes.

> <img src="./media/image120.png"
> style="width:7.05912in;height:3.8875in" />
>
> <img src="./media/image121.png" style="width:6.5in;height:3.61806in"
> alt="A screenshot of a computer Description automatically generated" />

## **Task 3: Connect the customer info to the flow**

In the next section, you aggregate the product and customer info to
output it in a format that the large language model can use. But first,
you need to connect the customer info to the flow.

1.  Select the ellipses icon next to **+ More tools** and then
    select **Raw file mode** to switch to raw file mode. This mode
    allows you to copy and paste nodes in the graph.

> <img src="./media/image122.png"
> style="width:7.00461in;height:3.47083in" />
>
> <img src="./media/image123.png" style="width:6.97083in;height:3.94865in"
> alt="Screenshot of the raw file mode option in prompt flow." />
>
> <img src="./media/image124.png" style="width:7.05007in;height:3.75627in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Replace all instances
    of **querySearchResource** with **queryProductIndex** in the graph.
    We're renaming the node to better reflect that it retrieves product
    info and contrasts with the **queryCustomerIndex** node that you
    added to the flow.

> <img src="./media/image125.png"
> style="width:4.82077in;height:4.65417in" />
>
> <img src="./media/image126.png"
> style="width:4.07917in;height:4.05566in" />
>
> <img src="./media/image127.png"
> style="width:4.59583in;height:4.69421in" />
>
> <img src="./media/image128.png"
> style="width:4.91667in;height:3.5875in" />

3.  Rename and replace all instances
    of **chunkDocuments** with **chunkProductDocuments** in the graph.

> <img src="./media/image129.png" style="width:5.4in;height:6.075in" />
>
> <img src="./media/image130.png"
> style="width:5.56667in;height:6.14167in" />

4.  Rename and replace all instances
    of **selectChunks** with **selectProductChunks** in the graph.

> <img src="./media/image131.png"
> style="width:5.50833in;height:5.925in" />
>
> <img src="./media/image132.png" style="width:5.525in;height:5.9in" />

5.  Copy and paste
    the **chunkProductDocuments** and **selectProductChunks** nodes to
    create similar nodes for the customer info. Rename the new
    nodes **chunkCustomerDocuments** and **selectCustomerChunks** respectively.Simllarly
    like below code

> \- name: chunkCustomerDocuments
>
> type: python
>
> source:
>
> type: code
>
> path: chunkProductDocuments.py
>
> inputs:
>
> data_source: Azure AI Search
>
> max_tokens: 1050
>
> queries: \${extractSearchIntent.output}
>
> query_type: Hybrid (vector + keyword)
>
> results: \${queryCustomerIndex.output}
>
> top_k: 5
>
> use_variants: false
>
> \- name: selectCustomerChunks
>
> type: python
>
> source:
>
> type: code
>
> path: filterChunks.py
>
> inputs:
>
> min_score: 0.3
>
> results: \${chunkCustomerDocuments.output}
>
> top_k: 5
>
> use_variants: false
>
> <img src="./media/image133.png"
> style="width:5.39167in;height:6.21667in" />

14. Within the **chunkCustomerDocuments** node, replace
    the **\${queryProductIndex.output}** input
    with **\${queryCustomerIndex.output}**.

> <img src="./media/image134.png"
> style="width:5.23333in;height:4.44167in" />

15. Within the **selectCustomerChunks** node, replace
    the **\${chunkProductDocuments.output}** input
    with **\${chunkCustomerDocuments.output}.**

> <img src="./media/image135.png"
> style="width:5.31667in;height:4.36667in" />

16. Select **Save** from the top menu to save your changes.

> <img src="./media/image136.png"
> style="width:5.675in;height:5.20833in" />
>
> By now, the **flow.dag.yaml** file should include nodes (among others)
> that look similar to the following:

<span class="mark">id: template_chat_flow</span>

> <span class="mark">name: Template Chat Flow</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">chat_history:</span>
>
> <span class="mark">type: list</span>
>
> <span class="mark">default: \[\]</span>
>
> <span class="mark">is_chat_input: false</span>
>
> <span class="mark">is_chat_history: true</span>
>
> <span class="mark">query:</span>
>
> <span class="mark">type: string</span>
>
> <span class="mark">default: ""</span>
>
> <span class="mark">is_chat_input: true</span>
>
> <span class="mark">outputs:</span>
>
> <span class="mark">reply:</span>
>
> <span class="mark">type: string</span>
>
> <span class="mark">reference: \${generateReply.output}</span>
>
> <span class="mark">is_chat_output: true</span>
>
> <span class="mark">documents:</span>
>
> <span class="mark">type: string</span>
>
> <span class="mark">reference: \${aggregateChunks.output}</span>
>
> <span class="mark">is_chat_output: false</span>
>
> <span class="mark">nodes:</span>
>
> <span class="mark">- name: formatRewriteIntentInputs</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path:
> formatConversationForIntentRewriting.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">history: \${inputs.chat_history}</span>
>
> <span class="mark">max_tokens: 2000</span>
>
> <span class="mark">query: \${inputs.query}</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: rewriteIntent</span>
>
> <span class="mark">type: llm</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path:
> ragcore/prompt_templates/rewriteIntent.jinja2</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">deployment_name: gpt-4</span>
>
> <span class="mark">temperature: 0.7</span>
>
> <span class="mark">top_p: 0.95</span>
>
> <span class="mark">max_tokens: 120</span>
>
> <span class="mark">presence_penalty: 0</span>
>
> <span class="mark">frequency_penalty: 0</span>
>
> <span class="mark">conversation:
> \${formatRewriteIntentInputs.output}</span>
>
> <span class="mark">provider: AzureOpenAI</span>
>
> <span class="mark">connection: copilotazureai3640805165_aoai</span>
>
> <span class="mark">api: chat</span>
>
> <span class="mark">module: promptflow.tools.aoai</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: extractSearchIntent</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: extractSearchIntent.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">intent: \${rewriteIntent.output}</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: queryProductIndex</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: package</span>
>
> <span class="mark">tool:
> promptflow_vectordb.tool.common_index_lookup.search</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">mlindex_content: \></span>
>
> <span class="mark">embeddings:</span>
>
> <span class="mark">api_base:
> https://copilotazureai3640805165.openai.azure.com</span>
>
> <span class="mark">api_type: Azure</span>
>
> <span class="mark">api_version: 2023-07-01-preview</span>
>
> <span class="mark">batch_size: '16'</span>
>
> <span class="mark">connection:</span>
>
> <span class="mark">id: \>-</span>
>
> <span class="mark">/subscriptions/2ad97659-df19-4123-ab60-775764ea635a/resourceGroups/AOAI-RG351/providers/Microsoft.MachineLearningServices/workspaces/contoso-outdoor-proj/connections/copilotazureai3640805165_aoai</span>
>
> <span class="mark">connection_type: workspace_connection</span>
>
> <span class="mark">deployment: text-embedding-ada-002</span>
>
> <span class="mark">dimension: 1536</span>
>
> <span class="mark">file_format_version: '2'</span>
>
> <span class="mark">kind: open_ai</span>
>
> <span class="mark">model: text-embedding-ada-002</span>
>
> <span class="mark">schema_version: '2'</span>
>
> <span class="mark">index:</span>
>
> <span class="mark">api_version: 2023-07-01-preview</span>
>
> <span class="mark">connection:</span>
>
> <span class="mark">id: \>-</span>
>
> <span class="mark">/subscriptions/2ad97659-df19-4123-ab60-775764ea635a/resourceGroups/AOAI-RG351/providers/Microsoft.MachineLearningServices/workspaces/contoso-outdoor-proj/connections/mysearchservice345</span>
>
> <span class="mark">connection_type: workspace_connection</span>
>
> <span class="mark">endpoint:
> https://mysearchservice345.search.windows.net/</span>
>
> <span class="mark">engine: azure-sdk</span>
>
> <span class="mark">field_mapping:</span>
>
> <span class="mark">content: content</span>
>
> <span class="mark">embedding: contentVector</span>
>
> <span class="mark">filename: filepath</span>
>
> <span class="mark">metadata: meta_json_string</span>
>
> <span class="mark">title: title</span>
>
> <span class="mark">url: url</span>
>
> <span class="mark">index: product-info</span>
>
> <span class="mark">kind: acs</span>
>
> <span class="mark">semantic_configuration_name: azureml-default</span>
>
> <span class="mark">queries: \${extractSearchIntent.output}</span>
>
> <span class="mark">query_type: Hybrid (vector + keyword)</span>
>
> <span class="mark">top_k: 5</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: chunkCustomerDocuments</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: chunkProductDocuments.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">data_source: Azure AI Search</span>
>
> <span class="mark">max_tokens: 1050</span>
>
> <span class="mark">queries: \${extractSearchIntent.output}</span>
>
> <span class="mark">query_type: Hybrid (vector + keyword)</span>
>
> <span class="mark">results: \${queryCustomerIndex.output}</span>
>
> <span class="mark">top_k: 5</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: selectCustomerChunks</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: filterChunks.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">min_score: 0.3</span>
>
> <span class="mark">results: \${chunkCustomerDocuments.output}</span>
>
> <span class="mark">top_k: 5</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: chunkProductDocuments</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: chunkProductDocuments.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">data_source: Azure AI Search</span>
>
> <span class="mark">max_tokens: 1050</span>
>
> <span class="mark">queries: \${extractSearchIntent.output}</span>
>
> <span class="mark">query_type: Hybrid (vector + keyword)</span>
>
> <span class="mark">results: \${queryProductIndex.output}</span>
>
> <span class="mark">top_k: 5</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: selectProductChunks</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: filterChunks.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">min_score: 0.3</span>
>
> <span class="mark">results: \${chunkProductDocuments.output}</span>
>
> <span class="mark">top_k: 5</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: shouldGenerateReply</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: shouldGenerateReply.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">chunks: \${aggregateChunks.output}</span>
>
> <span class="mark">queries: \${extractSearchIntent.output}</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: formatGenerateReplyInputs</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: formatReplyInputs.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">chunks: \${aggregateChunks.output}</span>
>
> <span class="mark">history: \${inputs.chat_history}</span>
>
> <span class="mark">max_conversation_tokens: 2000</span>
>
> <span class="mark">max_tokens: 5000</span>
>
> <span class="mark">query: \${inputs.query}</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: generateReply</span>
>
> <span class="mark">type: llm</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path:
> ragcore/prompt_templates/generateReply.jinja2</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">inputs: \${formatGenerateReplyInputs.output}</span>
>
> <span class="mark">deployment_name: gpt-4</span>
>
> <span class="mark">temperature: 0.7</span>
>
> <span class="mark">top_p: 0.95</span>
>
> <span class="mark">max_tokens: 800</span>
>
> <span class="mark">presence_penalty: 0</span>
>
> <span class="mark">frequency_penalty: 0</span>
>
> <span class="mark">indomain: "True"</span>
>
> <span class="mark">role_info: You are an AI assistant that helps
> people find information.</span>
>
> <span class="mark">provider: AzureOpenAI</span>
>
> <span class="mark">connection: copilotazureai3640805165_aoai</span>
>
> <span class="mark">api: chat</span>
>
> <span class="mark">module: promptflow.tools.aoai</span>
>
> <span class="mark">activate:</span>
>
> <span class="mark">when: \${shouldGenerateReply.output}</span>
>
> <span class="mark">is: true</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: queryCustomerIndex</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: package</span>
>
> <span class="mark">tool:
> promptflow_vectordb.tool.common_index_lookup.search</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">mlindex_content: \></span>
>
> <span class="mark">embeddings:</span>
>
> <span class="mark">kind: none</span>
>
> <span class="mark">schema_version: '2'</span>
>
> <span class="mark">index:</span>
>
> <span class="mark">api_version: 2023-07-01-preview</span>
>
> <span class="mark">connection:</span>
>
> <span class="mark">id:
> /subscriptions/2ad97659-df19-4123-ab60-775764ea635a/resourceGroups/AOAI-RG351/providers/Microsoft.MachineLearningServices/workspaces/contoso-outdoor-proj/connections/mysearchservice345</span>
>
> <span class="mark">connection_type: workspace_connection</span>
>
> <span class="mark">endpoint:
> https://mysearchservice345.search.windows.net/</span>
>
> <span class="mark">engine: azure-sdk</span>
>
> <span class="mark">field_mapping:</span>
>
> <span class="mark">content: content</span>
>
> <span class="mark">embedding: null</span>
>
> <span class="mark">metadata: meta_json_string</span>
>
> <span class="mark">index: customer-info</span>
>
> <span class="mark">kind: acs</span>
>
> <span class="mark">semantic_configuration_name: azureml-default</span>
>
> <span class="mark">queries: \${extractSearchIntent.output}</span>
>
> <span class="mark">query_type: Keyword</span>
>
> <span class="mark">top_k: 5</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">- name: aggregateChunks</span>
>
> <span class="mark">type: python</span>
>
> <span class="mark">source:</span>
>
> <span class="mark">type: code</span>
>
> <span class="mark">path: aggregateChunks.py</span>
>
> <span class="mark">inputs:</span>
>
> <span class="mark">input1: \${selectProductChunks.output}</span>
>
> <span class="mark">input2: \${selectCustomerChunks.output}</span>
>
> <span class="mark">use_variants: false</span>
>
> <span class="mark">node_variants: {}</span>
>
> <span class="mark">environment:</span>
>
> <span class="mark">python_requirements_txt: requirements.txt</span>

**Note**: **flow.dag.yaml** file is available in the C:\Labfiles

## **Task 4: Aggregate product and customer info**

At this point, the prompt flow only uses the product information.

- **extractSearchIntent** extracts the search intent from the user's
  question.

- **queryProductIndex** retrieves the product info from
  the *product-info* index.

- The **LLM** tool (for large language models) receives a formatted
  reply via
  the **chunkProductDocuments** \> **selectProductChunks** \> **formatGeneratedReplyInputs** nodes.

You need to connect and aggregate the product and customer info to
output it in a format that the **LLM** tool can use. Follow these steps
to aggregate the product and customer info:

1.  Switch off the  **Raw file mode** .

<img src="./media/image137.png"
style="width:5.78333in;height:4.41667in" />

2.  Select **Python** from the list of tools.

<img src="./media/image138.png"
style="width:7.11535in;height:4.42083in" />

3.  Name the tool **aggregateChunks** and select **Add**.

> <img src="./media/image139.png"
> style="width:6.49167in;height:4.91667in" />

4.  Copy and paste the following Python code to replace all contents in
    the **aggregateChunks** code block.

> PythonCopy
>
> from promptflow import tool
>
> from typing import List
>
> @tool
>
> def aggregate_chunks(input1: List, input2: List) -\> str:
>
> interleaved_list = \[\]
>
> for i in range(max(len(input1), len(input2))):
>
> if i \< len(input1):
>
> interleaved_list.append(input1\[i\])
>
> if i \< len(input2):
>
> interleaved_list.append(input2\[i\])
>
> return interleaved_list
>
> <img src="./media/image140.png"
> style="width:6.49167in;height:6.15833in" />

5.  Select the **Validate and parse input** button to validate the
    inputs for the **aggregateChunks** node. If the inputs are valid,
    prompt flow parses the inputs and creates the necessary variables
    for you to use in your code.

<img src="./media/image141.png" style="width:6.5in;height:6.03056in"
alt="Screenshot of the prompt flow node for aggregating product and customer information." />

6.  Edit the **aggregateChunks** node to connect the product and
    customer info. Set the **inputs** to the following values:

| **Name**   | **Type** | **Value**                         |
|------------|----------|-----------------------------------|
| **input1** | list     | *\${selectProductChunks.output}*  |
| **input2** | list     | *\${selectCustomerChunks.output}* |

> <img src="./media/image142.png"
> style="width:5.90833in;height:6.28333in" />

7.  Select the **shouldGenerateReply** node from the graph. Select or
    enter **\${aggregateChunks.output}** for the **chunks** input.

> <img src="./media/image143.png" style="width:5.7in;height:5.54167in" />

8.  Select the **formatGenerateReplyInputs** node from the graph. Select
    or enter **\${aggregateChunks.output}** for the **chunks** input.

> <img src="./media/image144.png" style="width:5.49167in;height:6in" />

9.  Select the **outputs** node from the graph. Select or
    enter **\${aggregateChunks.output}** for the **chunks** input.

> <img src="./media/image145.png" style="width:5.825in;height:6.2in" />

10. Select **Save** from the top menu to save your changes. Remember to
    save your prompt flow periodically as you make changes.

> <img src="./media/image146.png"
> style="width:6.93469in;height:3.19583in" />

## **Task 5: Chat in prompt flow with product and customer info**

By now you have both the product and customer info in prompt flow. You
can chat with the model in prompt flow and get answers to questions such
as "How many TrailWalker hiking shoes did Daniel Wilson buy?" Before
proceeding to a more formal evaluation, you can optionally chat with the
model to see how it responds to your questions.

1.  Continue from the previous section with the **outputs** node
    selected. Make sure that the **reply** output has the **Chat
    output** radio button selected. Otherwise, the full set of documents
    are returned in response to the question in chat.

> <img src="./media/image147.png"
> style="width:5.83333in;height:4.91667in" />

2.  Select **Chat** from the top menu in prompt flow to try chat.

<img src="./media/image148.png"
style="width:6.49167in;height:1.025in" />

3.  Enter "**How many TrailWalker hiking shoes did Daniel Wilson buy?**"
    and then select the right arrow icon to send.

> <img src="./media/image149.png"
> style="width:7.03044in;height:3.47917in" />

** Note:** It might take a few seconds for the model to respond. You can
expect the response time to be faster when you use a deployed flow

4.  The response is what you expect. The model uses the customer info to
    answer the question.

> <img src="./media/image150.png" style="width:6.5in;height:5.375in" />

# Exercise 4: Evaluate the flow using a question and answer evaluation dataset

## **Task 1: Deploy the flow**

Now that you [built a
flow](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-copilot-ai-studio#create-a-prompt-flow-from-the-playground) and
completed a
metrics-based [evaluation](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-copilot-ai-studio#evaluate-the-flow-using-a-question-and-answer-evaluation-dataset),
it's time to create your online endpoint for real-time inference. That
means you can use the deployed flow to answer questions in real time.

1.  In the Prompt flow pane, select **Deploy** on the flow editor.

<img src="./media/image151.png"
style="width:6.49167in;height:1.83333in" />

2.  Provide the requested information on the **Basic Settings** page in
    the deployment wizard. Select **Next** to proceed to the advanced
    settings pages.

<img src="./media/image152.png"
style="width:7.0125in;height:3.69079in" />

3.  On the **Advanced settings - Endpoint** page, leave the default
    settings and select **Next**.

> <img src="./media/image153.png"
> style="width:7.00751in;height:3.67917in" />

4.  On the **Advanced settings - Deployment** page, leave the default
    settings and select **Next**.

> <img src="./media/image154.png"
> style="width:7.0313in;height:3.6375in" />

5.  On the **Advanced settings - Outputs & connections** page, make sure
    all outputs are selected under **Included in endpoint response**.

6.  Select **Review + Create** to review the settings and create the
    deployment.

> <img src="./media/image155.png"
> style="width:7.10574in;height:3.7125in" />

7.  Select **Create** to deploy the prompt flow.

> <img src="./media/image156.png"
> style="width:7.00805in;height:3.5625in" />

## **Task 2: Use the deployed flow**

Your copilot application can use the deployed prompt flow to answer
questions in real time. You can use the REST endpoint or the SDK to use
the deployed flow.

1.  To view the status of your deployment AI studio,
    select **Deployments** from the left navigation.

> <img src="./media/image157.png" style="width:6.5in;height:6.125in" />
>
> <img src="./media/image158.png" style="width:6.5in;height:3.675in" />

2.  Select the contoso-outdoor-proj deployment. If you see a message
    that says "Currently this endpoint has no deployments" or the State
    is still Updating, you might need to select Refresh after a couple
    of minutes to see the deployment.

> <img src="./media/image158.png" style="width:6.5in;height:3.675in" />
>
> <img src="./media/image159.png"
> style="width:6.87604in;height:3.35417in" />
>
> <img src="./media/image160.png"
> style="width:7.12233in;height:3.52917in" />

## **Task 3: Create an evaluation**

1.  In the Azure AI Studio page, select **Prompt flow** from the left
    menu

<img src="./media/image161.png" style="width:6.5in;height:4.99167in" />

2.  Select the **Contoso outdoor flow** prompt flow

<img src="./media/image162.png"
style="width:6.49167in;height:2.59167in" />

3.  Select **Evaluate** \> **Built-in evaluation** from the top menu in
    prompt flow.

> <img src="./media/image163.png"
> style="width:6.49167in;height:3.20833in" />

4.  In the **Create a new evaluation** wizard, enter a name for your
    evaluation i.e **evaluate_from_flow**.

5.  Select **Question and answer without context** from the scenario
    options.

6.  Select the flow to evaluate. In this example, select ***Contoso
    outdoor flow*** or whatever you named your flow. Then
    select **Next**.

<img src="./media/image164.png"
style="width:7.32318in;height:4.18333in" />

7.  Select **Add your dataset** on the **Configure test data** page.
    Click on **Upload file**.

<img src="./media/image165.png"
style="width:7.125in;height:4.58232in" />

8.  Navigate to **C:\Labfiles** location and select
    **qa-evaluation.jsonl ,** then click on **Open** button.

<img src="./media/image166.png"
style="width:7.12524in;height:3.04583in" />

9.  After the file is uploaded, you need to configure your data columns
    to match the required inputs for prompt flow to execute a batch run
    that generate output for evaluation. Enter or select the following
    values for each data set mapping for prompt flow.

10. Select **Next**.

| **Name**         | **Description**  | **Type** | **Data source**         |
|------------------|------------------|----------|-------------------------|
| **chat_history** | The chat history | list     | *\${data.chat_history}* |
| **query**        | The query        | string   | *\${data.question}*     |

<img src="./media/image167.png" style="width:6.5in;height:4.275in" />

11. Select the metrics you want to use to evaluate your flow. In this
    example, select Coherence, Fluency, GPT similarity, and F1 score.

12. Select a connection and model to use for evaluation. In this
    example, select **gpt-4**. Then select **Next**.

<img src="./media/image168.png" style="width:6.5in;height:3.95833in" />

**Note:** Evaluation with AI-assisted metrics needs to call another GPT
model to do the calculation. For best performance, use a model that
supports at least 16k tokens such as gpt-4-32k or gpt-35-turbo-16k
model. If you didn't previously deploy such a model, you can deploy
another model by following the steps in [**the AI Studio chat playground
quickstart**](https://learn.microsoft.com/en-us/azure/ai-studio/quickstarts/get-started-playground#deploy-a-chat-model).
Then return to this step and select the model you deployed.

13. You need to configure your data columns to match the required inputs
    to generate evaluation metrics. Enter the following values to map
    the dataset to the evaluation properties and click on **Next**
    button.

| **Name** | **Description** | **Type** | **Data source** |
|----|----|----|----|
| **question** | A query seeking specific information. | string | *\${data.question}* |
| **answer** | The response to question generated by the model as answer. | string | \${run.outputs.reply} |
| **documents** | String with context from retrieved documents. | string | \${run.outputs.documents} |

<img src="./media/image169.png"
style="width:6.49167in;height:4.38333in" />

14. Review the evaluation details and then select **Submit**. You're
    taken to the **Metric evaluations** page.

<img src="./media/image170.png" style="width:6.5in;height:4.7in" />

## **Task 4: View the evaluation status and results**

1.  After you [create an
    evaluation](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-copilot-ai-studio#create-an-evaluation),
    if you aren't there already go to the **Evaluation**. On
    the **Metric evaluations** page, you can see the evaluation status
    and the metrics that you selected. You might need to
    select **Refresh** after a couple of minutes to see
    the **Completed** status.

> <img src="./media/image171.png" style="width:6.5in;height:4.46597in" />
>
> <img src="./media/image172.png"
> style="width:6.49167in;height:4.08333in" />
>
> <img src="./media/image173.png" style="width:6.5in;height:4.01667in" />

2.  Select your Evaluation flow

> <img src="./media/image173.png" style="width:6.5in;height:4.01667in" />
>
> <img src="./media/image174.png"
> style="width:6.49167in;height:3.79167in" />
>
> <img src="./media/image175.png" style="width:6.5in;height:3.54097in"
> alt="A screenshot of a computer Description automatically generated" />

**Tip:** Once the evaluation is in **Completed** status, you don't need
a compute session to complete the rest of this tutorial. You can stop
your compute instance to avoid incurring unnecessary Azure costs. For
more information, see [**how to start and stop
compute**](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/create-manage-compute#start-or-stop-a-compute-instance).

## Task 5: Clean up resources

To avoid incurring unnecessary Azure costs, you should delete the
resources you created in this quickstart if they're no longer needed. To
manage resources, you can use the [Azure
portal](https://portal.azure.com/?azure-portal=true).

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

> <img src="./media/image176.png" style="width:6.5in;height:4.58472in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the assigned resource group.

> <img src="./media/image177.png" style="width:6.49167in;height:4.15833in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Carefully select all resources except Azure Open AI service (that
    you have created in **Lab 1**).

**Note**: Don’t select Azure OpenAI service.

4.  In the Resource group page, navigate to
    <span class="mark">the</span> command bar and click on **Delete**.

**Important Note**: Don’t click on **Delete resource group**. If you
don’t see the **Delete** option in the command bar, then click on the
horizontal ellipsis.

<img src="./media/image178.png"
style="width:7.09619in;height:3.17917in" />

5.  In the **Delete Resources** pane that appears on the right side,
    enter the **delete** and click on **Delete** button.

<img src="./media/image179.png" style="width:6.10053in;height:7.01727in"
alt="A screenshot of a computer Description automatically generated" />

6.  On **Delete confirmation** dialog box, click on D**elete** button.

> <img src="./media/image180.png" style="width:5.06711in;height:3.50447in"
> alt="A screenshot of a computer Description automatically generated" />

7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 4 selected items.**

**Summary:**

This use case walks users through deploying a custom chat application
with PostgreSQL and OpenAI on Azure, focusing on cloud-based application
deployment and management.. In this lab, you’ve set up the development
environment, installed necessary tools like Azure CLI and Node.js,
configured Azure resources using Azure Developer CLI, and deployed the
application to Azure Container Apps. In this lab, you’ve gained
proficiency in managing Azure resources, integrating OpenAI for advanced
chat functionalities, and ensuring proper deployment and verification
through Azure Portal. You’ve acquired hands-on experience in deploying
scalable, cloud-native applications with integrated AI capabilities on
Microsoft Azure.

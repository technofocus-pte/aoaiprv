**Lab 08: Implementing Q&A using semantic answering**

**Introduction**

A simple web application for an OpenAI-enabled document search. This
repo uses Azure OpenAI Service for creating embeddings vectors from
documents. For answering the question of a user, it retrieves the most
relevant document and then uses GPT-3 to extract the matching answer for
the question.

<img src="./media/image1.png" style="width:6.5in;height:3.65625in"
alt="Architecture" />

**Prerequisites**

- Before starting this Lab complete Lab \#1 - Provisioning Azure OpenAI
  resource.

**Objectives**

- To deploy chat and embedding models in Azure AI Studio.

- To use a custom template for deploying the required resources such as
  App Service, Search Service, Form recognizer, etc.

- To deploy aoaichatsearch-site Web App and perform Azure OpenAI-enabled
  document search, text summarization, and conversation data extraction.

- To delete the deployed resources and models.

## **Task 1: Deploy the Chat model and Embedding model**

1.  Open your browser, navigate to the address bar, and type or paste
    the following UR: <https://oai.azure.com/> then press the **Enter**
    button.

> <img src="./media/image2.png" style="width:5.60417in;height:2.1625in" />
>
> **Note**: If you are directed to the **Azure OpenAI Studio** home
> page, then skip steps \#2 to \#4, else
> continue<span class="mark">.</span>

2.  In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

> <img src="./media/image3.png" style="width:3.69583in;height:3.59653in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Then, enter the password and click on the **Sign in** button**.**

> <img src="./media/image4.png" style="width:4.5in;height:3.56042in"
> alt="A screenshot of a login box Description automatically generated" />

4.  In **Stay signed in?** window, click on the **Yes** button.

> <img src="./media/image5.png" style="width:4.46806in;height:2.98617in"
> alt="Graphical user interface, application Description automatically generated" />

5.  On the **Welcome to Azure OpenAI Studio** dialog box, under the
    **Subscription** field, enter the subscription assigned to you, and
    in the **Resource** field, select the Resource name that you’ve
    created in Lab \#1, and then click on the **Use resource** button.

<img src="./media/image6.png" style="width:5.80278in;height:4.97708in"
alt="A screenshot of a computer Description automatically generated" />

6.  Wait for the Azure OpenAI studio to launch.

<img src="./media/image7.png" style="width:5.74752in;height:3.23544in"
alt="A screenshot of a computer Description automatically generated" />

7.  On the **Azure OpenAI Studio** homepage, click on **Create new
    deployment** button.

<img src="./media/image8.png" style="width:6.49167in;height:4.81667in"
alt="A screenshot of a computer Description automatically generated" />

8.  In the **Deployments** page, click on +**Create new deployment**.

> <img src="./media/image9.png" style="width:4.24432in;height:3.35078in"
> alt="A screenshot of a computer Description automatically generated" />

9.  In the **Deploy model dialog** box, under the **Model name** field,
    click on the V chevron button; navigate and select carefully
    **gpt-4**.

10. Select the **Model version** as **0125-Preview,** in the
    **Deployment type** as **Standard, Deployment name field**, enter
    **gpt-4**, and click on the **Create** button.

> <img src="./media/image10.png" style="width:5.075in;height:4.95in" />

11. You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded. (You can also view the
    notification by clicking on the bell icon beside **Azure AI \| Azure
    OpenAI Studio**).

<img src="./media/image11.png" style="width:4.58373in;height:1.30011in"
alt="A screenshot of a phone Description automatically generated" />

12. In the **Deployments** page, click on +**Create new deployment**.

<img src="./media/image12.png"
style="width:7.04512in;height:4.25417in" />

13. In the **Deploy model dialog** box, under the **Model name** field,
    click on the V chevron button; navigate and carefully select
    **text-embedding-ada-002**. Select the **Model version** as **2
    (Default),** in the **Deployment name field**, enter
    **text-embedding-ada-002**, and click on the **Create** button.

<img src="./media/image13.png"
style="width:6.13333in;height:5.09167in" />

14. You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded. (You can also view the
    notification by clicking on the bell icon beside **Azure AI \| Azure
    OpenAI Studio**).

<img src="./media/image14.png" style="width:6.26667in;height:2.175in" />

## **Task 2: Deploy on Azure (WebApp + Batch Processing) with Azure Cognitive Search**

1.  Open your edge browser, navigate to the address bar, and type or
    paste the following URL:
    <https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fruoccofabrizio%2Fazure-open-ai-embeddings-qna%2Fmain%2Finfrastructure%2Fdeployment_ACS.json>
    then press the **Enter** button.

<img src="./media/image15.png"
style="width:6.49167in;height:2.25833in" />

2.  On **Custom deployment** window, under the **Basics** tab, enter the
    following details to deploy the custom template and then click on
    **Review + create.**

| **Subscription** | Select your Azure OpenAI subscription |
|----|----|
| **Resource group** | Select the Resource group that you’ve created in **Lab \#1** |
| **Resource Prefix** | **aoaichatsearchXXXX+++**(can be a unique name) |
| **Azure Cognitive Search Sku** | Standard |
| **Hosting plan Sku** | B3 |
| **OpenAI Name** | Enter your OpenAI name that you have created in **Lab \#1** (here, we entered Azure-openai-test21) |
| **OpenAI Key** | Enter your OpenAI key that you have saved in your notepad in **Lab \#1\>Task \#2** |
| **Open AI Engine** | **gpt-4** |
| **Open AI Deployment Type** | **Chat** |
| **Open AI Embeddings Engine Doc** | text-embeddeding-ada-002 |
| **Open AI Embeddings Engine Query** | text-embeddeding-ada-002 |

<img src="./media/image16.png"
style="width:6.97549in;height:5.92917in" />

<img src="./media/image17.png"
style="width:7.09139in;height:5.54583in" />

3.  On **Review + create** tab, once the Validation is Passed, click on
    the **Create** button.

<img src="./media/image18.png" style="width:6.49167in;height:6.875in" />

4.  Wait for the deployment to complete. The deployment will take around
    15-17 minutes.

> <img src="./media/image19.png" style="width:6.5in;height:3.39583in"
> alt="A screenshot of a computer Description automatically generated" />

5.  Click on the **Go to resource group** button.

> <img src="./media/image20.png" style="width:6.5in;height:4.50833in" />

## **Task 3: Azure OpenAI-enabled document search through web application**

1.  On the **aoaiXXX-RG** resource group window, under **Resources**
    tab, navigate to the **App Service** - **aoaaichatsearch-site** and
    click on it.

<img src="./media/image21.png"
style="width:7.36198in;height:4.80417in" />

2.  On **aoaichatsearch-site** Web App **Overview** page, navigate to
    the command bar and click on **Browse**, it will navigate you to the
    web application.

<img src="./media/image22.png"
style="width:7.23012in;height:4.6625in" />

3.  Wait for the web application deployment to complete. The deployment
    will take approximately **10-15** minutes.

<img src="./media/image23.png" style="width:5.66184in;height:3.87376in"
alt="A screenshot of a computer Description automatically generated" />

4.  On the web application home page, to verify the deployments status
    click on the **Check deployments** button under Microsoft.

<img src="./media/image24.png"
style="width:6.49167in;height:4.08333in" />

5.  To check the deployment status, it may take around 5-6 min.

<img src="./media/image25.png" style="width:6.5in;height:2.56667in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image26.png" style="width:6.5in;height:4.3125in" />

6.  On Web App home page, navigate and click on **Add Document** on the
    left-hand side to add the data.

<img src="./media/image27.png" style="width:6.5in;height:4.01667in" />

7.  On **Add Document** pane, click on the **Browse files** button to
    upload documents that needs to be added to the knowledge base.

<img src="./media/image28.png"
style="width:7.26875in;height:2.67206in" />

8.  Navigate to **C:\Labfiles\Contoso Electronics** location in the VM
    and select **Benefit_Options.pdf,** then click on **Open** button.

<img src="./media/image29.png" style="width:6.5in;height:4.10625in" />

9.  Click again on the **Browse files,** navigate to
    **C:\Labfiles\Contoso Electronics** location in the VM and select
    **employee_handbook.pdf**, then click on **Open** button.

<img src="./media/image30.png" style="width:6.5in;height:2.58333in" />

<img src="./media/image31.png" style="width:6.5in;height:4.08333in" />

10. Similarly, add **Northwind_Health_Plus_Benefits_Details.pdf** and
    **Northwind_Standard_Benefits_Details.pdf**

<img src="./media/image32.png" style="width:6.5in;height:4.16667in" />

<img src="./media/image33.png" style="width:6.5in;height:4.61111in" />

11. The uploaded data will be added to the knowledge base and it’ll take
    approximately 5-7 minutes.

12. Click on **Document Management** to verify whether the files are
    successfully uploaded or not.

<img src="./media/image34.png"
style="width:7.32765in;height:3.75357in" />

<img src="./media/image35.png"
style="width:7.38399in;height:3.82137in" />

13. Click on **Index Management** to verify the files, keys, and source.

<img src="./media/image36.png"
style="width:7.32358in;height:2.82008in" />

14. Then, click on **Chat.**

<img src="./media/image37.png"
style="width:6.40903in;height:4.56042in" />

15. In the **Chat session** section, enter the following prompt, then
    press the **Enter** button and view the response.

**You**: **what is the employee's portion of the healthcare cost from
each paycheck in Contoso Electronics**

<img src="./media/image38.png"
style="width:7.26433in;height:2.39583in" />

<img src="./media/image39.png" style="width:6.5in;height:5in" />

16. In the **Chat session** section, click on the **Clear chat** button.

<img src="./media/image40.png"
style="width:6.07008in;height:3.66906in" />

17. In the **Chat session** section, enter the following prompt, then
    press the **Enter** button and view the response.

**You**: **How do I file a complaint or appeal with Northwind Health
Plus?**

<img src="./media/image41.png"
style="width:6.55042in;height:4.19129in" />

18. In the **Chat session** section, click on the **Clear chat** button.

<img src="./media/image42.png" style="width:6.5in;height:3.83333in" />

19. In the **Chat session** section, enter the following prompt. then
    press the **Enter** button and view the response.

**You**: **Does my plan covers my eye exams?**

<img src="./media/image43.png"
style="width:6.49236in;height:3.35625in" />

20. Click on **Utils-Document Summary** on the left-hand side.

<img src="./media/image44.png"
style="width:6.49236in;height:3.58333in" />

21. In the **Summarization** section, select the **Basic Summary** radio
    button**.**

<img src="./media/image45.png"
style="width:6.49236in;height:3.55278in" />

22. In the **Summarization** window, under **Enter some text to
    summarize** section, in the message box, replace the current text
    with the following, then click on the **Summarize** button.

<span class="mark">It’s been six months since we reinvented search
with [the new AI-powered Bing and
Edge](https://blogs.microsoft.com/blog/2023/02/07/reinventing-search-with-a-new-ai-powered-microsoft-bing-and-edge-your-copilot-for-the-web/).
In that short time, you’ve engaged in so many unique and creative ways;
to date we’ve seen over 1 billion chats and over 750 million images fill
the world of Bing! We’ve also seen nine consecutive quarters of growth
on Edge, meaning we’re more able than ever to bring our best-in-class AI
experiences to users across the web.</span>

<img src="./media/image46.png"
style="width:7.34678in;height:2.57765in" />

23. Check the summary of the text that you’ve entered.

<img src="./media/image47.png" style="width:6.5in;height:3.98472in" />

24. After reviewing the Summary result, click on the **Clear summary**
    button.

<img src="./media/image48.png" style="width:6.5in;height:4.09861in" />

25. Now, scroll up and select the **Bullet Points** radio button.
    Under **Enter some text to summarize** section, in the message box,
    replace the current text with the following and then click on the
    **Summarize** button.

<span class="mark">Microsoft has made its Azure OpenAI Service generally
available, bringing the enterprise generative AI tools out of its
invite-only program. Now any customers who meet Microsoft’s standards
can access the professional versions of OpenAI’s large language model
GPT-3.5 and the related text-to-image tool DALL-E 2, computer
programming assistant Codex, and the popular ChatGPT chatbot interface
for the LLM.</span>

<span class="mark">Microsoft launched the Azure OpenAI Service with an
eye toward offering businesses a way to develop apps without coding,
write reports, and put together marketing content. The scope has grown
since then to encompass new facets of the OpenAI’s models, including
chat and visuals. Those interested in the tools have to explain how they
will use the AI tools and agree to Microsoft’s ethical guidelines in
their application for access. The decision to widen the Azure OpenAI
Service’s availability arrives in tandem with Microsoft’s plans to
integrate ChatGPT and DALL-E into its Office suite, Bing search engine,
and other consumer products. Azure OpenAI Service followed earlier
experiments to integrate GPT-3 into Microsoft projects like the low-code
Power Apps programming tool and the GitHub Copilot programming
assistant.</span>

<img src="./media/image49.png" style="width:6.5in;height:3.59097in" />

26. You’ll see the summary results in the form of bullet points.

<img src="./media/image50.png" style="width:6.5in;height:4.28056in" />

27. Click on **Utils-Conversation Data Extraction** on the left side.

<img src="./media/image51.png"
style="width:5.37311in;height:4.55182in" />

28. On the **Conversation data extraction** pane, click on the **Execute
    tasks** and view the response under **OpenAI result**.

<img src="./media/image52.png"
style="width:6.49236in;height:3.93194in" />

29. Review the data extracted from the conversation between the Agent
    and the User.

<img src="./media/image53.png"
style="width:5.56117in;height:2.60133in" />

## Task 4: Deleting the deployed resources and models

1.  To delete the deployed resources, navigate to **Azure portal home**
    page, click on **Resource groups**.

> <img src="./media/image54.png" style="width:6.5in;height:4.58472in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the Resource groups page, select your resource group.

> <img src="./media/image55.png" style="width:6.5in;height:3.10694in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Select all the deployed resources except **Azure OpenAI Service**.

**Important Note:** Please do not select and delete the **Azure OpenAI
Service** (Azure-openai-testXX), as the same service will be used in
other labs.

> <img src="./media/image56.png" style="width:6.5in;height:3.83333in" />
>
> <img src="./media/image57.png" style="width:6.5in;height:3.91667in" />

4.  In the Resource group page, navigate to command bar and click on
    **Delete**.

**Note**: Don’t click on **Delete resource group**. If you don’t see the
**Delete** option in the command bar, then click on the horizontal
ellipsis, then navigate and click on **Delete**.

<img src="./media/image58.png"
style="width:7.31348in;height:2.16667in" />

5.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “delete” to confirm deletion** field, type
    **delete,** then click on **Delete** button.

> <img src="./media/image59.png"
> style="width:5.3125in;height:7.20139in" />

6.  On **Delete confirmation** dialog box, click on **Delete** button.

> <img src="./media/image60.png"
> style="width:4.48611in;height:2.68056in" />

7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 10 selected items.**

> <img src="./media/image61.png" style="width:5.30879in;height:2.13352in"
> alt="A screenshot of a computer Description automatically generated" />

8.  Go back to **Azure AI Studio** page, click on **Deployments** on the
    left side navigation menu, then select **text-embedding-ada-002
    model** and click on **Delete deployment** in the command bar.

<img src="./media/image62.png"
style="width:6.39583in;height:3.74722in" />

9.  On **Confirm delete** dialog box, click on **Delete** button.

<img src="./media/image63.png" style="width:6.5in;height:3.8375in" />

10. You’ll receive a notification stating – **Successfully Deleted
    deployment text-embedding-ada-002.**

<img src="./media/image64.png"
style="width:4.35175in;height:1.56571in" />

11. Similarly, delete **gpt-35-turbo model**.

**Summary**

You've deployed gpt-35-turbo chat model and text-embedding-ada-002
embedding model in your Azure AI Studio, then you’ve deployed the
necessary resources using a custom template. You've uploaded
unstructured documents in aoaichatsearch-site Web App and extracted the
precise information in a chat session. You've generated basic as well as
bullet points summary from sample texts, then you've extracted the data
from a conversation. At the end of the lab, you've deleted the resources
and models to efficiently manage your Azure OpenAI resources.

**Important Note: Please do not delete the Resource Group. If deleted,
you’ll not be able to proceed with the next lab or create a new Resource
Group.**

**Please do not delete the Azure OpenAI Service (Azure-openai-testXX).
The same service will be used throughout all the labs.**
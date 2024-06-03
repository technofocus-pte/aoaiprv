# Lab 11 -Chat with your data using RAG Solution accelerator

**Introduction**

 The *Chat with your data* Solution accelerator is a powerful tool that
combines the capabilities of Azure AI Search and Large Language Models
(LLMs) to create a conversational search experience. This solution
accelerator uses an Azure OpenAI GPT model and an Azure AI Search index
generated from your data, which is integrated into a web application to
provide a natural language interface, including speech-to-text
functionality, for search queries. Users can drag and drop files, point
to storage, and take care of technical setup to transform documents.
There is a web app that users can create in their own subscription with
security and authentication.

The sample data illustrates how this accelerator could be used in the
financial services industry (FSI).

In this scenario, a financial advisor is preparing for a meeting with a
potential client who has expressed interest in Woodgrove Investments’
Emerging Markets Funds. The advisor prepares for the meeting by
refreshing their understanding of the emerging markets fund's overall
goals and the associated risks.

Now that the financial advisor is more informed about Woodgrove’s
Emerging Markets Funds, they're better equipped to respond to questions
about this fund from their client.

Note: Some of the sample data included with this accelerator was
generated using AI and is for illustrative purposes only.

<img src="./media/image1.png" style="width:7.27307in;height:4.08333in"
alt="Solution Architecture - Chat with your data" />

## Task 1: Deploy infrastructure from template

1.  Open your browser, navigate to the address bar, and type or paste
    the following UR: !!
    [www.portal.azure.com/](https://portal.azure.com/) !!then press the
    **Enter** button.

2.  In the **Microsoft Azure** window, enter your **Sign-in**
    credentials, and click on the **Next** button.

> <img src="./media/image2.png" style="width:3.69583in;height:3.59653in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Then, enter the password and click on the **Sign in** button**.**

> <img src="./media/image3.png" style="width:4.5in;height:3.56042in"
> alt="A screenshot of a login box Description automatically generated" />

4.  In **Stay signed in?** window, click on the **Yes** button.

> <img src="./media/image4.png" style="width:4.46806in;height:2.98617in"
> alt="Graphical user interface, application Description automatically generated" />

5.  Open a new browser and enter the following URL in the address bar:
    <https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fchat-with-your-data-solution-accelerator%2Fmain%2Finfra%2Fmain.json>
    to open the Azure Portal.

6.  On **Custom deployment** window, under the **Basics** tab, enter the
    following details to deploy the custom template and then click on
    **Review + create.**

| **Environment Name** | Enter RAGSolutionXX(XXXcan be a unique name) |
|----------------------|----------------------------------------------|
| **Location**         | East US                                      |

<img src="./media/image5.png" style="width:5.3125in;height:5.65068in" />

7.  On **Review + create** tab, once the Validation is Passed, click on
    the **Create** button.

<img src="./media/image6.png" style="width:6.5in;height:6.61667in" />

8.  Wait for the deployment to complete. The deployment will take around
    17-19 minutes.

9.  Click on the **Go to Subscription** button

<img src="./media/image7.png"
style="width:7.10526in;height:3.32917in" />

## Task 2: Verify deployed resources in the Azure portal

1.  On the Home page, click on **Resource Groups**.

> <img src="./media/image8.png" style="width:6.49167in;height:3.625in" />

2.  Click on your resource group name **rg-RAGSolutionXX**

> <img src="./media/image9.png" style="width:6.425in;height:3.40833in" />

3.  Make sure the below resource got deployed successfully into East US
    region

- Azure App Service

- Azure Application Insights

- Azure Bot

- Azure OpenAI

- Azure Document Intelligence

- Azure Function App

- Azure Search Service

- Azure Storage Account

- Azure Speech Service

<img src="./media/image10.png"
style="width:7.34345in;height:3.95417in" />

<img src="./media/image11.png"
style="width:7.31319in;height:3.90538in" />

## Task 3: Testing the deployment

1.  On the resource group and click on **Web-** {RESOURCE_TOKEN} **-
    admin-docker** resource name.

<img src="./media/image12.png"
style="width:6.96308in;height:3.44583in" />

2.  Navigate to the admin site
    https://web-{RESOURCE_TOKEN}-admin.azurewebsites.net/

<img src="./media/image13.png"
style="width:7.43013in;height:2.82917in" />

<img src="./media/image14.png" style="width:7.34371in;height:3.59889in"
alt="A screenshot of a computer Description automatically generated" />

3.  In **Chat with your data Solution Accelerator** page, from the left
    navigation menu select **Ingest Data.**

<img src="./media/image15.png"
style="width:7.02739in;height:2.7875in" />

4.  In the Add documents Batch pane, Click on **Browse file** and
    navigate to **C:\Labfiles \data** location and select **all files,**
    then click on **Open** button.

<img src="./media/image16.png"
style="width:7.12807in;height:2.97917in" />

<img src="./media/image17.png" style="width:6.5in;height:4.10833in" />

5.  To upload files will take 1-2 minutes

<img src="./media/image18.png"
style="width:7.37092in;height:3.7375in" />

6.  Click on the **Reprocess all documents in the Azure Storage
    account.**

<img src="./media/image19.png"
style="width:7.22606in;height:3.32083in" />

<img src="./media/image20.png" style="width:7.39301in;height:3.56855in"
alt="A screenshot of a chat Description automatically generated" />

7.  In **Chat with your data Solution Accelerator** page, from the left
    navigation menu select **Configuration** and select the **check box-
    Enable post-answering prompt.**

<img src="./media/image21.png" style="width:6.5in;height:3.70833in" />

8.  In the configuration pane , Click on the **Save configuration.**

<img src="./media/image22.png" style="width:6.5in;height:3.51667in" />

<img src="./media/image23.png" style="width:6.5in;height:3.70833in" />

9.  Go back to the resource group page and click on **the Storage
    account** name

<img src="./media/image24.png"
style="width:6.49236in;height:3.37847in" />

10. From the left navigation menu, click on **Containers.**

<img src="./media/image25.png"
style="width:6.49236in;height:4.75764in" />

11. In the Containers page, select **documents**.

<img src="./media/image26.png"
style="width:7.01522in;height:3.27462in" />

12. Make sure all the files should be deployed successfully

<img src="./media/image27.png" style="width:7.12448in;height:4.11103in"
alt="A screenshot of a computer Description automatically generated" />

13. Go back to the resource group page

<img src="./media/image28.png" style="width:6.5in;height:3.86389in" />

14. In the resource group page, select App service as
    **web-{RESOURCE_TOKEN}-docker**

<img src="./media/image29.png"
style="width:7.01577in;height:4.5625in" />

15. On Web App **Overview** page, navigate to the command bar and click
    on **Browse**, it will navigate you to the web application.

<img src="./media/image30.png"
style="width:7.31819in;height:3.74432in" />

<img src="./media/image31.png" style="width:6.5in;height:3.51042in"
alt="A screenshot of a computer Description automatically generated" />

16. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

**Describe in more detail the risks from market volatility**

<img src="./media/image32.png"
style="width:7.08044in;height:3.75947in" />

<img src="./media/image33.png"
style="width:7.35498in;height:3.63068in" />

17. In the **Chat session** section, select the references link and
    observe the details of search document on right side of the page.

<img src="./media/image34.png"
style="width:7.33448in;height:3.54735in" />

18. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

**CodeCopy**

**How does Woodgrove Financial handle payroll taxes for employees
outside the U.S.?**

<img src="./media/image35.png"
style="width:7.15814in;height:4.63826in" />

<img src="./media/image36.png"
style="width:7.33018in;height:3.5625in" />

19. In the **Azure AI** web app page, enter the following text and click
    on the **Submit icon** as shown in the below image.

What is FORM 10-K and explain?

<img src="./media/image37.png"
style="width:6.49236in;height:4.46181in" />

## **Task 4: Delete Azure OpenAI Resource**

1.  To Azure OpenAI resource , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

> <img src="./media/image38.png" style="width:6.5in;height:4.22569in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on your resource group.

> <img src="./media/image9.png" style="width:6.425in;height:3.40833in" />

3.  On an overview page of resource group Select the **Delete resource
    group**

<img src="./media/image39.png"
style="width:6.49236in;height:4.03056in" />

4.  In the **Delete Resources** pane that appears on the right side,
    enter the **resource group name** and click on **Delete** button.

<img src="./media/image40.png"
style="width:5.46944in;height:7.28056in" />

5.  On **Delete confirmation** dialog box, click on D**elete** button.

<img src="./media/image41.png"
style="width:2.93958in;height:1.66667in" />

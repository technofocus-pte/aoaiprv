**Use case 9 - Performing advanced data analytics on business database
and answering business questions using Azure OpenAI Service**

**Introduction**

This lab delves into the integration of Azure OpenAI capabilities to
answer business questions through advanced data analytics performed on a
business database. Leveraging the power of Open AI, such as
ChatGPT/GPT-4, you’ll learn to construct complex queries and glean
insights from the data. The lab showcases the application's versatility
by addressing questions of varying complexity, such as revenue trends
and forecasting.

 Examples of questions are:

- **Simple**: Show me daily revenue trends in 2016 per region

- **More difficult**: Is that true that top 20% customers generate 80%
  revenue in 2016?

- **Advanced**: Forecast monthly revenue for next 12 months starting
  from June-2018

This integration supports both Python's built-in SQLITE and Microsoft
SQL Server, providing a comprehensive analytical toolset for businesses.

**Objectives**

- To deploy gpt-35-turbo model in Azure OpenAI Studio in order to
  facilitate the subsequent business question analysis.

- To efficiently create an Azure SQL Database with relevant
  configurations in preparation for data analysis tasks.

- To configure the hosted demo application and use SQL Query Writing
  Assistant and Data Analysis Assistant of the demo app for SQL query
  translation and advanced data analysis.

- To delete the gpt-35-turbo model, SQL database, and SQL server.

*Important: You can proceed with this lab only GPT-4 is available on
your Azure OpenAI Service. If it is not approved, you can request access
to GPT-4* [*https://aka.ms/oai/get-gpt4*](https://aka.ms/oai/get-gpt4)

## **Task 1: Create Azure OpenAI resource**

1.  In Azure portal, click on **portal menu** represented by three
    horizontal bars on the top left corner of page, as shown in the
    below image.

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

4.  In the **Marketplace** page, navigate to the **Azure OpenAI** tile,
    click on the V chevron button beside **Create**, then navigate and
    click on the **Azure OpenAI** as shown in the below image.

> <img src="./media/image4.png" style="width:4.8625in;height:5.056in"
> alt="A screenshot of a computer Description automatically generated" />

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

| **Subscription** | Select your subscription |
|----|----|
| **Resource group** | Click on **Create new**\> enter **AOAI-RGXX** (XX can be a unique number) |
| **Region** | For this lab, you will use a **GPT-4** model. This model is currently only available in [certain regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models). Please select a region from this list, In this lab **West US** is using for this resource |
| **Name** | **azure-openai-testXX** (XX can be a unique number) |
| **Pricing tier** | Select **Standard S0** |

<img src="./media/image5.png" style="width:6.5in;height:3.99861in" />

<img src="./media/image6.png" style="width:6.5in;height:5.05625in"
alt="A screenshot of a computer Description automatically generated" />

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> <img src="./media/image7.png" style="width:5.58101in;height:5.89583in"
> alt="A screenshot of a computer Description automatically generated" />

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> <img src="./media/image8.png" style="width:5.1625in;height:6.08222in"
> alt="A screenshot of a computer Description automatically generated" />

8.  In the **Review + submit** tab, once the Validation is Passed, click
    on the **Create** button.

> <img src="./media/image9.png" style="width:6.5in;height:5.47431in"
> alt="A screenshot of a computer Description automatically generated" />

9.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

<img src="./media/image10.png" style="width:6.5in;height:3.56806in"
alt="A screenshot of a computer Description automatically generated" />

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on **Go to resource** button.

<img src="./media/image11.png" style="width:6.5in;height:3.73472in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 2: Deploy the models in Azure OpenAI**

1.  In **azure-openai-testXXX** page, navigate and click on **Go to
    Azure OpenAI Studio** as shown in the below image.

<img src="./media/image12.png" style="width:6.5in;height:3.93333in" />

2.  Wait for the Azure OpenAI studio to launch.

<img src="./media/image13.png" style="width:6.38037in;height:3.59169in"
alt="A screenshot of a computer Description automatically generated" />

3.  On the **Azure OpenAI Studio** homepage, click on **Create new
    deployment** button.

<img src="./media/image14.png" style="width:6.49167in;height:4.81667in"
alt="A screenshot of a computer Description automatically generated" />

4.  In the **Deployments** page, click on +**Create new deployment**.

> <img src="./media/image15.png" style="width:4.24432in;height:3.35078in"
> alt="A screenshot of a computer Description automatically generated" />

5.  In the **Deploy model dialog** box, under the **Model name** field,
    click on the V chevron button; navigate and select carefully
    **gpt-35-turbo**.

> <img src="./media/image16.png" style="width:6.16667in;height:4.43333in"
> alt="A screenshot of a computer Description automatically generated" />

6.  Select the **Model version** as **Auto-update to default,** in the
    **Deployment name field**, enter **gpt-35-turbo**, and click on the
    **Create** button.

> <img src="./media/image17.png" style="width:6in;height:5.1in" />

7.  You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded (You can also view the notification
    by clicking on the bell icon beside **Azure AI \| Azure AI
    Studio)**.

<img src="./media/image18.png" style="width:5.71667in;height:2.2in" />

8.  In the **Deployments** page, click on +**Create new deployment**.

> <img src="./media/image19.png"
> style="width:6.49167in;height:5.31667in" />

9.  In the **Deploy model dialog** box, under **Select a model** field,
    carefully select **gpt-4**, under **Model version** field, select
    **1106-Preview**, under the **Deployment name** field, enter
    **gpt-4**. Then, click on **Advanced options \>** as shown in the
    below image.

> <img src="./media/image20.png" style="width:6.01974in;height:5.02756in"
> alt="A screenshot of a computer Description automatically generated" />

10. Navigate to **Tokens Per Minute Rate Limit (thousands)** and move
    the slider to the extreme right to increase the quota limit to its
    maximum extent for your deployment. Then, click on the **Create**
    button.

> <img src="./media/image21.png" style="width:6.17112in;height:5.47061in"
> alt="A screenshot of a computer Description automatically generated" />

11. You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded (You can also view the notification
    by clicking on the bell icon beside **Azure AI \| Azure AI
    Studio)**.

<img src="./media/image22.png"
style="width:4.91667in;height:2.03333in" />

## **Task 2: Create an Azure SQL Database**

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:
    <https://portal.azure.com/#create/Microsoft.AzureSQL> then press the
    **Enter** button.

<img src="./media/image23.png"
style="width:6.0375in;height:2.86111in" />

2.  Navigate to **SQL databases** section, ensure that **Single
    database** is selected under **Resource type**, then click on the
    **Create** button.

<img src="./media/image24.png" style="width:6.5in;height:2.50005in" />

3.  On the **Create SQL Database** page provide the following details:

<!-- -->

1.  Subscription – Select your Azure OpenAI subscription

2.  Resource group – Select your Resource group(that you have created in
    **Lab 1**)

3.  Database name - **aoaisql**

4.  Server - **Create new** – provide the below Server details

    1.  Server name – Click on **Create new**, then enter **aoaisqlxx**
        \[Substitute **xx** with random number\]

    2.  Location – **East US**

    3.  Authentication – **Use both SQL and Microsoft Entra
        authentication**

    4.  Set Azure AD Admin – Click on **Set admin** and choose the
        Tenant admin **Select your Azure OpenAI subscription**

    5.  Server admin login – **aoaiuser**

    6.  Password – **Password321!**

    7.  Confirm password - **Password321!**

    8.  Click on **OK**

> <img src="./media/image25.png" style="width:6.5in;height:6.45833in" />

***Note**: Save the **server admin login** and **password** on the
notepad to use the information in the upcoming task.*

<img src="./media/image26.png"
style="width:6.49167in;height:7.05833in" />

<img src="./media/image27.png"
style="width:6.49167in;height:4.48333in" />

<img src="./media/image28.png" style="width:6.5in;height:6.91667in" />

5.  Want to use SQL elastic pool? – **No**

6.  Compute + storage – Click on **Configure database** – Click on
    **Service tier** dropdown and Choose **Basic**, then set the Data
    max size (GB) – **2**, then click on the **Apply** button.

7.  Backup storage redundancy - **Locally-redundant backup storage**

8.  Click on **Next: Networking\>**

<img src="./media/image29.png" style="width:6.5in;height:6.96667in" />

4.  On the Networking tab, provide the below details

    1.  Connectivity method – **Public endpoint**

    2.  Firewall rules

        1.  Allow Azure services and resources to access this server –
            **Yes**

        2.  Add current client IP address - **Yes**

    3.  Click on **Security**

<img src="./media/image30.png" style="width:6.5in;height:6.51667in" />

5.  On the **Security** tab, in **Enable Microsoft Defender for SQL**
    select the check box of **Start free trail** and select **Next:
    Additional settings**

<img src="./media/image31.png"
style="width:6.49167in;height:6.04167in" />

6.  On the **Additional settings** tab, under the **Data source** select
    the **Sample** as **Use existing data** and select **Next:
    Review+create.**

<img src="./media/image32.png" style="width:6.5in;height:6.33333in" />

7.  On the **Review + create** tab, click on the **Create** button.

<img src="./media/image33.png" style="width:6.5in;height:7.06667in" />

8.  The Deployment would be completed in 3-5 minutes.

<img src="./media/image34.png" style="width:6.5in;height:3.25486in" />

9.  After the deployment is completed, click on the **Go to resource**
    button.

<img src="./media/image35.png"
style="width:7.20076in;height:3.00417in" />

10. In **aoaisql (aoaisql29/aoaisql)** page, copy **SQL database** and
    **Server name** and paste them on a notepad (as shown in the below
    image), and then **Save** the notepad to use the information in the
    upcoming lab.

<img src="./media/image36.png"
style="width:7.39524in;height:3.5125in" />

<img src="./media/image37.png" style="width:5.22545in;height:5.39213in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 3: Configure and use the demo application for SQL query translation and advanced data analysis**

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:
     <https://app-web-ulajovkr7vyd4.azurewebsites.net/> then press the
    **Enter** button.

<img src="./media/image38.png" style="width:6.5in;height:3.26597in" />

2.  On the **web app** page, in the left side navigation menu, click on
    **Settings** button.

<img src="./media/image39.png"
style="width:5.50417in;height:6.89485in" />

3.  Under **Azure OpenAI Settings**, enter the below details and then
    click on the **Submit** button.

| ChatGPT deployment name | **gpt-35-turbo** |
|----|----|
| GPT-4 deployment name (if not specified, default to ChatGPT's) | **gpt-4** |
| Azure OpenAI Endpoint: | Enter Azure OpenAI Service Endpoint (*Endpoint information that you have saved on your notepad in **Lab \#1)*** |
| Azure OpenAI Key | Enter Azure OpenAI Key (*Key information that you have saved on your notepad in **Lab \#1)*** |
| SQL Server | **aoaisqlXX.database.windows.net** (SQL Server *information that you have saved on your notepad in **Task 1** of this lab)* |
| Database | **aoaisql** (Database *information that you have saved on your notepad in **Task 1** of this lab)* |
| User | **Aoaiuser** |
| Password | **Password321!** |

<img src="./media/image40.png" style="width:5.75in;height:8.125in" />

<img src="./media/image41.png" style="width:5.575in;height:8.025in" />

4.  There are two applications

    - **SQL Query Writing Assistant**: A simple application that
      translate business question into SQL query language, then execute
      and display result.

    - **Data Analysis Assistant**: A more sophisticated application to
      perform advanced data analytics such as statistical analysis and
      forecasting. Here, we demonstrate the use of [Chain of
      Thought](https://arxiv.org/abs/2201.11903) and [React](https://arxiv.org/abs/2210.03629) techniques
      to perform multi-step processing where the next step in the chain
      also depends on the observation/result from the previous step.

5.  Use SQL Query Writing Assistant in the web app page - Under **Choose
    the app**, select **SQL Query Writing Assistant** radio button,
    select **GPT Model** as **ChatGPT** then select **Show code** box.
    Under **Ask me a question** text box, enter the following question
    and click on the **Submit** button.

> **<span class="mark">Show me revenue by product in ascending
> order</span>**
>
> <img src="./media/image42.png" style="width:4.6in;height:7.76667in" />

<img src="./media/image43.png" style="width:6.5in;height:3.96458in"
alt="A screenshot of a computer Description automatically generated" />

6.  Use SQL Query Writing Assistant in the web app page - Under **Choose
    the app**, select **SQL Query Writing Assistant** radio button,
    select **GPT Model** as **GPT 4** then select **Show code** box.
    Under **Ask me a question** text box, enter the following question
    and click on the **Submit** button.

**<span class="mark">Pick top 20 customers generated most revenue in
2016 and for each customer show 3 products that they purchased
most</span>**

<img src="./media/image44.png"
style="width:5.56667in;height:8.03333in" />

<img src="./media/image45.png" style="width:6.5in;height:4.01944in"
alt="A screenshot of a computer Description automatically generated" />

7.  Now, use Data Analyst Assistant in the web app page - Under **Choose
    the app,** select **Data Analysis Assistant** radio button, select
    **GPT Model** as **GPT 4** then select **Show code** box and **Show
    prompt**. Under **Ask me a question** text box, enter the following
    question and click on the **Submit** button.

**<span class="mark">Pick top 20 customers generated most revenue in
2016 and for each customer show 3 products that they purchased
most</span>**

<img src="./media/image46.png" style="width:5.75in;height:8in" />

<img src="./media/image47.png" style="width:6.5in;height:4.10556in"
alt="A screenshot of a computer Description automatically generated" />

8.  Now, use Data Analyst Assistant in the web app page - Under **Choose
    the app,** select **Data Analysis Assistant** radio button, select
    **GPT Model** as **Chat** **GPT** then select **Show code** box.
    Under **Ask me a question** text box, enter the following question
    and click on the **Submit** button.

> **<span class="mark">Show me daily revenue trends 2016 per
> region</span>**

<img src="./media/image48.png" style="width:5.16667in;height:7.825in" />

<img src="./media/image49.png" style="width:7.2745in;height:4.55744in"
alt="A screenshot of a computer Description automatically generated" />

9.  For advanced questions such as forecasting in the web app page,
    under **Choose the app,** select **Data Analysis Assistant** radio
    button, select **GPT Model** as **ChatGPT** under **Ask me a
    question** text box, enter the following question and click on the
    **Submit** button.

**Note**: This time do not select **Show code** box.

> **<span class="mark">Predict monthly revenue for next 6 months
> starting from June 2018. Do not use Prophet.</span>**

<img src="./media/image50.png" style="width:3.94167in;height:8.025in" />

<img src="./media/image51.png" style="width:6.5in;height:3.67558in" />

<img src="./media/image52.png" style="width:6.5in;height:4.11749in"
alt="A screenshot of a computer Description automatically generated" />

## Task 4: Delete the deployed model

1.  In Azure OpenAI Studio, on the left pane, under the **Management**
    section, click on **Deployments**. Select **gpt-35-turbo**
    deployment name and click on **Delete deployment**.

<img src="./media/image53.png" style="width:6.5in;height:2.93125in" />

2.  In the **Confirm delete** dialog box, click on the **Delete**
    button. You will see the notification – **Successfully Deleted
    deployment**.

> <img src="./media/image54.png" style="width:3.075in;height:1.51667in" />
>
> <img src="./media/image55.png"
> style="width:5.12544in;height:2.31687in" />

3.  Select **gpt-4** deployment name and click on **Delete deployment**.
    If **Delete deployment** on the command bar is not visible, then
    click on the horizontal ellipses, navigate and click on **Delete
    deployment**.

<img src="./media/image56.png" style="width:6.5in;height:4.04167in" />

4.  In the **Confirm delete** dialog box, click on the **Delete**
    button. You will see the notification – **Successfully Deleted
    deployment**.

> <img src="./media/image57.png" style="width:2.575in;height:1.61667in" />
>
> <img src="./media/image58.png" style="width:4.97543in;height:1.75849in"
> alt="A screenshot of a computer Description automatically generated" />

## Task 5: Delete the SQL database and SQL server

1.  To delete the SQL database and server, navigate to **Azure portal
    Home** page, click on **Resource groups**.

> <img src="./media/image59.png" style="width:6.49167in;height:4.58333in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the resource group that you’ve created in this lab.

> <img src="./media/image60.png"
> style="width:6.38333in;height:2.56667in" />

3.  Select SQL database and SQL server that you’ve created.

> <img src="./media/image61.png"
> style="width:6.97008in;height:3.94583in" />

4.  In the Resource group page, navigate to command bar and click on
    **Delete**.

**Note**: In case, you did not see the **Delete** option on the command
bar, then click on the horizontal ellipsis, navigate and click on
**delete**.

<img src="./media/image62.png" style="width:6.49167in;height:2.925in" />

5.  In the **Delete Resources** pane that appears on the right side,
    enter **delete** and then click on **Delete** button.

> <img src="./media/image63.png"
> style="width:5.24167in;height:7.21667in" />

6.  On **Delete confirmation** dialog box, click on the **Delete**
    button.

> <img src="./media/image64.png" style="width:3.21695in;height:1.64181in"
> alt="A screenshot of a computer error Description automatically generated" />

7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 2 selected items**.

> <img src="./media/image65.png" style="width:4.79208in;height:2.04184in"
> alt="A screenshot of a computer Description automatically generated" />

**Summary**

In this lab, you’ve deployed gpt-35-turbo model in Azure AI Studio and
created

an Azure SQL Database with relevant configurations. Then, you’ve
configured the hosted demo application. You've used SQL Query Writing
Assistant of the demo app to translate business question into SQL query
language, then executed it and viewed the result. Then, you've used Data
Analysis Assistant of the hosted demo app to perform advanced data
analytics. You've deleted the gpt-3-turbo model, SQL database, and SQL
server to effectively and efficiently manage the Azure OpenAI resources.

**Important Note: Please do not delete the Resource Group. If deleted,
you’ll not be able to proceed with the next lab or create a new Resource
Group.**

**Please do not delete the Azure OpenAI Service (Azure-openai-testXX).
The same service will be used throughout all the labs.**

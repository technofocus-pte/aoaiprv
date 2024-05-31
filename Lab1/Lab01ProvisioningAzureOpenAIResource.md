# Lab 01: Provisioning Azure OpenAI resource

**Introduction**

Azure OpenAI Service brings the generative AI models developed by OpenAI
to the Azure platform, enabling you to develop powerful AI solutions
that benefit from the security, scalability, and integration of services
provided by the Azure cloud platform. The first step to use an Azure
Open AI model is to provision an Azure OpenAI resource. In this lab,
you'll learn how to get started with Azure OpenAI service by
provisioning Azure OpenAI resource in the Azure portal.

**Objectives**

-   To configure VM settings and register necessary Azure resource
    providers.

-   To create an Azure OpenAI resource and retrieve key and endpoint.

-   To install the required Python libraries.

## **Task 0: Sync Host environment time**

1.  In your VM, navigate and click in the **Search bar**, type
    **Settings** and then click on **Settings** under **Best match**.

> ![](https://github.com/technofocus-pte/aoaiprv/blob/main/images/Picture1.png)

2.  On Settings window, navigate and click on **Time & language**.

![](./media/image2.png){width="5.922367672790901in"
height="5.213708442694664in"}

3.  On **Time & language** page, navigate and click on **Date & time**.

![](./media/image3.png){width="6.5in" height="5.276388888888889in"}

4.  Scroll down and navigate to **Additional settings** section, then
    click on **Syn now** button. It will take 3-5 minutes to syn.

![](./media/image4.png){width="6.5in" height="5.048611111111111in"}

5.  Close the **Settings** window.

![](./media/image5.png){width="6.483409886264217in"
height="5.109148075240595in"}

## **Task 1: Register the required Resource providers**

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    [[https://portal.azure.com/]{.underline}](https://portal.azure.com/),
    then press the **Enter** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image6.png){width="6.491666666666666in"
> height="4.141666666666667in"}

2.  In the **Sign in** window, enter the **Username** and click on the
    **Next** button.

![](./media/image7.png){width="4.183711723534558in"
height="4.071298118985127in"}

3.  Then, enter the password and click on the **Sign in** button**.**

> ![A login screen with a log in box Description automatically
> generated](./media/image8.png){width="4.50872375328084in"
> height="3.600311679790026in"}

4.  In **Stay signed in?** window, click on the **Yes** button.

> ![Graphical user interface, application Description automatically
> generated](./media/image9.png){width="4.468055555555556in"
> height="2.9861745406824145in"}

5.  On **Welcome to Microsoft Azure** dialog box, click on **Maybe
    later** button.

> ![A screenshot of a computer Description automatically
> generated](./media/image10.png){width="6.5in" height="4.425in"}

6.  In the Azure portal search box, type **Subscriptions**, then click
    on **Subscriptions** under **Services**.

![A screenshot of a computer Description automatically
generated](./media/image11.png){width="6.5in"
height="3.6944444444444446in"}

7.  In the **Subscriptions** page, navigate and click on **Azure Pass --
    Sponsorship**.

![A screenshot of a computer Description automatically
generated](./media/image12.png){width="6.5in"
height="2.5791666666666666in"}

8.  In the **Azure Pass -- Sponsorship** page left-sided navigation
    menu, navigate to the **Settings** section, then click on the
    **Resource Providers**.

![A screenshot of a computer Description automatically
generated](./media/image13.png){width="6.5in"
height="4.621527777777778in"}

9.  In the **Azure Pass -- Sponsorship \| Resource providers** page,
    navigate to the search box and type **Microsoft.Storage**. Select
    the **Microsoft.Storage** under **Provider**, then click on the
    **Register** as shown in the below image.

![](./media/image14.png){width="6.5in" height="4.275in"}

10. You'll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

![A screenshot of a computer Description automatically
generated](./media/image15.png){width="2.934830489938758in"
height="1.65084208223972in"}

11. In the **Azure Pass -- Sponsorship \| Resource providers** page,
    navigate to the search box and type **Microsoft.Security**. Select
    the **Microsoft.Security** under **Provider**, then click on the
    **Register** as shown in the below image.

![](./media/image16.png){width="6.5in" height="4.283333333333333in"}

12. You'll see a notification stating - **Successfully registered
    resource provider** once the registration is successful. You can
    also view the notification by clicking on the bell icon in the Azure
    portal.

![](./media/image17.png){width="3.5753094925634294in"
height="1.2084383202099738in"}

13. Repeat the steps #10 and #11 to register the following Resource
    providers.

    -   **Microsoft.CognitiveServices**

    -   **Microsoft.Search**

    -   **Microsoft.Sql**

    -   **Microsoft.Web**

    -   **Microsoft.ManagedIdentity**

## **Task 2: Create Azure OpenAI resource**

1.  From the Azure portal home page, click on **Azure portal menu**
    represented by three horizontal bars on the left side of the
    Microsoft Azure command bar as shown in the below image.

> ![](./media/image18.png){width="6.5in" height="4.696527777777778in"}

2.  Navigate and click on **+ Create a resource**.

> ![](./media/image19.png){width="6.5in" height="4.781944444444444in"}

3.  On **Create a resource** page, in the **Search services and
    marketplace** search bar, type **Azure OpenAI**, then press the
    **Enter** button.

> ![](./media/image20.png){width="4.779166666666667in"
> height="4.190206692913386in"}

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you've already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

> ![](./media/image21.png){width="4.8625in"
> height="5.055999562554681in"}

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

+--------------------------------+-------------------------------------+
| > **Subscription**             | > Select the assigned subscription  |
+================================+=====================================+
| > **Resource group**           | Click on **Create new**\> enter     |
|                                | **AOAI-RGXX**(XX can be a unique    |
|                                | number, you can add more digits     |
|                                | after XX to make the name unique)   |
+--------------------------------+-------------------------------------+
| > **Region**                   | Select **East US**                  |
+--------------------------------+-------------------------------------+
| > **Name**                     | Azure-openai-testXX (XX can be a    |
|                                | unique number, you can add more     |
|                                | digits after XX to make the name    |
|                                | unique) (here, we entered           |
|                                | **Azure-open-test39**)              |
+--------------------------------+-------------------------------------+
| > **Pricing tier**             | > Select **Standard S0**            |
+--------------------------------+-------------------------------------+

> ![](./media/image22.png){width="6.5in" height="6.466666666666667in"}
>
> ![](./media/image23.png){width="6.5in" height="6.416666666666667in"}

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> ![](./media/image24.png){width="5.581007217847769in"
> height="5.895833333333333in"}

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> ![](./media/image25.png){width="5.8515726159230095in"
> height="4.8375in"}

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> ![](./media/image26.png){width="6.483333333333333in"
> height="7.516666666666667in"}

9.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

![A screenshot of a computer Description automatically
generated](./media/image27.png){width="7.1342060367454065in"
height="3.1326476377952757in"}

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

![](./media/image28.png){width="7.097435476815398in"
height="3.2708333333333335in"}

## **Task 3: Retrieve the key and endpoint of Azure OpenAI service**

1.  In your **Azure-open-testXX \| Model deployments** window, navigate
    to the **Resource Management** section, and click on **Keys and
    Endpoints**.

![](./media/image29.png){width="6.9785422134733155in"
height="5.554166666666666in"}

2.  In **Keys and Endpoints** page, copy **KEY1, KEY 2,** and
    **Endpoint** values and paste them in a notepad as shown in the
    below image, then **Save** the notepad to use the information in the
    upcoming lab.

![](./media/image30.png){width="6.5in" height="4.266666666666667in"}

![](./media/image31.png){width="6.144800962379702in"
height="3.885314960629921in"}

***Note:** You can use either KEY1 or KEY2. Always having two keys
allows you to securely rotate and regenerate keys without causing a
service disruption*.

## Task 4: Install Python libraries and pip updating 

1.  In your windows search bar, type **Command Prompt**. In the
    **Command Prompt App** dialog box, navigate and click on **Run as
    administrator**. If you see the dialog box - **Do you want to allow
    this app to make changes to your device?** then click on the **Yes**
    button.

![](./media/image32.png){width="5.256879921259842in"
height="4.8525043744531935in"}

2.  Move into the folder where the Python was installed and run the
    **pip** command. i.e., **C:\\Users\\Admin**

> copy
>
> **[python -m pip install \--upgrade pip]{.mark}**
>
> ![](./media/image33.png){width="6.5in" height="2.075in"}

3.  Run the following command to install Python libraries - openai,
    num2words, matplotlib, plotly, scipy, scikit-learn, pandas, tiktoken

Copy

[pip install openai num2words matplotlib plotly scipy scikit-learn
pandas tiktoken]{.mark}

![](./media/image34.png){width="6.5in" height="4.456944444444445in"}

![](./media/image35.png){width="6.5in" height="4.25in"}

4.  Run the below command to install the Transformers package:

> Copy
>
> [pip install transformers]{.mark}

![Text Description automatically
generated](./media/image36.png){width="6.5in"
height="3.286111111111111in"}

**Summary**

In this lab, you've set the VM time, registered the necessary Azure
resource providers, then provisioned Azure OpenAI resource. You've
learned how to retrieve keys and endpoint information that will be used
for deploying Azure OpenAI models in the upcoming labs. Finally, you've
successfully installed Python libraries.

**Please do not delete the Resource group and Azure OpenAI Service
(Azure-openai-testXX). The same Resource group and AOAI service will be
used throughout all the labs.**

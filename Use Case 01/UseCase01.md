**Use Case- Fashion Trend Analysis with GPT-4 Turbo and Vision on Azure
OpenAI**

**Introduction:**

GPT-4 Turbo with Vision on Azure OpenAI service is now in public
preview. GPT-4 Turbo with Vision is a large multimodal model (LMM)
developed by OpenAI that can analyze images and provide textual
responses to questions about them. It incorporates both natural language
processing and visual understanding. With enhanced mode, you can use the
Azure AI Vision features to generate additional insights from the images

**Objective:**

- To deploy Azure OpenAI resources and configure them.

- To deploy specific Azure OpenAI model like GPT-4 Vision.

- Set up your development environment with Python, Jupyter Notebook, and
  required libraries.

- This usecase related to fashion use cases. These might involve image
  analysis, text generation, or other AI tasks.

 

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

    1.  **Subscription**: Select the assigned subscription

    2.  **Resource group:** Click on **Create new**\> enter
        **AOAI-RGXX**(XX can be a unique number, you can add more digits
        after XX to make the name unique)

    3.  **Region**: For this lab, you will use a  **gpt-4-vision**
        model. This model is currently only available in [certain
        regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models).
        Please select a region from this list, In this lab **Sweden
        Central** is using for this resource.

    4.  **Name**: **aoai-gpt4-visionXX** (XX can be a unique number)

    5.  **Pricing tier**: Select **Standard S0**

> <img src="./media/image5.png" style="width:6.5in;height:5.50833in" />

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> <img src="./media/image6.png" style="width:5.58101in;height:5.89583in"
> alt="A screenshot of a computer Description automatically generated" />

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> <img src="./media/image7.png" style="width:5.1625in;height:6.08222in"
> alt="A screenshot of a computer Description automatically generated" />

8.  In the **Review + submit** tab, once the Validation is Passed, click
    on the **Create** button.

> <img src="./media/image8.png"
> style="width:6.49167in;height:5.43333in" />

9.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on **Go to resource** button.

> <img src="./media/image9.png" style="width:6.5in;height:4.575in" />

11. Click on **Keys and Endpoints** from the left navigation menu and
    then copy the endpoint value in a notepad to **AzureAI ENDPOINT**
    and key to a variable **AzureAIKey**.

> <img src="./media/image10.png"
> style="width:6.94583in;height:3.94102in" />

12. On the **aoai-gpt4-visionXX** window, click on **Overview** in the
    left-sided navigation menu, scroll down to **Get Started** tile and
    click on **Go to AzureOpenAI Studio** button as shown in the below
    image to open **Azure OpenAI Studio** in a new browser.

<img src="./media/image10.png"
style="width:7.04243in;height:3.99583in" />

## **Task 2: Deploying an Azure OpenAI model gpt-4-vision**

1.  On the **Azure OpenAI Studio** homepage, click on **Create new
    deployment** button.

> <img src="./media/image11.png"
> style="width:6.75417in;height:4.09238in" />

2.  In the **Deployments** page, click on +**Create new deployment**.

<img src="./media/image12.png" style="width:6.5in;height:5.76667in"
alt="A screenshot of a computer Description automatically generated" />

3.  In the **Deploy model dialog** box, under the **Model name** field,
    click on the V chevron button; navigate and select carefully
    **gpt-4**.

4.  Select the **Model version** as **vision-preview,** in the
    **Deployment type** as **Standard, Deployment name field**, enter
    +++**gpt-4-vision+++**, and click on the **Create** button.

<img src="./media/image13.png" style="width:5.15833in;height:6.925in" />

5.  You will see a notification – **Successfully Created deployment**
    when the deployment is succeeded.

<img src="./media/image14.png"
style="width:4.6375in;height:2.61724in" />

## Task 3: GPT-4 Turbo with Vision demo

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> <img src="./media/image15.png" style="width:5.24583in;height:5.24583in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open Folder**.

> <img src="./media/image16.png" style="width:3.77917in;height:4.6555in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Navigate and select **GPT4V-Fashion** folder from **C:\LabFiles**
    and click on the **Select Folder** button.

<img src="./media/image17.png"
style="width:6.49167in;height:4.71667in" />

4.  If you see a dialog box - **Do you trust the authors of the files in
    this folder?**, then click on **Yes, I trust the author**.

<img src="./media/image18.png" style="width:3.95417in;height:3.27083in"
alt="A screenshot of a computer Description automatically generated with medium confidence" />

5.  In Visual Studio Code dropdown the **Gpt 4V-FASHION**, click on
    **azure.env** file.

<img src="./media/image19.png"
style="width:6.08333in;height:3.85833in" />

6.  Update the parameters ,replace **Azure OpenAI Endpoint, Azure OpenAI
    Key(**The values that you have saved in your notepad in the **Task
    1)** and Save the file.

<img src="./media/image20.png" style="width:6.5in;height:2.30833in" />

7.  In Visual Studio Code dropdown the **GPT 4V-FASHION** and select
    **GPT-4 with Vision demo with Azure Open AI - Fashion
    usecase.ipynb** notebook.

> <img src="./media/image21.png"
> style="width:5.01667in;height:3.36667in" />

8.  In the main page of Visual Studio Code editor, scroll down to
    **install requirements** heading and run the 1<sup>st</sup> cell. If
    prompted to select the environment, then select **Python
    Environments** as shown in the image.

> <img src="./media/image22.png" style="width:6.5in;height:4.66667in" />
>
> <img src="./media/image23.png" style="width:6.49167in;height:3.225in" />

9.  If prompted to select the path, then select the **Python version
    3.11.5(or later version)** path as shown in the image.

> <img src="./media/image24.png"
> style="width:6.49167in;height:3.43333in" />

10. If you see an windows security alert dialog box - then click on
    **Allow access**.

> <img src="./media/image25.png"
> style="width:5.35833in;height:3.95833in" />
>
> <img src="./media/image26.png"
> style="width:5.84399in;height:4.56718in" />
>
> <img src="./media/image27.png" style="width:5.125in;height:3.75in" />
>
> <img src="./media/image28.png" style="width:6.49167in;height:4.05in" />

11. To restart Jupyter kernel, click on **Restart** button.

> <img src="./media/image29.png"
> style="width:6.7375in;height:4.21978in" />

12. To import the libraries, select **4<sup>th</sup>** cell. Then,
    execute the cell by clicking on the **start icon**.

> <img src="./media/image30.png"
> style="width:6.49167in;height:4.19167in" />

13. Select **5<sup>th</sup>** cell. Then, execute the cell by clicking
    on the **start icon**.

> <img src="./media/image31.png"
> style="width:6.49167in;height:4.89167in" />

14. To check the OpenAI, system versions, select **6<sup>th
    </sup>**,7<sup>th</sup> , 8<sup>th</sup> and 9<sup>th</sup> cells.
    Then, execute the cell by clicking on the **start icon**.

> <img src="./media/image32.png"
> style="width:6.49167in;height:4.76667in" />

15. To load the configuration values, select and execute the
    **10<sup>th</sup>** ,11<sup>th</sup> and 12<sup>th</sup> cells by
    clicking on the **Play** button.

> <img src="./media/image33.png" style="width:6.5in;height:4.53403in"
> alt="A screenshot of a computer program Description automatically generated" />

16. Define a helper function to create embeddings, select and execute
    the 13<sup>th</sup> .14<sup>th</sup> cells by clicking on the
    **Play** button.

> <img src="./media/image34.png"
> style="width:6.16281in;height:3.57917in" />
>
> <img src="./media/image35.png"
> style="width:6.1625in;height:4.55867in" />

17. To run the example, select and execute the 15<sup>th</sup> ,
    16<sup>th</sup> cells by clicking on the **Play** button.

> <img src="./media/image36.png"
> style="width:4.82083in;height:3.86781in" />
>
> <img src="./media/image37.png"
> style="width:5.81667in;height:4.28596in" />

18. To run the example, select and execute the **17<sup>th</sup>
    ,18<sup>th</sup>** cells by clicking on the **Play** button.

> <img src="./media/image38.png" style="width:5.58081in;height:4.25in" />
>
> <img src="./media/image39.png"
> style="width:5.64625in;height:4.51338in" />

19. To run the example, select and execute the **19<sup>th</sup>
    ,20<sup>th</sup>** cells by clicking on the **Play** button.

> <img src="./media/image40.png" style="width:6.2in;height:4.54454in" />
>
> <img src="./media/image41.png" style="width:5.81883in;height:4.28923in"
> alt="A screenshot of a computer Description automatically generated" />

20. To run the example, select and execute the **21<sup>st</sup>
    ,22<sup>nd</sup>** cells by clicking on the **Play** button.

> <img src="./media/image42.png"
> style="width:6.49167in;height:4.81667in" />
>
> <img src="./media/image43.png"
> style="width:5.01667in;height:3.69649in" />

21. To run the example, select and execute the **23<sup>st</sup>
    ,24<sup>nd</sup>** cells by clicking on the **Play** button.

> <img src="./media/image44.png" style="width:6.5in;height:4.825in" />

<img src="./media/image45.png"
style="width:7.0375in;height:5.34128in" />

22. To run the example, select and execute the **25<sup>th</sup>
    ,26<sup>th</sup>** cells by clicking on the **Play** button.

> <img src="./media/image46.png"
> style="width:5.53333in;height:4.17838in" />
>
> <img src="./media/image47.png"
> style="width:5.96957in;height:4.39873in" />

23. To run the example, select and execute the **27<sup>th</sup>
    ,28<sup>th</sup>** cells by clicking on the **Play** button.

> <img src="./media/image48.png"
> style="width:5.18333in;height:3.72801in" />
>
> <img src="./media/image49.png" style="width:6.5in;height:4.79097in"
> alt="A screenshot of a computer Description automatically generated" />

24. To run the example, select and execute the **27<sup>th</sup>
    ,28<sup>th</sup>** cells by clicking on the **Play** button.

> <img src="./media/image50.png"
> style="width:5.70826in;height:4.29583in" />
>
> <img src="./media/image51.png" style="width:6.09359in;height:4.20497in"
> alt="A screenshot of a computer Description automatically generated" />

25. To generate WebApp, select and execute the **29<sup>th</sup>** cells
    by clicking on the **Play** button.

> <img src="./media/image52.png" style="width:6.74486in;height:5.05in" />

26. To generate WebApp, select and execute the **30<sup>th</sup>** cell
    by clicking on the **Play** button.

> <img src="./media/image53.png"
> style="width:6.24167in;height:4.64924in" />

27. After the application has been successfully deployed, you see a URL
    displayed in the terminal. Copy the **URL**

<img src="./media/image54.png" style="width:6.49167in;height:4.375in" />

28. Open your browser, navigate to the address bar, paste the Publick
    URL link. <img src="./media/image55.png"
    style="width:6.49167in;height:3.64167in" />

29. Open your browser, navigate to the address bar, paste the local URL
    link. Select any item

<img src="./media/image56.png" style="width:6.5in;height:4.125in" />

30. Click on the **Submit** button.

> <img src="./media/image57.png"
> style="width:6.49167in;height:3.93333in" />

<img src="./media/image58.png"
style="width:6.9875in;height:4.45229in" />

## Task 4: Delete the resources

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

> <img src="./media/image59.png" style="width:6.5in;height:4.58472in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the AOAI-RGXXX resource group.

> <img src="./media/image60.png" style="width:4.675in;height:3.55833in"
> alt="A screenshot of a computer Description automatically generated" />

3.  In the **Resource group** home page, select the **delete resource
    group**

<img src="./media/image61.png" style="width:6.49167in;height:3.24167in"
alt="A screenshot of a computer Description automatically generated" />

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “resource group name” to confirm deletion**
    field, then click on the **Delete** button.

<img src="./media/image62.png" style="width:4.44993in;height:4.4625in"
alt="A screenshot of a computer Description automatically generated" />

5.  On **Delete confirmation** dialog box, click on **Delete** button.

> <img src="./media/image63.png" style="width:3.475in;height:1.85833in"
> alt="A screenshot of a computer error Description automatically generated" />

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

<img src="./media/image64.png" style="width:3.4253in;height:2.81691in"
alt="A screenshot of a computer Description automatically generated" />

**Summary**

In this hands-on lab, participants delve into advanced AI capabilities
using Azure OpenAI. Starting with the setup of essential Azure
resources, they deploy AI models like GPT-4-vision. The lab specifically
explores how GPT-4, equipped with vision capabilities, can revolutionize
fashion-related tasks—think image recognition, personalized style
recommendations, and trend analysis.

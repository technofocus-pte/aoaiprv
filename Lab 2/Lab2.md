# Lab 2 - Generating images using DALL-E and DALL-E3 

**Introduction**

The DALL-E models, currently in preview, generate images from text
prompts that the user provides. This generative AI model presents myriad
opportunities for developers, artists, designers, educators, and others.
It can bridge the gap between what you can imagine and what you can
create. This generative model allows for cross-domain, general
understanding, and zero-shot translation between text prompt and images,
often with a remarkable degree of realism. The main capability of the
Azure OpenAI DALL·E is to take text prompt and generate images.

**Objective**

- To generate image using text in DALL-E playground.

**Important Note:** If you’re facing any **API issues**, please consider
changing the available region
"https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models"

# Exercise 1: Explore image-generation in the DALL-E playground

## Task 1: Create Azure OpenAI resource

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

4.  In the **Marketplace** page, navigate to the **Azure OpenAI**
    section, click on the Create button dropdown, then select **Azure
    OpenAI** as shown in the image. (In case, you’ve already clicked on
    the **Azure** **OpenAI** tile, then click on the **Create** button
    on the **Azure OpenAI page**).

> <img src="./media/image4.png" style="width:4.8625in;height:5.056in" />

5.  In the **Create Azure OpenAI** window, under the **Basics** tab,
    enter the following details and click on the **Next** button.

<table>
<colgroup>
<col style="width: 45%" />
<col style="width: 54%" />
</colgroup>
<thead>
<tr class="header">
<th><blockquote>
<p><strong>Subscription</strong></p>
</blockquote></th>
<th><blockquote>
<p>Select the assigned subscription</p>
</blockquote></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><blockquote>
<p><strong>Resource group</strong></p>
</blockquote></td>
<td>Click on <strong>Create new</strong>&gt; enter
<strong>AOAI-RGXX</strong>(XX can be a unique number, you can add more
digits after XX to make the name unique)</td>
</tr>
<tr class="even">
<td><blockquote>
<p><strong>Region</strong></p>
</blockquote></td>
<td>For this lab, you will use a <strong>DALL-E3</strong> model. This
model is currently only available in <a
href="https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models">certain
regions</a>. Please select a region from this list, In this lab
<strong>Sweden Central</strong> is using for this resource.</td>
</tr>
<tr class="odd">
<td><blockquote>
<p><strong>Name</strong></p>
</blockquote></td>
<td><strong>Azure-openai-testXX</strong> (XX can be a unique number, you
can add more digits after XX to make the name unique) (here, we entered
<strong>Azure-open-test39</strong>)</td>
</tr>
<tr class="even">
<td><blockquote>
<p><strong>Pricing tier</strong></p>
</blockquote></td>
<td><blockquote>
<p>Select <strong>Standard S0</strong></p>
</blockquote></td>
</tr>
</tbody>
</table>

> <img src="./media/image5.png" style="width:6.5in;height:6.46667in"
> alt="A screenshot of a computer Description automatically generated" />
>
> <img src="./media/image6.png" style="width:6.5in;height:6.25833in" />

6.  In the **Network** tab, leave all the radio buttons in the default
    state, and click on the **Next** button.

> <img src="./media/image7.png" style="width:5.58101in;height:5.89583in"
> alt="A screenshot of a computer Description automatically generated" />

7.  In the **Tags** tab, leave all the fields in the default state, and
    click on the **Next** button.

> <img src="./media/image8.png" style="width:5.85157in;height:4.8375in"
> alt="A screenshot of a computer Description automatically generated" />

8.  In the **Review+submit** tab, once the Validation is Passed, click
    on the **Create** button.

> <img src="./media/image9.png" style="width:4.92132in;height:5.3125in" />

9.  Wait for the deployment to complete. The deployment will take around
    2-3 minutes.

<img src="./media/image10.png" style="width:7.13421in;height:3.13265in"
alt="A screenshot of a computer Description automatically generated" />

10. On **Microsoft.CognitiveServicesOpenAI** window, after the
    deployment is completed, click on the **Go to resource** button.

<img src="./media/image11.png"
style="width:7.09744in;height:3.27083in" />

## Task 2: Retrieve the key and endpoint of Azure OpenAI service

1.  In your **Azure-open-testXX \| Model deployments** window, navigate
    to the **Resource Management** section, and click on **Keys and
    Endpoints**.

<img src="./media/image12.png"
style="width:6.97854in;height:5.55417in" />

2.  In **Keys and Endpoints** page, copy **KEY1, KEY 2,** and
    **Endpoint** values and paste them in a notepad as shown in the
    below image, then **Save** the notepad to use the information in the
    upcoming lab.

<img src="./media/image13.png" style="width:6.5in;height:4.26667in" />

<img src="./media/image14.png"
style="width:6.1448in;height:3.88531in" />

***Note:** You can use either KEY1 or KEY2. Always having two keys
allows you to securely rotate and regenerate keys without causing a
service disruption*.

## Task 3: [Cognitive Services OpenAI Contributor](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/role-based-access-control#cognitive-services-contributor) for the Azure OpenAI resource

1.  From the left menu, click on the **Access control(IAM).**

<img src="./media/image15.png" style="width:6.39167in;height:4.825in" />

2.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image16.png" style="width:6.5in;height:5.46667in" />

3.  Type the [**Cognitive Services OpenAI
    Contributor**](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/role-based-access-control#cognitive-services-contributor)
    in the search box and select it. Click **Next**

<img src="./media/image17.png"
style="width:5.6375in;height:5.68087in" />

4.  In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image18.png"
style="width:5.71721in;height:5.8125in" />

5.  On the Select members tab , search your Azure OpenAI subscription
    and click **Select.**

<img src="./media/image19.png" style="width:5.325in;height:7.1in" />

6.  In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image20.png"
style="width:6.49167in;height:5.06667in" />

<img src="./media/image21.png" style="width:6.5in;height:6.95in" />

7.  You will see a notification – added as [**Cognitive Services OpenAI
    Contributor**](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/role-based-access-control#cognitive-services-contributor)
    for Azure Pass-Sponsorship.

##  Task 4: Create image-generation in the DALL-E playground

1.  In **Azure-openai-testXX** page, click on **Overview** in the
    left-sided navigation menu, scroll down and click on **Go to Azure
    OpenAI Studio** button as shown in the below image.

> <img src="./media/image22.png" style="width:6.5in;height:3.80833in" />

2.  Wait for the Azure OpenAI studio to launch.

<img src="./media/image23.png" style="width:6.38037in;height:3.59169in"
alt="A screenshot of a computer Description automatically generated" />

3.  In the **Azure AI Studio** landing page, navigate and click on
    **DALL-E playground** to use the image generation APIs.

<img src="./media/image24.png"
style="width:7.06016in;height:3.69886in" />

4.  Start exploring Azure OpenAI capabilities with a no-code approach
    through the **DALL-E playground** .

<img src="./media/image25.png" style="width:6.5in;height:3.24653in" />

# Exercise 2: Generate images using DALl-E-3 with Azure OpenAI Service

## Task 1: Generate images using DALL-E-3

1.  In Azure OpenAI Studio Home page, under **Playground**, select the
    **DALL-E**.

<img src="./media/image26.png"
style="width:5.98333in;height:5.16667in" />

2.  Make sure to choose the **dall-e-3** model from the Deployment
    dropdown.

<img src="./media/image27.png" style="width:6.5in;height:3.71667in" />

3.  In **DALL-E playground** window, under **Prompt**, enter your image
    prompt in the text box - **An elephant on a skateboard** as shown in
    the below image and click on the **Generate** button.

<img src="./media/image28.png"
style="width:7.19139in;height:2.19583in" />

<img src="./media/image29.png" style="width:6.5in;height:5.94792in" />

4.  Select **View code** near the top of the page, you can use this code
    to write an application that completes the same task.

<img src="./media/image30.png"
style="width:6.49167in;height:5.39167in" />

<img src="./media/image31.png" style="width:5.22545in;height:7.02561in"
alt="A screenshot of a computer program Description automatically generated" />

5.  In the **Deployments** window, copy **Deployment name** and paste
    them in a notepad (as shown in the image), and then **Save** the
    notepad to use the information in the upcoming task.

<img src="./media/image32.png" style="width:6.49167in;height:4.3in" />

## Task 2: Install Microsoft .NET SDK

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    <https://download.visualstudio.microsoft.com/download/pr/9f9ad302-a698-4fab-9765-e313f7e14151/8ad751b6cfc11276b4e2adef4e319db7/dotnet-sdk-8.0.200-win-x64.exe>
    , then press the **Enter** button

2.  **Dotnet-sdk-8.0.200-win-x64.exe** file will be downloaded. Click on
    the downloaded file to install the .NET SDK software

> <img src="./media/image33.png" style="width:3.15833in;height:0.85833in"
> alt="A black text on a white background Description automatically generated" />

3.  Click on **Install** button.

<img src="./media/image34.png" style="width:5.96667in;height:4.46667in"
alt="A screenshot of a computer Description automatically generated" />

4.  On User Account control tab, click on the Yes button

<img src="./media/image35.png" style="width:4.18333in;height:3.575in"
alt="A screenshot of a computer error Description automatically generated" />

5.  After installation was successful , click on close button

<img src="./media/image36.png" style="width:5.95833in;height:4.44167in"
alt="A screenshot of a computer Description automatically generated" />

## Task 3: Azure DALL·E- 3 image generation example

1.  Click on your Windows search box, type **Visual Studio Code**, then
    click on **Visual Studio Code** under Best match.

> <img src="./media/image37.png" style="width:6.5in;height:5.34931in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Visual Studio Code** editor, click on **File**, then
    navigate and click on **Open File**.

<img src="./media/image38.png" style="width:2.95417in;height:3.97784in"
alt="A screenshot of a computer Description automatically generated" />

3.  Navigate and select **DALL-E-3** notebook from **C:\LabFiles** and
    click on the **Open** button.

<img src="./media/image39.png" style="width:5.65833in;height:4.31667in"
alt="A screenshot of a computer Description automatically generated" />

4.  In case, **Do you want to allow untrusted files in this window?**
    dialog box appears, then click on the **Open** button.

<img src="./media/image40.png" style="width:5.39583in;height:3.55in"
alt="A screenshot of a computer screen Description automatically generated" />

5.  Install the Azure Open AI SDK using the command. Click on **Execute
    cell start icon** as shown in the image.

<img src="./media/image41.png" style="width:7.1179in;height:3.69583in"
alt="A screenshot of a computer Description automatically generated" />

6.  If prompted to select the environment, then select **.NET
    Interactive** as shown in the image.

<img src="./media/image42.png" style="width:6.73309in;height:3.1375in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image43.png" style="width:7.18685in;height:2.96381in"
alt="A screenshot of a computer Description automatically generated" />

7.  Execute the **2<sup>nd</sup> cell** by clicking on the **start
    icon**.

<img src="./media/image44.png" style="width:7.15431in;height:4.14583in"
alt="A screenshot of a computer Description automatically generated" />

8.  Run this cell, it will prompt you for the apiKey, endPoint, and
    imageGeneration deployment name.

9.  Once the resource is created, then add azure openai endpoint. Beside
    the comment **\#Add your key ,#Add your endpoint here** (you’ve
    saved in a notepad in Lab 1\> Task \#3.) and **\#Add your** **image
    deployment name** replace the URL with endpoint URL that you’ve
    saved in a notepad in Exercise 2\>Task \#2. Then, execute the cell
    by clicking on the **start icon**.

<img src="./media/image45.png" style="width:7.22831in;height:2.61667in"
alt="A screenshot of a computer Description automatically generated" />

10. In case, a notification stating **enter to API key** appears, then
    click on the **enter**.

<img src="./media/image46.png" style="width:7.24713in;height:2.425in"
alt="A screenshot of a computer Description automatically generated" />

11. In case, a notification stating **enter to Endpoint** appears, then
    click on the **enter**.

<img src="./media/image47.png" style="width:7.07738in;height:2.41667in"
alt="A screenshot of a computer Description automatically generated" />

12. In case, a notification stating **image deployment** appears, then
    click on the **enter**.

<img src="./media/image48.png" style="width:6.99781in;height:4.1in"
alt="A screenshot of a computer program Description automatically generated" />

13. Import namesapaces and create an instance of OpenAiClient using the
    azureOpenAIEndpoint and the azureOpenAIKey. Then, execute the cell
    by clicking on the **start icon**.

<img src="./media/image49.png" style="width:7.29016in;height:2.92917in"
alt="A screenshot of a computer program Description automatically generated" />

14. Import namesapaces and create an instance of OpenAiClient using the
    azureOpenAIEndpoint and the azureOpenAIKey. Replace the existing
    code with the below code.** **Then, execute the cell by clicking on
    the **start icon**.

> **OpenAIClient client = new (new Uri(azureOpenAIEndpoint), new
> AzureKeyCredential(azureOpenAIKey));**
>
> <img src="./media/image50.png" style="width:6.5in;height:3.94167in"
> alt="A screenshot of a computer program Description automatically generated" />

15. Import SkiaSharp to display images. Then, execute the cell by
    clicking on the **start icon**.

<img src="./media/image51.png" style="width:6.88559in;height:3.64583in"
alt="A screenshot of a computer Description automatically generated" />

16. The method returns the SKSurface object, which now contains the
    drawn image. Then, execute the cell by clicking on the **start
    icon**.

<img src="./media/image52.png" style="width:7.01116in;height:4.62917in"
alt="A screenshot of a computer program Description automatically generated" />

17. With setup and authentication complete, you can now generate images
    on the Azure OpenAI service and retrieve them from the returned
    URLs.

18. The first step in this process is to actually generate the images.
    Then, execute the cell by clicking on the **start icon**.

<img src="./media/image53.png" style="width:7.06296in;height:3.42083in"
alt="A screenshot of a computer Description automatically generated" />

19. Create the image using the response and SkiaSharp and display it.
    Then, execute the cell by clicking on the **start icon**.

<img src="./media/image54.png" style="width:7.07901in;height:4.77083in"
alt="A screenshot of a computer screen Description automatically generated" />

## Task 4: Clean up resources

To avoid incurring unnecessary Azure costs, you should delete the
resources you created in this quick start if they're no longer needed.
To manage resources, you can use the [Azure
portal](https://portal.azure.com/?azure-portal=true).

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

> <img src="./media/image55.png" style="width:6.5in;height:4.58472in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the resource group that you’ve created.

> <img src="./media/image56.png" style="width:6.49167in;height:4.15833in"
> alt="A screenshot of a computer Description automatically generated" />

3.  In the **Resource group** home page, select the **delete resource
    group** .

<img src="./media/image57.png" style="width:6.5in;height:3.61667in" />

4.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “resource group name” to confirm deletion**
    field, then click on the **Delete** button.

<img src="./media/image58.png"
style="width:5.95833in;height:5.88333in" />

5.  On **Delete confirmation** dialog box, click on **Delete** button.

> <img src="./media/image59.png" style="width:3.475in;height:1.85833in" />

6.  Click on the bell icon, you’ll see the notification –**Deleted
    resource group AOAI-RG89.**

<img src="./media/image60.png"
style="width:3.4253in;height:2.81691in" />

**Summary**

In this lab, you’ve used DALL-E playground and generated images using
text. Then, you’ve used Azure Dalle-E image generation code in Visual
Studio for generating images with the Azure OpenAI service and viewed
the downloaded image in Visual Studio as well as browser.

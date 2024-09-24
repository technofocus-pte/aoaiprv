# Use Case-Building a chat app (using .NET) using Azure OpenAI Service and RAG

This sample demonstrates a few approaches for creating ChatGPT-like
experiences over your own data using the Retrieval Augmented Generation
pattern. It uses Azure OpenAI Service to access the ChatGPT model
(gpt-4o-mini), and Azure AI Search for data indexing and retrieval.

The repo includes sample data so it's ready to try end-to-end. In this
sample application, we use a fictitious company called Contoso
Electronics, and the experience allows its employees to ask questions
about the benefits, internal policies, as well as job descriptions and
roles.

<img src="./media/image1.png" style="width:6.5in;height:3.07153in"
alt="A diagram of a computer process Description automatically generated" />

- To install Azure CLI and Node.js on your local machine.

- To assign an owner role to the user.

- To install the Dev Containers extension and set up the development
  environment.

- To deploy a chat application to Azure and use it to get answers from
  PDF files.

- To delete the deployed resources and models.

## Task 1: Install Azure Cli and set the policy scope to Local machine

1.  In your windows search bar, type **PowerShell**. In the
    **PowerShell** dialog box, navigate and click on **Run as
    administrator**. If you see the dialog box - **Do you want to allow
    this app to make changes to your device?** then click on the **Yes**
    button.

> <img src="./media/image2.png" style="width:5.15417in;height:6.14535in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Run the following command to install Azure Cli on the PowerShell

<span class="mark">PowerShell copy</span>

> **winget search Microsoft.PowerShell**

<img src="./media/image3.png" style="width:4.95833in;height:1.8in" />

3.  Run the following command

> <span class="mark">PowerShell copy</span>
>
> winget install --id Microsoft.Powershell --source winget

<img src="./media/image4.png"
style="width:7.23022in;height:2.92917in" />

4.  Verify the Installation, run the following command

<span class="mark">PowerShell copy</span>

> pwsh

<img src="./media/image5.png" style="width:6.5in;height:3.2in" />

## Task 2: Install .NET

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    https://dotnet.microsoft.com/en-us/download/dotnet/8.0 then press
    the **Enter** button.

<img src="./media/image6.png" style="width:6.5in;height:4.74375in"
alt="A screenshot of a computer Description automatically generated" />

2.  Select and click on **Windows -x64**

<img src="./media/image7.png"
style="width:5.87587in;height:4.35417in" />

3.  In Downloads Click on the **Open** button.

<img src="./media/image8.png"
style="width:3.91667in;height:1.64167in" />

4.  **Dotnet-sdk** file will be downloaded. Click on the downloaded file
    to set up **Dotnet-sdk**

<img src="./media/image9.png"
style="width:5.54787in;height:1.74583in" />

5.  In the **Microsoft .NET SDK 8.0.401** window, click on the
    **Install** button

<img src="./media/image10.png" style="width:6.5in;height:4.84167in" />

6.  Click on the **Yes** button

<img src="./media/image11.png"
style="width:4.64167in;height:3.40833in" />

7.  In the **Microsoft .NET SDK 8.0.401** window, click on the Close
    button

<img src="./media/image12.png" style="width:6.5in;height:4.81667in" />

## Task 3: Run the Docker

1.  In your Windows search box, type Docker , then click on **Docker
    Desktop**.

<img src="./media/image13.png"
style="width:6.49167in;height:5.81667in" />

2.  Run the Docker Desktop.

<img src="./media/image14.png" style="width:7.1577in;height:4.04991in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 4: Deploy Azure services needed for the application**

1.  Change the current directory to the **Labfiles** directory and
    navigate into the project cd .\\**Chat** folder by running the below
    commands.

> cd\\
>
> **+++cd Labfiles+++**
>
> **+++cd .\Chat+++**
>
> <img src="./media/image15.png" style="width:3.58364in;height:1.30845in"
> alt="A screenshot of a computer program Description automatically generated" />

2.  Run the below command to install azure cli

> **+++winget install microsoft.azd+++**
>
> <img src="./media/image16.png" style="width:6.5in;height:1.97431in"
> alt="A blue screen with white text Description automatically generated" />

3.  Run the below command to login the azure portal

> **+++azd auth login+++**

4.  Default browser opens to sign in .Sign in with your Azure
    subscription account.

> <img src="./media/image17.png" style="width:5.72083in;height:4.025in" />
>
> <img src="./media/image18.png" style="width:4.90833in;height:4.275in" />

5.  Close the browser

> <img src="./media/image19.png" style="width:6.5in;height:1.6375in"
> alt="A screenshot of a computer Description automatically generated" />
>
> <img src="./media/image20.png" style="width:4.14203in;height:1.79182in"
> alt="A screenshot of a computer program Description automatically generated" />

6.  Run azd up - This will provision Azure resources and deploy this
    sample to those resources, including building the search index based
    on the files found in the ./data folder.

> **+++azd up+++**

7.  When prompted, select a **subscription** to create the resources and
    select a location **East US2**, This location is used for most the
    resources including hosting. 

**Note:** For this use case, you will use a GPT-4, text-embedding-ada-2
models. This models is currently only available in [certain
regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models).
Please select a region from this list, In this lab **East US2** is using
for this resource

>  <img src="./media/image21.png" style="width:6.5in;height:3.64167in" />

8.  Wait until app is deployed. It may take 20-30 minutes for the
    deployment to complete.

<img src="./media/image22.png" style="width:6.5in;height:4.45764in" />

> <img src="./media/image23.png"
> style="width:6.49167in;height:4.54167in" />

9.  After the application has been successfully deployed, you see a URL
    displayed in the terminal. Copy the **URL**

> <img src="./media/image24.png" style="width:6.5in;height:5.625in" />

10. Open a browser go to <https://portal.azure.com> and sign in with
    your Azure subscription account.

11. On the Home page, click on **Resource Groups**

> <img src="./media/image25.png" style="width:6.5in;height:3.275in" />

12. Click on your resource group.

> <img src="./media/image26.png" style="width:6.5in;height:2.96667in" />

13. Make sure the below resource got deployed successfully

<img src="./media/image27.png" style="width:6.5in;height:3.61667in" />

<img src="./media/image28.png"
style="width:6.49167in;height:3.78333in" />

<img src="./media/image29.png"
style="width:7.25754in;height:4.14583in" />

<img src="./media/image30.png"
style="width:6.49167in;height:3.64167in" />

14. On the resource group and click on **Azure OpenAI** resource name.

> <img src="./media/image31.png"
> style="width:6.49167in;height:3.68333in" />

15. On the **Azure OpenAI** window, click on **Overview** in the left
    navigation menu, then under the **Get Started** tab, click on the
    **Go to Azure OpenAI Studio** button to open **Azure OpenAI Studio**
    in a new browser.

> <img src="./media/image32.png" style="width:6.5in;height:3.675in" />

16. Make sure **gpt-4o-mini**, **text-embedding-ada-002** should be
    deployed successfully .

> <img src="./media/image33.png" style="width:6.5in;height:4.15in" />

17. On the resource group and click on **storage account** resource
    name.

> <img src="./media/image34.png" style="width:6.5in;height:3.71667in" />
>
> <img src="./media/image35.png"
> style="width:6.38722in;height:3.3125in" />

18. Now open the URL it into a browser

> <img src="./media/image36.png" style="width:6.5in;height:3.91736in" />

19. Click on the **Chat**

> <img src="./media/image37.png" style="width:6.5in;height:3.91667in" />

20. In the **Blazor OpenAI** web app page, enter the following text and
    click on the **Submit icon** as shown in the below image.

> **+++What is included in my Northwind Health Plus plan that is not in
> standard?+++**
>
> <img src="./media/image38.png"
> style="width:7.11468in;height:3.85417in" />
>
> <img src="./media/image39.png" style="width:6.08988in;height:3.624in"
> alt="A screenshot of a computer Description automatically generated" />

21. In the **Blazor OpenAI** web app page, enter the following text and
    click on the **Submit icon** as shown in the below image.

> **+++Can I use out-of-network providers?+++**
>
> <img src="./media/image40.png"
> style="width:6.76639in;height:3.70417in" />
>
> <img src="./media/image41.png"
> style="width:6.23588in;height:3.38976in" />

22. In the **Blazor OpenAI** web app page, enter the following text and
    click on the **Submit icon** as shown in the below image.

> **+++Are there any exclusions or restrictions?+++**
>
> <img src="./media/image42.png"
> style="width:6.49167in;height:3.20833in" />
>
> <img src="./media/image43.png" style="width:6.5in;height:3.34167in" />

23. In the **Blazor OpenAI** web app page, enter the following text and
    click on the **Submit icon** as shown in the below image.

> **+++What does a Product Manager do?+++**
>
> <img src="./media/image44.png" style="width:6.5in;height:3.72778in" />

24. Click on the **Documents.**

> <img src="./media/image45.png"
> style="width:6.69595in;height:3.6875in" />

## Task 5: Delete the Resources

1.  To delete Resource group , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

> <img src="./media/image46.png" style="width:6.5in;height:4.22569in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the resource group.

> <img src="./media/image47.png"
> style="width:5.30307in;height:4.0125in" />

3.  In the resource group home page , select **Delete resource group**
    button.

> <img src="./media/image48.png" style="width:4.40833in;height:2.2875in"
> alt="A screenshot of a computer Description automatically generated" />

4.  On the Delete a resource group tab, enter the resource group and
    click on the **Delete** button.

> <img src="./media/image49.png" style="width:3.14194in;height:1.79182in"
> alt="A screenshot of a computer error Description automatically generated" />

**Summary**

In this lab, you’ve learned how to set up and deploy an intelligent chat
application using Azure's suite of tools and services. Starting with the
installation of essential tools like Azure CLI and Node.js, you’ve
configured your development environment using Dev Containers in Visual
Studio Code. You've deployed a chat application that utilizes Azure
OpenAI and Azure Cognitive Search to answer questions from PDF files.
Finally, you’ve deleted the deployed resources to effectively manage
resources. This hands-on experience has equipped you with the skills to
develop and manage intelligent chat applications using the Retrieval
Augmented Generation pattern on Azure.

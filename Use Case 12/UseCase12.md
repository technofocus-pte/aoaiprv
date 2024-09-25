**Use case-Building a Serverless AI Chat using LangChain**

Building AI applications can be complex and time-consuming, but using
LangChain.js and Azure serverless technologies allows to greatly
simplify the process. This application is a chatbot that uses a set of
enterprise documents to generate responses to user queries.

We provide sample data to make this sample ready to try, but feel free
to replace it with your own. We use a fictitious company called *Contoso
Real Estate*, and the experience allows its customers to ask support
questions about the usage of its products. The sample data includes a
set of documents that describes its terms of service, privacy policy and
a support guide.

<img src="./media/image1.png" style="width:6.5in;height:5.72847in"
alt="A diagram of a computer Description automatically generated" />

- **Serverless Architecture**: Utilizes Azure Functions and Azure Static
  Web Apps for a fully serverless deployment.

- **Retrieval-Augmented Generation (RAG)**: Combines the power of Azure
  Cosmos DB and LangChain.js to provide relevant and accurate responses.

- **Scalable and Cost-Effective**: Leverages Azure's serverless
  offerings to provide a scalable and cost-effective solution.

- **Local Development**: Supports local development using Ollama for
  testing without any cloud costs.

**Objective**

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

> **winget install microsoft.azd**

<img src="./media/image3.png" style="width:6.5in;height:2.66667in"
alt="A screen shot of a computer Description automatically generated" />

3.  Run the below command to set the policy to **Unrestricted** and
    enter **A** when asked to change the execution policy.

> **Set-ExecutionPolicy Unrestricted**
>
> <img src="./media/image4.png" style="width:6.5in;height:2.03056in"
> alt="A computer screen with white text Description automatically generated" />

## Task 2: Install Node.js

1.  Open your browser, navigate to the address bar, type or paste the
    following URL: <https://nodejs.org/en/download/> then press the
    **Enter** button.

<img src="./media/image5.png" style="width:5.78333in;height:2.05in" />

2.  Select and click on **Windows Installer**.

<img src="./media/image6.png" style="width:6.49167in;height:3.56667in"
alt="A screenshot of a computer Description automatically generated" />

3.  **Node-V** file will be downloaded. Click on the downloaded file to
    set up **Node.js**

<img src="./media/image7.png" style="width:5.30833in;height:2.14167in"
alt="A screenshot of a computer Description automatically generated" />

4.  In the **Welcome to the Node.js Setup Wizard** window, click on the
    **Next button**.

<img src="./media/image8.png" style="width:5.09167in;height:3.94167in"
alt="A screenshot of a computer Description automatically generated" />

5.  In the **End-User License Agreement** window, select **I accept the
    terms in the License agreement** radio button and click on the
    **Next** button.

<img src="./media/image9.png" style="width:5.06667in;height:3.95833in"
alt="A screenshot of a software setup Description automatically generated" />

6.  In the **Destination Folder** window, click on the **Next** button.

<img src="./media/image10.png" style="width:5.08333in;height:3.91667in"
alt="A screenshot of a computer Description automatically generated" />

7.  In the **Custom Setup** window, click on the **Next** button.

<img src="./media/image11.png" style="width:5.075in;height:4.00833in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image12.png" style="width:5.14167in;height:4in"
alt="A screenshot of a computer Description automatically generated" />

8.  In Ready to install Node.js window, click on **Install.**

<img src="./media/image13.png" style="width:5.13333in;height:3.95833in"
alt="A screenshot of a software Description automatically generated" />

9.  In **Completing the Node.js Setup Wizard window**, click on the
    **Finish** button to complete the installation process.

<img src="./media/image14.png" style="width:5.09167in;height:4.06667in"
alt="A screenshot of a computer Description automatically generated" />

## Task 3: Assign a user as an owner of an Azure subscription

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:
    [<u>https://portal.azure.com/</u>](https://portal.azure.com/), then
    press the **Enter** button.

> <img src="./media/image15.png" style="width:6.49167in;height:4.14167in"
> alt="A screenshot of a computer Description automatically generated" />

2.  In the **Microsoft Azure** window, use the **User Credentials** to
    login to Azure.

<img src="./media/image16.png" style="width:4.18371in;height:4.0713in"
alt="A screenshot of a computer Description automatically generated" />

3.  Then, enter the password and click on the **Sign in** button**.**

> <img src="./media/image17.png" style="width:4.5in;height:3.56042in"
> alt="A screenshot of a login box Description automatically generated" />

4.  In **Stay signed in?** window, click on the **Yes** button.

> <img src="./media/image18.png" style="width:4.46806in;height:2.98617in"
> alt="Graphical user interface, application Description automatically generated" />

5.  Type in **Subscriptions** in the search bar and select
    **Subscriptions**.

<img src="./media/image19.png" style="width:6.5in;height:3.69444in"
alt="A screenshot of a computer Description automatically generated" />

6.  Click on your assigned **subscription**.

<img src="./media/image20.png" style="width:6.5in;height:2.57917in"
alt="A screenshot of a computer Description automatically generated" />

7.  From the left menu, click on the **Access control(IAM).**

<img src="./media/image21.png" style="width:6.49167in;height:5.41667in"
alt="A screenshot of a computer Description automatically generated" />

8.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

<img src="./media/image22.png" style="width:5.8625in;height:4.02624in"
alt="A screenshot of a computer Description automatically generated" />

9.  In the Role tab, select the **Privileged administrator roles** and
    select **Owner** . Click **Next**

<img src="./media/image23.png" style="width:4.99212in;height:4.2625in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image24.png" style="width:5.00417in;height:6.0673in"
alt="A screenshot of a computer Description automatically generated" />

10. In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

<img src="./media/image25.png" style="width:6.5in;height:7.05in"
alt="A screenshot of a computer Description automatically generated" />

11. On the Select members tab , select your Azure OpenAI credentials and
    click **Select.**

<img src="./media/image26.png" style="width:3.89167in;height:7.275in"
alt="A screenshot of a computer Description automatically generated" />

12. In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

<img src="./media/image27.png" style="width:5.99953in;height:6.65417in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image28.png" style="width:4.9625in;height:5.26788in"
alt="A screenshot of a computer Description automatically generated" />

13. You will see a notification – added as Owner for Azure
    Pass-Sponsorship.

<img src="./media/image29.png" style="width:3.53781in;height:1.61264in"
alt="A screenshot of a computer Description automatically generated" />

## Task 4: Run the Docker

1.  In your Windows search box, type Docker , then click on **Docker
    Desktop**.

> <img src="./media/image30.png"
> style="width:5.62208in;height:5.0375in" />

2.  Run the Docker Desktop.

> <img src="./media/image31.png" style="width:5.96626in;height:3.37578in"
> alt="A screenshot of a computer Description automatically generated" />

## **Task 5:** **Install Dev Containers extension**

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> <img src="./media/image32.png"
> style="width:4.94583in;height:4.94583in" />

2.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    [https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers%20)
    then press the **Enter** button.

> <img src="./media/image33.png" style="width:6.55254in;height:4.12474in"
> alt="A screenshot of a computer Description automatically generated" />

3.  On Dev Containers page, select on Install button.

<img src="./media/image34.png" style="width:6.53595in;height:3.7875in"
alt="A screenshot of a computer Description automatically generated" />

4.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

<img src="./media/image35.png" style="width:7.07006in;height:4.32917in"
alt="A screenshot of a computer Description automatically generated" />

5.  Open the Visual Studio Code.

<img src="./media/image36.png" style="width:6.5in;height:4.55in"
alt="A screenshot of a computer Description automatically generated" />

## Task 6: Open development environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    <https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/Azure-Samples/serverless-chat-langchainjs>

then press the **Enter** button.

<img src="./media/image37.png" style="width:6.5in;height:1.24375in"
alt="A white background with black text Description automatically generated" />

2.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

> <img src="./media/image38.png" style="width:6.5in;height:1.47917in"
> alt="A screenshot of a computer Description automatically generated" />
>
> <img src="./media/image39.png" style="width:6.5in;height:4.12292in" />

3.  Do you want to install the recommended ‘ Azure Functions’ extension
    from Microsoft for the repository? dialog box appears, then click on
    the **Install** button.

> <img src="./media/image40.png" style="width:6.5in;height:3.51667in" />
>
> <img src="./media/image41.png" style="width:6.5in;height:3.57639in"
> alt="A screenshot of a computer Description automatically generated" />

4.  Sign in to Azure with the Azure Developer CLI. Run the following
    command on the Terminal

> BashCopy
>
> **<span class="mark">azd auth login</span>**
>
> <img src="./media/image42.png"
> style="width:6.49167in;height:3.56667in" />

5.  Default browser opens to sign in .Sign in with your Azure
    subscription account.

> <img src="./media/image43.png" style="width:5.72083in;height:4.025in"
> alt="A screenshot of a computer Description automatically generated" />
>
> <img src="./media/image44.png" style="width:4.90833in;height:4.275in" />

6.  Close the browser

> <img src="./media/image45.png" style="width:6.5in;height:1.6375in"
> alt="A screenshot of a computer Description automatically generated" />

7.  Once logged in, the details of the Azure login are populated in the
    terminal.

<img src="./media/image46.png" style="width:6.5in;height:2.3in" />

## Task 7: Deploy chat app to Azure

1.  Run the following Azure Developer CLI command to provision the Azure
    resources and deploy the source code

> BashCopy
>
> **<span class="mark">azd up</span>**

2.  prompted to enter an environment name, enter the
    **aoailangchainXX(**(XX can be a unique number)

> <img src="./media/image47.png" style="width:6.5in;height:3.85833in" />

3.  When prompted, select a **subscription** to create the resources and
    select a location **East US2**, This location is used for most the
    resources including hosting. 

**Note:** For this use case, you will use a GPT-4, text-embedding-ada-2
models. This models is currently only available in [certain
regions](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#embeddings-models).
Please select a region from this list, In this lab **East US2** is using
for this resource

<img src="./media/image48.png" style="width:6.5in;height:3.58333in" />

> <img src="./media/image49.png"
> style="width:6.49167in;height:3.75833in" />

4.  Wait until app is deployed. It may take 20-30 minutes for the
    deployment to complete.

> <img src="./media/image50.png"
> style="width:6.49167in;height:4.20833in" />

5.  After the application has been successfully deployed, you see a URL
    displayed in the terminal. Copy the **URL**.

> <img src="./media/image51.png" style="width:5.775in;height:3.52134in" />

## Task 8: Verify deployed resources in the Azure portal

1.  Open a browser go to <https://portal.azure.com> and sign in with
    your Azure subscription account.

2.  On the Home page, click on **Resource Groups**.

> <img src="./media/image52.png"
> style="width:5.39583in;height:3.23058in" />

3.  Click on your resource group name **rg-aoailangchainXX**

> <img src="./media/image53.png"
> style="width:6.49167in;height:2.94167in" />

4.  Make sure the below resource got deployed successfully

    - Application insights

    - Azure Cosmos DB

    - Azure OpenAI Service

    - Function App

    - Azure Storage

    - Azure Networking

    - Static Web App

> <img src="./media/image54.png"
> style="width:6.49167in;height:3.35833in" />
>
> <img src="./media/image55.png" style="width:6.5in;height:3.88125in"
> alt="A screenshot of a computer Description automatically generated" />

6.  On the resource group and click on **Azure OpenAI** resource name.

> <img src="./media/image56.png"
> style="width:6.49167in;height:3.39167in" />

7.  On the **Azure OpenAI** window, click on **Overview** in the left
    navigation menu, then under the **Get Started** tab, click on the
    **Go to Azure OpenAI Studio** button to open **Azure OpenAI Studio**
    in a new browser.

> <img src="./media/image57.png" style="width:6.5in;height:3.51667in" />

8.  Make sure **gpt-4**, **text-embedding-ada-002** should be deployed
    successfully .

<img src="./media/image58.png" style="width:6.49167in;height:4.275in" />

9.  Now open the URL (**(**The URL that you have saved in your notepad
    in the **Task 7)** it into a browser.

<img src="./media/image59.png" style="width:6.5in;height:3.52361in"
alt="A screenshot of a computer Description automatically generated" />

10. Click on an example **How to search and book rentals**?

> <img src="./media/image60.png" style="width:6.5in;height:3.56667in" />
>
> <img src="./media/image61.png"
> style="width:6.49167in;height:3.61667in" />

11. Click on an example **How can I download the mobile app**?

<img src="./media/image62.png"
style="width:6.49167in;height:3.55833in" />

## Task 9: Delete the Resources

1.  To delete Resource group , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

> <img src="./media/image63.png" style="width:6.5in;height:4.22569in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the rg-aoailangchainXX resource group.

> <img src="./media/image64.png"
> style="width:6.49167in;height:3.55833in" />

3.  In the resource group home page , select **Delete resource group**
    button.

> <img src="./media/image65.png"
> style="width:6.49167in;height:3.76667in" />

4.  On the Delete a resource group tab, enter the resource group and
    click on the **Delete** button.

> <img src="./media/image66.png"
> style="width:5.00833in;height:7.21667in" />
>
> <img src="./media/image67.png" style="width:3.14194in;height:1.79182in"
> alt="A screenshot of a computer error Description automatically generated" />

**Summary**

In this lab, you’ve learned how to set up and deploy an intelligent chat
application using Azure's suite of tools and services. Starting with the
installation of essential tools like Azure CLI and Node.js, you’ve
configured your development environment using Dev Containers in Visual
Studio Code. You've deployed Serverless AI Chat using LangChain that
utilizes Azure OpenAI and storage account to answer questions from PDF
files. Finally, you’ve deleted the deployed resources to effectively
manage resources. This hands-on experience has equipped you with the
skills to develop and manage intelligent chat applications using the
Retrieval Augmented Generation pattern on Azure.

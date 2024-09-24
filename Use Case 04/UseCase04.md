**Introduction**

This sample demonstrates a few approaches for creating ChatGPT-like
experiences over your own data using the Retrieval Augmented Generation
pattern. It uses Azure OpenAI Service to access the ChatGPT model
(gpt-35-turbo), and Azure Cognitive Search for data indexing and
retrieval.

The repo includes sample data so it's ready to try end to end. In this
sample application we use a fictitious company called Contoso
Electronics, and the experience allows its employees to ask questions
about the benefits, internal policies, as well as job descriptions and
roles.

This use case you through the process of developing a sophisticated chat
application using the Retrieval Augmented Generation (RAG) pattern on
the Azure platform. By leveraging Azure OpenAI Service and Azure
Cognitive Search, you will create a chat application that can
intelligently answer questions using your own data. This lab uses a
fictitious company, Contoso Electronics, as a case study to demonstrate
how to build a ChatGPT-like experience over enterprise data, covering
aspects such as employee benefits, internal policies, and job roles.

<img src="./media/image1.png" style="width:6.5in;height:3.09097in"
alt="RAG Architecture" />

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

<img src="./media/image6.png"
style="width:6.49167in;height:3.56667in" />

3.  **Node-V** file will be downloaded. Click on the downloaded file to
    set up **Node.js**

<img src="./media/image7.png" style="width:5.30833in;height:2.14167in"
alt="A screenshot of a computer Description automatically generated" />

4.  In the **Welcome to the Node.js Setup Wizard** window, click on the
    **Next button**.

<img src="./media/image8.png"
style="width:5.09167in;height:3.94167in" />

5.  In the **End-User License Agreement** window, select **I accept the
    terms in the License agreement** radio button and click on the
    **Next** button.

<img src="./media/image9.png" style="width:5.06667in;height:3.95833in"
alt="A screenshot of a software setup Description automatically generated" />

6.  In the **Destination Folder** window, click on the **Next** button.

<img src="./media/image10.png" style="width:5.08333in;height:3.91667in"
alt="A screenshot of a computer Description automatically generated" />

7.  In the **Custom Setup** window, click on the **Next** button.

<img src="./media/image11.png" style="width:5.075in;height:4.00833in" />

<img src="./media/image12.png" style="width:5.14167in;height:4in" />

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

<img src="./media/image27.png" style="width:6.49167in;height:7.2in"
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

<img src="./media/image30.png"
style="width:6.49167in;height:5.81667in" />

2.  Run the Docker Desktop.

<img src="./media/image31.png"
style="width:7.1577in;height:4.04991in" />

## **Task 5:** **Install Dev Containers extension**

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> <img src="./media/image32.png"
> style="width:4.94583in;height:4.94583in" />

2.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    [https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers%20)
    then press the **Enter** button.

> <img src="./media/image33.png" style="width:7.04314in;height:4.43356in"
> alt="A screenshot of a computer Description automatically generated" />

3.  On Dev Containers page, select on Install button.

<img src="./media/image34.png"
style="width:7.03927in;height:4.07917in" />

4.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

<img src="./media/image35.png"
style="width:7.07006in;height:4.32917in" />

5.  Open the Visual Studio Code.

<img src="./media/image36.png" style="width:6.5in;height:4.55in"
alt="A screenshot of a computer Description automatically generated" />

## Task 6: Open development environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    <https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo>

then press the **Enter** button.

<img src="./media/image37.png" style="width:6.5in;height:1.24375in"
alt="A white background with black text Description automatically generated" />

2.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

<img src="./media/image38.png" style="width:6.5in;height:1.47917in"
alt="A screenshot of a computer Description automatically generated" />

3.  To Staring Dev container will take 13-15 min

> <img src="./media/image39.png" style="width:6.5in;height:3.93403in"
> alt="A screenshot of a computer Description automatically generated" />

4.  Sign in to Azure with the Azure Developer CLI. Run the following
    command on the Terminal

> BashCopy
>
> **<span class="mark">azd auth login</span>**
>
> <img src="./media/image40.png" style="width:6.5in;height:4.43333in" />

5.  Default browser opens to sign in .Sign in with your Azure
    subscription account.

> <img src="./media/image41.png" style="width:5.72083in;height:4.025in" />
>
> <img src="./media/image42.png" style="width:4.90833in;height:4.275in" />

6.  Close the browser

<img src="./media/image43.png" style="width:6.5in;height:1.6375in"
alt="A screenshot of a computer Description automatically generated" />

7.  Once logged in, the details of the Azure login are populated in the
    terminal.

> <img src="./media/image44.png" style="width:6.5in;height:4.47847in"
> alt="A screenshot of a computer Description automatically generated" />

## Task 7: Deploy chat app to Azure

1.  Run the following Azure Developer CLI command to provision the Azure
    resources and deploy the source code

> BashCopy
>
> **<span class="mark">azd up</span>**

<img src="./media/image45.png"
style="width:7.21875in;height:4.8125in" />

2.  prompted to enter an environment name, enter the **chatsampleRAG**

> <img src="./media/image46.png"
> style="width:6.98784in;height:4.2375in" />

3.  When prompted, select a **subscription** to create the resources and
    select a location **East US2**, This location is used for most the
    resources including hosting. 

> <img src="./media/image47.png" style="width:6.49167in;height:3.5in" />

4.  When prompted, **enter a value for the ‘openAiResourceGroupLocation’
    infrastructure parameter** select **East US2.**

> <img src="./media/image48.png" style="width:6.5in;height:3.30833in" />

5.  When prompted, enter a values for openai resource group locatin
    infrastructure parameter then select **East US 2
    .**<img src="./media/image49.png" style="width:6.5in;height:4.05in" />

6.  save the value in the environment for future use (y/N) enter **Y.**

> <img src="./media/image50.png" style="width:6.5in;height:3.90833in" />

7.  Wait until app is deployed. It may take 35-40 minutes for the
    deployment to complete.

> <img src="./media/image51.png" style="width:6.5in;height:3.34375in"
> alt="A screenshot of a computer Description automatically generated" />

8.  After the application has been successfully deployed, you see a URL
    displayed in the terminal. Copy the **URL**.

<img src="./media/image52.png"
style="width:6.49167in;height:3.98333in" />

9.  Open your browser, navigate to the address bar, paste the link. Now,
    resource group will open in a new browser

<img src="./media/image53.png" style="width:6.5in;height:2.51042in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image54.png" style="width:6.5in;height:3.96111in"
alt="A screenshot of a computer Description automatically generated" />

## Task 8: Use chat app to get answers from PDF files

1.  Wait for the web application deployment to complete.

<img src="./media/image55.png" style="width:6.5in;height:3.20903in" />

2.  In the **GPT+Eneterprise data \|Sample** web app page, enter the
    following text and click on the **Submit icon** as shown in the
    below image.

> **<span class="mark">What happens in a performence review?</span>**

<img src="./media/image56.png"
style="width:7.18333in;height:3.59167in" />

<img src="./media/image57.png" style="width:7.18086in;height:3.67559in"
alt="A screenshot of a computer Description automatically generated" />

3.  From the answer, select a **citation**.

<img src="./media/image58.png"
style="width:7.3871in;height:3.81667in" />

4.  In the right-pane, use the tabs to understand how the answer was
    generated.

| **Tab** | **Description** |
|----|----|
| **Thought process** | This is a script of the interactions in chat. You can view the system prompt (content) and your user question (content). |
| **Supporting content** | This includes the information to answer your question and the source material. The number of source material citations is noted in the **Developer settings**. The default value is **3**. |
| **Citation** | This displays the original page that contains the citation. |

<img src="./media/image59.png"
style="width:7.31185in;height:3.49167in" />

<img src="./media/image60.png"
style="width:7.13819in;height:3.48673in" />

<img src="./media/image61.png" style="width:7.38in;height:3.6in" />

5.  Select the selected tab again to close the pane.

6.  The intelligence of the chat is determined by the OpenAI model and
    the settings that are used to interact with the model.

7.  Select the **Developer settings**.

<img src="./media/image62.png"
style="width:7.44004in;height:3.3375in" />

<img src="./media/image63.png"
style="width:4.76708in;height:7.62566in" />

| **Setting** | **Description** |
|----|----|
| Override prompt template | This is the prompt that is used to generate the answer. |
| Retrieve this many search results | This is the number of search results that are used to generate the answer. You can see these sources returned in the *Thought process* and *Supporting content* tabs of the citation. |
| Exclude category | This is the category of documents that are excluded from the search results. |
| Use semantic ranker for retrieval | This is a feature of [Azure AI Search](https://learn.microsoft.com/en-us/azure/search/semantic-search-overview#what-is-semantic-search) that uses machine learning to improve the relevance of search results. |
| Use query-contextual summaries instead of whole documents | When both Use semantic ranker and Use query-contextual summaries are checked, the LLM uses captions extracted from key passages, instead of all the passages, in the highest ranked documents. |
| Suggest follow-up questions | Have the chat app suggest follow-up questions based on the answer. |
| Retrieval mode | **Vectors + Text** means that the search results are based on the text of the documents and the embeddings of the documents. **Vectors** means that the search results are based on the embeddings of the documents. **Text** means that the search results are based on the text of the documents. |
| Stream chat completion responses | Stream response instead of waiting until the complete answer is available for a respon |

8.  Check the **Suggest follow-up questions** checkbox and ask the same
    question again.

<img src="./media/image64.png" style="width:3.65in;height:7.56667in" />

9.  Enter the following text and click on the **Submit icon** as shown
    in the below image.

> <span class="mark">What happens in a performance review?</span>

<img src="./media/image65.png" style="width:6.49167in;height:3.775in" />

10. The chat returned suggested follow-up questions such as the
    following

<img src="./media/image66.png" style="width:6.49167in;height:3.3in" />

11. In the **Settings** tab, deselect **Use semantic ranker for
    retrieval**.

<img src="./media/image67.png" style="width:6.5in;height:1.7in" />

<img src="./media/image68.png"
style="width:3.41667in;height:7.46667in" />

12. Enter the following text and click on the **Submit icon** as shown
    in the below image.

> <span class="mark">What happens in a performance review?</span>

<img src="./media/image69.png"
style="width:7.31612in;height:4.10417in" />

<img src="./media/image70.png"
style="width:7.29473in;height:4.70962in" />

## Task 9: Delete the Resources

1.  To delete Resource group , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

> <img src="./media/image71.png" style="width:6.5in;height:4.22569in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the sample web app resource group.

> <img src="./media/image72.png"
> style="width:4.73333in;height:4.36667in" />

3.  In the resource group home page , select **Delete resource group**
    button.

<img src="./media/image73.png"
style="width:6.98478in;height:4.6625in" />

4.  On the Delete a resource group tab, enter the resource group and
    click on the **Delete** button.

<img src="./media/image74.png" style="width:5.90417in;height:7.05in" />

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

**Introduction**

This scenario creates a web-based chat application with an API backend
that can use OpenAI chat models to answer questions about the items in a
PostgreSQL database table. The frontend is built with React and
FluentUI, while the backend is written with Python and FastAPI.

This scenario provides the following features:

- Hybrid search on the PostgreSQL database table, using [the pgvector
  extension](https://github.com/pgvector/pgvector) for the vector search
  plus [full text
  search](https://www.postgresql.org/docs/current/textsearch-intro.html),
  combining the results using RRF (Reciprocal Rank Fusion).

- OpenAI function calling to optionally convert user queries into query
  filter conditions, such as turning "Climbing gear cheaper than \$30?"
  into "WHERE price \< 30".

- Conversion of user queries into vectors using the OpenAI embedding
  API.

<img src="./media/image1.png" style="width:6.48333in;height:3.775in" />

In this use case, you will set up a comprehensive development
environment, deploy a chat application integrated with PostgreSQL, and
verify its deployment on Azure. This involves installing essential tools
like Azure CLI, Node.js, Docker, and Visual Studio Code, configuring
user roles in Azure, deploying the application using Azure Developer
CLI, and interacting with the deployed resources to ensure
functionality.

**Objective:**

- To configure the development environment on Windows by installing
  Azure CLI, Node.js, assigning Azure subscription roles, starting
  Docker Desktop, and enabling Visual Studio Code with Dev Containers
  extension.

- To deploy and test Custom Chat Application with PostgreSQL and OpenAI
  on Azure.

## Exercise 1: set up environment

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
    following URL: !!https://nodejs.org/en/download/!! then press the
    **Enter** button.

<img src="./media/image5.png" style="width:5.78333in;height:2.05in"
alt="A screenshot of a computer Description automatically generated" />

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
    the following URL: !!https://portal.azure.com/!!, then press the
    **Enter** button.

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

<img src="./media/image30.png" style="width:6.49167in;height:5.81667in"
alt="A screenshot of a computer Description automatically generated" />

2.  Run the Docker Desktop.

<img src="./media/image31.png" style="width:7.1577in;height:4.04991in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 5:** **Install Dev Containers extension**

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> <img src="./media/image32.png" style="width:4.94583in;height:4.94583in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    !!https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers!!
    then press the **Enter** button.

> <img src="./media/image33.png" style="width:7.04314in;height:4.43356in"
> alt="A screenshot of a computer Description automatically generated" />

3.  On Dev Containers page, select on Install button.

<img src="./media/image34.png" style="width:7.03927in;height:4.07917in"
alt="A screenshot of a computer Description automatically generated" />

4.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

<img src="./media/image35.png" style="width:7.07006in;height:4.32917in"
alt="A screenshot of a computer Description automatically generated" />

5.  Open the Visual Studio Code.

<img src="./media/image36.png" style="width:6.5in;height:3.66667in" />

<img src="./media/image37.png" style="width:6.5in;height:4.55in"
alt="A screenshot of a computer Description automatically generated" />

## Exercise 2: Deploy the application and test it from the browser

## Task 1: Open development environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    !!https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/rag-postgres-openai-python!!

then press the **Enter** button.

<img src="./media/image38.png" style="width:6.5in;height:1.24375in"
alt="A white background with black text Description automatically generated" />

2.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

<img src="./media/image39.png" style="width:6.5in;height:1.47917in"
alt="A screenshot of a computer Description automatically generated" />

3.  In case, **Allow an extension to open this URI?** dialog box
    appears, then click on the **Open** button.

<img src="./media/image40.png" style="width:6.5in;height:3.74167in" />

4.  In case, **Cloning a repository in a Dev Container may execute
    arbitrary code** dialog box appears, then click on the **Got it**
    button.

<img src="./media/image41.png" style="width:6.5in;height:3.81667in" />

5.  To Staring Dev container will take 13-15 min

<img src="./media/image42.png" style="width:6.54944in;height:4.57901in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image43.png" style="width:7.10291in;height:3.78215in"
alt="A screenshot of a computer Description automatically generated" />

6.  After cloning the repo press any key

<img src="./media/image44.png"
style="width:7.19082in;height:3.81667in" />

## Task 2: Deploy chat app to Azure

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image45.png" style="width:6.5in;height:5.64167in"
alt="A screenshot of a computer Description automatically generated" />

2.  Sign in to Azure with the Azure Developer CLI. Run the following
    command on the Terminal

> BashCopy
>
> **<span class="mark">!!azd auth login</span>!!**

<img src="./media/image46.png"
style="width:7.28363in;height:3.67917in" />

3.  Default browser opens to sign in. Sign in with your Azure
    subscription account.

> <img src="./media/image47.png" style="width:5.72083in;height:4.025in"
> alt="A screenshot of a computer Description automatically generated" />
>
> <img src="./media/image48.png" style="width:4.90833in;height:4.275in"
> alt="A login screen with a red box and blue text Description automatically generated" />

4.  Close the browser

<img src="./media/image49.png" style="width:6.5in;height:2.74722in"
alt="A screenshot of a computer Description automatically generated" />

5.  To create an environment for Azure resources, run the following
    Azure Developer CLI command.

> BashCopy
>
> **!!azd env new!!**

<img src="./media/image50.png" style="width:6.49167in;height:3.325in" />

6.  prompted to enter an environment name, enter the **ragsqlXX**(XX can
    be a unique number, you can add more digits after XX to make the
    name unique)

**Note:** When creating an environment, ensure that the name consists of
lowercase letters.

<img src="./media/image51.png"
style="width:6.49167in;height:2.03333in" />

7.  Run the following Azure Developer CLI command to provision the Azure
    resources and deploy the source code.

> BashCopy
>
> **!!azd up!!**

<img src="./media/image52.png"
style="width:6.49167in;height:3.51667in" />

8.  When prompted, select a **subscription** to create the resources and
    select the region closest to your location; in this lab, we have
    chosen the East US2
    region.<img src="./media/image53.png" style="width:6.5in;height:3.23333in" />

<img src="./media/image54.png" style="width:7.322in;height:3.23333in" />

9.  When prompted, **enter a value for the ‘openAILocation’
    infrastructure parameter** select the region closest to your
    location; in this lab, we have chosen the **North Central US**
    region
    <img src="./media/image55.png" style="width:7.1743in;height:3.1058in" />

<img src="./media/image56.png" style="width:6.5in;height:3.45486in"
alt="A screenshot of a computer program Description automatically generated" />

<img src="./media/image57.png" style="width:6.5in;height:3.66667in" />

10. Deployment will take around 19-20 min

<img src="./media/image58.png" style="width:6.12732in;height:3.87409in"
alt="A screenshot of a computer Description automatically generated" />

11. Deployment completed and front end hosted successfully. Copy the URL
    and paste it into a browser and save URL in notepad

URL look likes-

https://ragpsql-3vlvcq6uzuk-ca.wonderfulcliff-01f39f01.eastus2.azurecontainerapps.io/

<img src="./media/image59.png" style="width:6.49167in;height:4.35in" />

<img src="./media/image60.png" style="width:7.28573in;height:3.70436in"
alt="A screenshot of a chat Description automatically generated" />

## Task 3: Verify deployed resources in the Azure portal

1.  Open a browser go to !!https://portal.azure.com!! and sign in with
    your Azure subscription account.

2.  On the Home page, click on **Resource Groups**.

> <img src="./media/image61.png" style="width:6.5in;height:3.86667in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Click on your resource group name

> <img src="./media/image62.png"
> style="width:6.59825in;height:2.8375in" />

4.  Make sure the below resource got deployed successfully

- Container App

- Application Insights

- Container Apps Environment

- Log Analytics workspace

- Azure OpenAI

- Azure Database for PostgreSQL flexible server

- Container registry

> <img src="./media/image63.png" style="width:7.0174in;height:3.73137in"
> alt="A screenshot of a computer Description automatically generated" />

5.  On the resource group and click on **Azure OpenAI** resource name.

> <img src="./media/image64.png"
> style="width:6.99583in;height:3.76026in" />

6.  On the **Azure OpenAI** window, click on **Overview** in the left
    navigation menu, then under the **Get Started** tab, click on the
    **Go to Azure OpenAI Studio** button to open **Azure OpenAI Studio**
    in a new browser.

> <img src="./media/image65.png"
> style="width:7.05191in;height:3.30417in" />

7.  Make sure **gpt-35-turbo**, **text-embedding-ada-002** should be
    deployed successfully

> <img src="./media/image66.png" style="width:6.5in;height:3.25833in" />

## Task 4: Use chat app to get answers from files

1.  Now open the URL (**(**The URL that you have saved in your notepad
    in the **Exercise 2\> Task 2\>Step 11)** it into a browser.

2.  In the **RAG on database \|OpenAI+PoastgreSQL** web app page,
    **click on Best shoe for hiking?** button and observe the output

<img src="./media/image67.png"
style="width:7.09583in;height:3.79841in" />

<img src="./media/image68.png"
style="width:7.13868in;height:3.7417in" />

<img src="./media/image1.png" style="width:6.48333in;height:3.775in" />

3.  Click on the **clear chat.**

<img src="./media/image69.png"
style="width:6.49167in;height:3.61667in" />

4.  In the **RAG on database \|OpenAI+PoastgreSQL** web app page, click
    on **Climbing gear cheaper than \$30** button and observe the output

<img src="./media/image70.png"
style="width:6.49167in;height:3.21667in" />

<img src="./media/image71.png" style="width:6.49167in;height:3.075in" />

5.  Click on the **clear chat.**

<img src="./media/image69.png" style="width:6.49167in;height:3.61667in"
alt="A screenshot of a computer Description automatically generated" />

6.  In the **RAG on database \|OpenAI+PoastgreSQL** web app page, click
    on **Waterproof camping gear?** button and observe the output

<img src="./media/image72.png"
style="width:7.13329in;height:3.9375in" />

<img src="./media/image73.png"
style="width:7.3592in;height:4.10417in" />

## Task 5: Delete the Resources

1.  To delete Resource group , type **Resource groups** in the Azure
    portal search bar, navigate and click on **Resource groups** under
    **Services**.

<img src="./media/image74.png" style="width:6.5in;height:3.16667in" />

2.  Click on the sample web app resource group.

> <img src="./media/image75.png" style="width:6.5in;height:2.88333in" />

3.  In the resource group home page , select **Delete resource group**
    button.

<img src="./media/image76.png"
style="width:7.14635in;height:4.32083in" />

4.  On the Delete a resource group tab, enter the resource group and
    click on the **Delete** button.

<img src="./media/image77.png" style="width:5.45in;height:7.20833in" />

Summary:

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

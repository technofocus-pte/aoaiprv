**Lab 10-Build a chat bot using Azure OpenAI, Azure Cosmos DB for NoSQL and Blazor (Optional)**

Applications can connect to Azure Cosmos DB for NoSQL or Azure OpenAI
using their respective .NET SDKs. These SDKs can extend existing .NET
applications with NoSQL data storage and AI completion functionality
with relatively low friction.

The .NET SDK for Azure Cosmos DB for NoSQL is useful for business
applications that need to manage various account resources including
databases, containers, and items. The SDK can perform queries that
return multiple items, operations on specific items, and even
transactions that batch operations together over multiple items.

The .NET SDK for Azure OpenAI provides a streamlined interface for
interacting with the various models available for deployment.
Specifically, the SDK includes classes to interface directly with the
model, send prompts, fine tune the requests, and parse the completion
responses.

# Exercise 1: Setup

To complete this project, you need an Azure Cosmos DB for NoSQL account
and an Azure OpenAI account. To streamline this process, deploy a Bicep
template to Azure with both of these accounts.

## Task 1: Deploy infrastructure from template

1.  Open a new browser and enter the following URL in the address bar:
    <https://portal.azure.com/> to open the Azure Portal.

<img src="./media/image1.png" style="width:5.96176in;height:2.9598in" />

2.  In the Azure portal, click on the **\[\>\_\] (Cloud Shell)** button
    at the top of the page to the right of the search box. A Cloud Shell
    pane will open at the bottom of the portal. The first time you open
    the Cloud Shell, you may be prompted to choose the type of shell you
    want to use (**Bash** or **PowerShell**). Select **Bash**. If you
    don’t see this option, then skip this step.

> <img src="./media/image2.png" style="width:6.48333in;height:3.21667in"
> alt="A screenshot of a computer Description automatically generated with medium confidence" />

3.  In **You have no storage mounted** dialog box, click on the **Create
    storage.**

> <img src="./media/image3.png"
> style="width:6.49167in;height:2.36667in" />
>
> <img src="./media/image4.png" style="width:6.5in;height:2.55in"
> alt="A screenshot of a computer screen Description automatically generated" />

4.  Ensure the type of shell indicated on the top left of the Cloud
    Shell pane is switched to ***Bash***. If it’s ***PowerShell**,*
    switch to ***Bash*** by using the drop-down menu.

> <img src="./media/image5.png"
> style="width:5.96667in;height:5.60833in" />

5.  Once the terminal starts, enter the following command to download
    the sample application.

6.  Create a new shell variable named **resourceGroupName** with the
    name of the Azure resource group that you create
    (mslearn-cosmos-openai).

>```Copy
> resourceGroupName="mslearn-cosmos-openai

<img src="./media/image6.png" style="width:6.35in;height:3.17917in" />

7.  Create a resource group using [az group
    create](https://learn.microsoft.com/en-us/cli/azure/group#az-group-create()).
    Then, execute the following command

>```Copy
>az group create --name \$resourceGroupName --location "eastus"

<img src="./media/image7.png" style="width:7.04415in;height:3.9375in" />

8.  Deploy
    the [azuredeploy.json](https://github.com/Azure-Samples/cosmosdb-chatgpt/blob/main/azuredeploy.json) template
    file to the resource group using [az group deployment
    create](https://learn.microsoft.com/en-us/cli/azure/group/deployment#az-group-deployment-create).
    Then, execute the following command.

>```Copy
>az deployment group create --resource-group \$resourceGroupName --name
>zero-touch-deployment --template-uri
>https://raw.githubusercontent.com/Azure-Samples/cosmosdb-chatgpt/start/azuredeploy.json

9.  Wait for the deployment to complete before proceeding with this
    project. This deployment can take approximately 5-10 minutes.

<img src="./media/image8.png"
style="width:7.03024in;height:2.94583in" />

## Task 2: Get Azure Cosmos DB for NoSQL and Azure OpenAI account credentials

Deployed Azure Cosmos DB for NoSQL and Azure OpenAI accounts and then
stored their credentials in the Azure App Service web app's
configuration. Now, you have the choice of using the Azure portal or
Azure CLI to retrieve the credentials for each service.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL:
    [<u>https://portal.azure.com/</u>](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/announcing-the-public-preview-of-real-time-diarization-in-azure/ba-p/3876802),
    then press the **Enter** button.

> <img src="./media/image9.png" style="width:6.49167in;height:4.14167in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the **Portal Menu**, then select **Resource group.**

<img src="./media/image10.png" style="width:6.49167in;height:3.4in" />

3.  Select the **mslearn-cosmos-openai** resource group.

<img src="./media/image11.png"
style="width:4.93333in;height:4.28333in" />

4.  On the **Resource Groups** page, expand the **Essentials** panel and
    observe the **Deployments** header. The status for the deployment
    should be **Succeeded** at this point.

<img src="./media/image12.png"
style="width:7.19123in;height:2.47083in" />

5.  Now, select the **Azure Cosmos DB** account to navigate to the
    resource's page.

> <img src="./media/image13.png"
> style="width:7.16697in;height:4.1125in" />

6.  Select the **Keys** option in the **Settings** section of the
    resource navigation menu. Record the value of
    the **URI** and **PRIMARY KEY** fields. You use these values later.

<img src="./media/image14.png"
style="width:7.41869in;height:3.12917in" />

7.  Return to the **Resource Groups** page. Select the **Azure
    OpenAI** account.

> <img src="./media/image15.png"
> style="width:6.82917in;height:4.74539in" />

8.  In your **Azure Open AI** window, navigate to the **Resource
    Management** section, and click on **Keys and Endpoints**.

<img src="./media/image16.png" style="width:6.5in;height:4.9in" />

9.  In **Keys and Endpoints** page, copy **KEY1,** (*You can use
    either KEY1 or KEY2)* and **Endpoint** and then **Save** the notepad
    to use the information in the upcoming tasks.

> <img src="./media/image17.png"
> style="width:7.04193in;height:4.2125in" />

## Task 3: Run the Docker

1.  In your Windows search box, type Docker , then click on **Docker
    Desktop**.

<img src="./media/image18.png"
style="width:6.49167in;height:5.81667in" />

2.  Run the Docker Desktop.

<img src="./media/image19.png" style="width:7.1577in;height:4.04991in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 4: Install Dev Containers extension**

1.  In your Windows search box, type Visual Studio, then click on
    **Visual Studio Code**.

> <img src="./media/image20.png" style="width:4.94583in;height:4.94583in"
> alt="A screenshot of a computer Description automatically generated" />
>
> <img src="./media/image21.png" style="width:6.5in;height:3.45625in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    [https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers%20)
    then press the **Enter** button.

> <img src="./media/image22.png" style="width:7.04314in;height:4.43356in"
> alt="A screenshot of a computer Description automatically generated" />

3.  On Dev Containers page, select on **Install** button.

<img src="./media/image23.png" style="width:7.03927in;height:4.07917in"
alt="A screenshot of a computer Description automatically generated" />

4.  Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

<img src="./media/image24.png" style="width:7.07006in;height:4.32917in"
alt="A screenshot of a computer Description automatically generated" />

5.  Open the Visual Studio Code.

<img src="./media/image25.png" style="width:6.5in;height:4.55in"
alt="A screenshot of a computer Description automatically generated" />

6.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in"
alt="A screenshot of a computer program Description automatically generated" />

7.  Clone
    the [azure-samples/cosmosdb-chatgpt](https://github.com/azure-samples/cosmosdb-chatgpt) GitHub
    repository into the current directory.

**Copy**

<span class="mark">git clone
https://github.com/Azure-Samples/cosmosdb-chatgpt.git</span>

<img src="./media/image27.png" style="width:6.5in;height:2.95486in"
alt="A screen shot of a computer Description automatically generated" />

8.  In the **Teminal**, go to **cosmosdb-chatgpt** directory.

Copy

<span class="mark">cd cosmosdb-chatgpt</span>

9.  Switch to the start branch of the repository. Run the below command
    in the terminal

> BashCopy
>
> <span class="mark">git checkout start</span>

<img src="./media/image28.png" style="width:6.5in;height:4.71319in"
alt="A screenshot of a computer Description automatically generated" />

## Task 3: Configure dev environment

1.  Open the **Command Palette**, search for the \>**Dev
    Containers** commands, and then select \>**Dev Containers: Open
    Folder in Container**.

<img src="./media/image29.png" style="width:6.5in;height:3.1in" />

2.  Navigate and select **cosmosdb-chatgpt** folder from **C:\LabFiles**
    and click on the **Select Folder** button.

> <img src="./media/image30.png"
> style="width:6.49167in;height:4.01667in" />
>
> <img src="./media/image31.png" style="width:6.5in;height:3.39792in" />

3.  Visual Studio Code a notification stating Folder contains a Dev
    Container configuration file. Reopen folder to develop in a
    container appers, then click on the **Reopen in Container** button.

> <img src="./media/image32.png"
> style="width:7.14378in;height:2.7125in" />

1.  In case, **Not all host requirements in devcontainer.json are met by
    the Docker daemon.** dialog box appears, then click on the
    **Continue** button.

> <img src="./media/image33.png" style="width:3.75in;height:2.14167in" />

2.  To Staring Dev container will take 2-3 min

<img src="./media/image34.png" style="width:7.21588in;height:3.84924in"
alt="A screenshot of a computer Description automatically generated" />

3.  Validate that .NET 8 is installed in your environment, Run the below
    command

> BashCopy
>
> <span class="mark">dotnet --list-sdks</span>

<img src="./media/image35.png" style="width:6.5in;height:2.57917in" />

4.  Build the .NET project. Run the bellow command on the terminal.

> BashCopy
>
> <span class="mark">dotnet build</span>

<img src="./media/image36.png"
style="width:6.49167in;height:7.31667in" />

5.  Close the terminal.

# Exercise 2 - Setup and run the starter web application

The first step of this project is to walk through the existing starter
application, ensure it builds successfully, and then run the
application.

There are a few requirements in this exercise:

- Open the **CodeTour** within the application and walk through the
  entire tour.

- Successfully build the application.

- Run the application using the **Hot Reload** feature of .NET

After you complete this exercise, you'll have a general understanding of
the project and its components.

## Task 1: Walk through a tour of the code

1.  Open your browser, navigate to the address bar, type or paste the
    following URL:
    <https://marketplace.visualstudio.com/items?itemName=vsls-contrib.codetour>
    then press the **Enter** button.

<img src="./media/image37.png" style="width:6.5in;height:3.43542in" />

2.  On **Code Tour** page, select on **Install** button.

<img src="./media/image38.png"
style="width:6.49167in;height:3.86667in" />

10. Open Visual Studio Code? dialog box appears, then click on the
    **Open Visual Studio Code** button.

<img src="./media/image39.png"
style="width:6.49167in;height:1.98333in" />

<img src="./media/image40.png" style="width:6.93761in;height:3.87498in"
alt="A screenshot of a computer Description automatically generated" />

11. Open the **Command Palette**, search for
    the \>**CodeTour** commands, and then select \>**CodeTour: Start
    Tour**.

<img src="./media/image41.png"
style="width:6.97998in;height:3.0375in" />

12. Review the overview of the guided tour.

13. The guided tour of the codebase walks you through the following
    components of the application:

<img src="./media/image42.png" style="width:6.5in;height:1.575in"
alt="A screen shot of a computer Description automatically generated" />

- The Message and Session types in the /Models path

> <img src="./media/image43.png" style="width:6.49167in;height:1.425in" />
>
> <img src="./media/image44.png"
> style="width:6.49167in;height:3.76667in" />

- The Bicep template and various properties of the resources it deployed

> <img src="./media/image45.png" style="width:6.49167in;height:4.725in" />

- The CosmosDbService and OpenAiService classes you modify as part of
  this project

> <img src="./media/image46.png" style="width:6.5in;height:1.90833in" />

14. Finally, review the final step of the guided tour and finish the
    tour.

> <img src="./media/image47.png" style="width:6.5in;height:1.53333in" />

## Task 2: Build and run the application

Now it's time to make sure the application works as expected. In this
step, build the application to verify that there's no issues before you
start and run the application using the stubbed out implementations of
the service methods.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in" />

2.  Start the application with hot reloads enabled using [dotnet
    watch](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-watch).
    Run the below command

> BashCopy
>
> <span class="mark">dotnet watch run --non-interactive</span>

<img src="./media/image48.png"
style="width:6.49167in;height:4.33333in" />

3.  Visual Studio Code launches an in-tool simple browser with the web
    application running.
    <img src="./media/image49.png" style="width:7.09284in;height:2.58404in"
    alt="A screenshot of a computer Description automatically generated" />

4.  In the web application, **create a New Chat** session with at least
    one message.

> <img src="./media/image50.png" style="width:6.5in;height:2.99167in" />

5.  The AI assistant responds with the prebaked string values that you
    observed during the guided tour of the project's code.

> <span class="mark">How do I learn the value of PI?</span>

<img src="./media/image51.png"
style="width:6.49167in;height:2.71667in" />

<img src="./media/image52.png" style="width:6.5in;height:3.25in"
alt="A screenshot of a computer Description automatically generated" />

6.  Close the terminal.

** <span class="mark">Important: </span>**<span class="mark">Closing the
terminal releases the port so you can rebuild and run this application
again later in this project. If you forget to close the terminal, you
may run into issues with the application's port already being in use
when debugging later in the project.</span>

# Exercise 3 - Connect to Azure OpenAI

The OpenAiService class contains a stub implementation of a service that
can send prompts to an AI assistant and parse the responses.

There are a few key requirements to tackle in this exercise:

- Import the .NET SDK for Azure OpenAI

- Add the Azure OpenAI endpoint and key to the application settings

- Modify the service class with various members and a client instance

## Task 1: Import the .NET SDK

The [Azure.AI.OpenAI](https://www.nuget.org/packages/Azure.AI.OpenAI) package
on NuGet provides a typed SDK to access various model deployments from
your account endpoint.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in"
alt="A screenshot of a computer program Description automatically generated" />

2.  Use [dotnet add
    package](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package) to
    import the Azure.AI.OpenAI package from NuGet specifying a
    prerelease version.

> BashCopy
>
> dotnet add package Azure.AI.OpenAI --prerelease

<img src="./media/image53.png" style="width:6.49167in;height:4.475in" />

3.  Build the .NET project again.

> BashCopy
>
> <span class="mark">dotnet build</span>

<img src="./media/image54.png"
style="width:6.49167in;height:6.03333in" />

4.  Close the terminal.

## Task 2: Add application settings

In a .NET application, it's common to use the configuration providers to
inject new settings into your application. For this application, use
the appsettings.Development.json file to provide the most current values
for the Azure OpenAI endpoint and key.

1.  In the root of the project, create a new file
    named **appsettings.Development.json**.

> <img src="./media/image55.png" style="width:4.7in;height:7.96667in" />

** Important**

On Linux, files are case-sensitive. The .NET environment for this
project is named **Development** and the filename must match that
environment name to work.

2.  Within the file, create a new JSON object with a placeholder
    property for OpenAi settings.

> JSONCopy
>
> {
>
> "OpenAi": {
>
> }
>
> }

3.  Within the OpenAi property, create two new properties for
    the Endpoint and Key. Use the Azure OpenAI endpoint and key settings
    you recorded earlier in this lab(Exercise 1\>Task 2).

> JSONCopy
>
> {
>
> "OpenAi": {
>
> "Endpoint": "\<your-azure-openai-endpoint\>",
>
> "Key": "\<your-azure-openai-key\>"
>
> }
>
> }

<img src="./media/image56.png" style="width:6.5in;height:2.66319in" />

** Note:** The key in this example is fictitious.

4.  Save the **appsettings.Development.json** file.

## Task 3: Add required members and a client instance

Finally, implement the class variables required to use the Azure OpenAI
client. At this step, implement a few static prompts and create a new
instance of the OpenAIClient class.

1.  Open the **Services/OpenAiService.cs** file.

> <img src="./media/image57.png" style="width:6.5in;height:6.875in" />

2.  Add using directives for the Azure and Azure.AI.OpenAI namespaces.

> C#Copy
>
> using Azure;
>
> using Azure.AI.OpenAI;

3.  Within the OpenAiService class, add a new variable
    named \_client that's of
    type [OpenAIClient](https://learn.microsoft.com/en-us/dotnet/api/azure.ai.openai.openaiclient).

> C#Copy
>
> <span class="mark">private readonly OpenAIClient \_client;</span>

4.  Create a new string variable named \_systemPromptText with a static
    block of text to send to the AI assistant before each prompt.

> C#Copy
>
> <span class="mark">private readonly string \_systemPrompt = @"</span>
>
> <span class="mark">You are an AI assistant that helps people find
> information.</span>
>
> <span class="mark">Provide concise answers that are polite and
> professional." + Environment.NewLine;</span>

5.  Create another new string variable named \_summarizePrompt with a
    static block of text to send to the AI assistant with instructions
    on how to summarize a conversation.

> C#Copy
>
> <span class="mark">private readonly string \_summarizePrompt =
> @"</span>
>
> <span class="mark">Summarize this prompt in one or two words to use as
> a label in a button on a web page.</span>
>
> <span class="mark">Do not use any punctuation." +
> Environment.NewLine;</span>

6.  Within the constructor of the class, add two extra lines of code to
    check if the endpoint or key is null.
    Use ArgumentNullException.ThrowIfNullOrEmpty to throw an error early
    if either of these values are null.

> C#Copy
>
> <span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(endpoint);</span>
>
> <span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(key);</span>

<span class="mark">**Note:**When you run the application, this will
throw an error right away if either of these settings don't have a valid
value provided through the **appsettings.Development.json** file.</span>

7.  Next, take the model name that is a parameter of the constructor and
    save it to the \_modelName variable.

> C#Copy
>
> <span class="mark">\_modelName = modelName;</span>

8.  Finally, create a new instance of the OpenAIClient class using the
    endpoint to build a Uri and the key to build an AzureKeyCredential.

> C#Copy
>
> <span class="mark">Uri uri = new(endpoint);</span>
>
> <span class="mark">AzureKeyCredential credential = new(key);</span>
>
> <span class="mark">\_client = new(</span>
>
> <span class="mark">endpoint: uri,</span>
>
> <span class="mark">keyCredential: credential</span>
>
> <span class="mark">);</span>

<img src="./media/image58.png"
style="width:7.35757in;height:5.9125in" />

**Reference code**

<span class="mark">using Cosmos.Chat.GPT.Models;</span>

<span class="mark">using Azure;</span>

<span class="mark">using Azure.AI.OpenAI;</span>

<span class="mark">namespace Cosmos.Chat.GPT.Services;</span>

<span class="mark">public class OpenAiService</span>

<span class="mark">{</span>

<span class="mark">private readonly string \_modelName =
String.Empty;</span>

<span class="mark">private readonly OpenAIClient \_client;</span>

<span class="mark">private readonly string \_systemPrompt = @"</span>

<span class="mark">You are an AI assistant that helps people find
information.</span>

<span class="mark">Provide concise answers that are polite and
professional." + Environment.NewLine;</span>

<span class="mark">private readonly string \_summarizePrompt = @"</span>

<span class="mark">Summarize this prompt in one or two words to use as a
label in a button on a web page.</span>

<span class="mark">Do not use any punctuation." +
Environment.NewLine;</span>

<span class="mark">public OpenAiService(string endpoint, string key,
string modelName)</span>

<span class="mark">{</span>

<span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(modelName);</span>

<span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(endpoint);</span>

<span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(key);</span>

<span class="mark">\_modelName = modelName;</span>

<span class="mark">Uri uri = new(endpoint);</span>

<span class="mark">AzureKeyCredential credential = new(key);</span>

<span class="mark">\_client = new(</span>

<span class="mark">endpoint: uri,</span>

<span class="mark">keyCredential: credential</span>

<span class="mark">);</span>

9.  Save the **Services/OpenAiService.cs** file.

<img src="./media/image59.png"
style="width:7.02499in;height:5.10417in" />

## Task 4: Build the project

At this point, your constructor should include enough logic to create a
client instance. Since the class doesn't do anything with the client
yet, there's no point in running the web application, but there's value
in building the application to make sure your code doesn't have any
omissions or errors.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in"
alt="A screenshot of a computer program Description automatically generated" />

2.  Build the .NET project.

> BashCopy
>
> <span class="mark">dotnet build</span>

<img src="./media/image60.png"
style="width:6.49167in;height:3.83333in" />

3.  Observe the build output and check to make sure there aren't any
    build errors.

4.  Close the terminal.

# Exercise 4- Implement the Azure OpenAI service

Let's start with the simplest service to implement, OpenAiService. This
service only contains two methods that we need to implement so we can
implement basic prompts and completions right away. We're not
implementing our Azure Cosmos DB for NoSQL data service until later, so
we can't persist our sessions across debugging sessions yet.

In this exercise, we have a few key requirements:

- Send a question from the user to the AI assistant and ask for a
  response.

- Send a series of prompts to the AI assistant and ask for a
  summarization of the conversation.

## Task 1: Ask the AI model a question

First, implement a question-answer conversation by sending a system
prompt, a question, and session ID so the AI model can provide an answer
in the context of the current conversation. Make sure you measure the
number of tokens it takes to parse the prompt and return a response (or
completion in this context).

1.  Open the **Services/OpenAiService.cs** file.

2.  Within the GetChatCompletionAsync method, remove any existing
    placeholder code:

> C#Copy
>
> public async Task\<(string completionText, int completionTokens)\>
> GetChatCompletionAsync(string sessionId, string userPrompt)
>
> <span class="mark">{</span>
>
> <span class="mark">}</span>

3.  Create a new variable named options of type ChatCompletionsOptions.
    Add the two message variables to the Messages list, set the value
    of User to the sessionId constructor parameter,
    set MaxTokens to 4000, and set the remaining properties to the
    recommended values here.

> C#Copy
>
> ChatCompletionsOptions options = new()
>
> {
>
> DeploymentName = "chatmodel",
>
> Messages = {
>
> new ChatRequestSystemMessage(\_systemPrompt),
>
> new ChatRequestUserMessage(userPrompt)
>
> },
>
> User = sessionId,
>
> MaxTokens = 4000,
>
> Temperature = 0.3f,
>
> NucleusSamplingFactor = 0.5f,
>
> FrequencyPenalty = 0,
>
> PresencePenalty = 0
>
> };

**Note: 4096** is the maximum number of tokens for
the **gpt-35-turbo** model. We're just rounding down here to simplify
things.

4.  Asynchronously invoke the GetChatCompletionsAsync method of the
    Azure OpenAI client variable (\_client). Pass in the name of the
    model (\_modelName) and the options variable you created. Store the
    result in a variable named completions of type ChatCompletions.

C#Copy

<span class="mark">Response\<ChatCompletions\> completionsResponse =
await_client.GetChatCompletionsAsync(options);</span>

<span class="mark">ChatCompletions completions =
completionsResponse.Value;</span>

** Note:** The GetChatCompletionsAsync method returns an object of
type Task\<Response\<ChatCompletions\>\>. The Response\<T\> class
contains a implicit conversion to type T allowing you to select a type
based on your application's needs. You can store the result as
either Response\<ChatCompletions\> to get the full metadata from the
response or just ChatCompletions if you only care about the content of
the result itself.

5.  Finally, return a tuple as the result of
    the GetChatCompletionAsync method with the content of the completion
    as a string, the number of tokens associated with the prompt, and
    the number of tokens for the response.

> C#Copy

return (

completionText: completions.Choices\[0\].Message.Content,

completionTokens: completions.Usage.CompletionTokens

);

<img src="./media/image61.png" style="width:6.49167in;height:5.075in" />

## Task 2: Ask the AI model to summarize a conversation

Now, send the AI model a different system prompt, your current
conversation, and session ID so the AI model can summarize the
conversation in a couple of words.

1.  Within the SummarizeAsync method, remove any existing placeholder
    code:

> C#Copy
>
> public async Task\<string\> SummarizeAsync(string sessionId, string
> conversationText)
>
> {
>
> }

2.  Create a ChatCompletionsOptions variable named options with the two
    message variables in the Messages list, User set to
    the sessionId constructor parameter, MaxTokens set to 200, and the
    remaining properties to the recommended values here:

> C#Copy
>
> <span class="mark">ChatCompletionsOptions options = new()</span>
>
> <span class="mark">{</span>
>
> <span class="mark">DeploymentName = "chatmodel",</span>
>
> <span class="mark">Messages = {</span>
>
> <span class="mark">new
> ChatRequestSystemMessage(\_systemPrompt),</span>
>
> <span class="mark">new ChatRequestUserMessage(conversationText)</span>
>
> <span class="mark">},</span>
>
> <span class="mark">User = sessionId,</span>
>
> <span class="mark">MaxTokens = 200,</span>
>
> <span class="mark">Temperature = 0.0f,</span>
>
> <span class="mark">NucleusSamplingFactor = 1.0f,</span>
>
> <span class="mark">FrequencyPenalty = 0,</span>
>
> <span class="mark">PresencePenalty = 0</span>
>
> <span class="mark">};</span>

3.  Invoke \_client.GetChatCompletionsAsync asynchronously with the
    model name (\_modelName) and the options variable as parameters.
    Store the result in a variable named completions of
    type ChatCompletions.

> C#Copy

<span class="mark">Response\<ChatCompletions\> completionsResponse =
await \_client.GetChatCompletionsAsync(options);</span>

<span class="mark">ChatCompletions completions =
completionsResponse.Value;</span>

4.  Return the content of the completion as a string as the result of
    the SummarizeAsync method.

> C#Copy

<span class="mark">string completionText =
completions.Choices\[0\].Message.Content;</span>

<span class="mark">return completionText;</span>

<img src="./media/image62.png"
style="width:7.34806in;height:5.59583in" />

**Note: Reference code**

<span class="mark">public async Task\<(string completionText, int
completionTokens)\> GetChatCompletionAsync(string sessionId, string
userPrompt)</span>

<span class="mark">{</span>

<span class="mark"></span>

<span class="mark">// ChatRequestSystemMessage systemMessage =
new(ChatRole.System, \_systemPrompt);</span>

<span class="mark">// ChatRequestUserMessage userMessage =
new(ChatRole.User, userPrompt);</span>

<span class="mark">ChatCompletionsOptions options = new()</span>

<span class="mark">{</span>

<span class="mark">DeploymentName = "chatmodel",</span>

<span class="mark">Messages = {</span>

<span class="mark">new ChatRequestSystemMessage(\_systemPrompt),</span>

<span class="mark">new ChatRequestUserMessage(userPrompt)</span>

<span class="mark">},</span>

<span class="mark">User = sessionId,</span>

<span class="mark">MaxTokens = 4000,</span>

<span class="mark">Temperature = 0.3f,</span>

<span class="mark">NucleusSamplingFactor = 0.5f,</span>

<span class="mark">FrequencyPenalty = 0,</span>

<span class="mark">PresencePenalty = 0</span>

<span class="mark">};</span>

<span class="mark">Response\<ChatCompletions\> completionsResponse =
await \_client.GetChatCompletionsAsync(options);</span>

<span class="mark">ChatCompletions completions =
completionsResponse.Value;</span>

<span class="mark">return (</span>

<span class="mark">completionText:
completions.Choices\[0\].Message.Content,</span>

<span class="mark">completionTokens:
completions.Usage.CompletionTokens</span>

<span class="mark">);</span>

<span class="mark">}</span>

<span class="mark">public async Task\<string\> SummarizeAsync(string
sessionId, string conversationText)</span>

<span class="mark">{</span>

<span class="mark">// ChatMessage systemMessage = new (ChatRole.System,
\_summarizePrompt);</span>

<span class="mark">// ChatMessage userMessage = new (ChatRole.User,
conversationText);</span>

<span class="mark">ChatCompletionsOptions options = new()</span>

<span class="mark">{</span>

<span class="mark">DeploymentName = "chatmodel",</span>

<span class="mark">Messages = {</span>

<span class="mark">new ChatRequestSystemMessage(\_systemPrompt),</span>

<span class="mark">new ChatRequestUserMessage(conversationText)</span>

<span class="mark">},</span>

<span class="mark">User = sessionId,</span>

<span class="mark">MaxTokens = 200,</span>

<span class="mark">Temperature = 0.0f,</span>

<span class="mark">NucleusSamplingFactor = 1.0f,</span>

<span class="mark">FrequencyPenalty = 0,</span>

<span class="mark">PresencePenalty = 0</span>

<span class="mark">};</span>

<span class="mark">Response\<ChatCompletions\> completionsResponse =
await \_client.GetChatCompletionsAsync(options);</span>

<span class="mark">ChatCompletions completions =
completionsResponse.Value;</span>

<span class="mark">string completionText =
completions.Choices\[0\].Message.Content;</span>

<span class="mark">return completionText;</span>

<span class="mark">}</span>

<span class="mark">}</span>

5.  Save the **Services/OpenAiService.cs** file.

## Task 3:Build the project

At this point, your application should have a thorough enough
implementation of the Azure OpenAI service that you can test the
application. Remember, you haven't implemented a data store yet, so your
conversations aren't persisted between debugging sessions.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in" />

2.  Build the .NET project.

> BashCopy
>
> <span class="mark">dotnet build</span>

<img src="./media/image63.png" style="width:6.5in;height:4.58333in" />

3.  Start the application with hot reloads enabled using dotnet watch.

> BashCopy
>
> <span class="mark">dotnet watch run --non-interactive</span>

<img src="./media/image64.png"
style="width:7.2528in;height:4.80417in" />

4.  Visual Studio Code launches the in-tool simple browser again with
    the web application running. In the web application, create a new
    chat session and ask the AI assistant a question. The AI assistant
    now responds with a completion created by the model. You should also
    notice that the *token* UI fields are now populated with real-world
    token usage for each completion and prompt.

<!-- -->

3.  On the web application click on the **Create New Chat** button.

<img src="./media/image65.png"
style="width:6.49167in;height:3.86667in" />

4.  Paste the following text in the text box and click on the **Send**
    icon.

**CodeCopy**

**How large microsoft's campus?**

<img src="./media/image66.png" style="width:6.49167in;height:4.75in" />

<img src="./media/image67.png" style="width:6.5in;height:4.83333in" />

<img src="./media/image68.png" style="width:6.5in;height:6.38333in" />

5.  To stop the port Press **ctrl+c** and close the terminal.

**Note:** The **Hot Reload** feature is enabled here if you need to make
a small correction to the application's code. For more information,
see [**.NET Hot Reload support for ASP.NET
Core**](https://learn.microsoft.com/en-us/aspnet/core/test/hot-reload).

# Exercise 5- Connect to Azure Cosmos DB for NoSQL

The CosmosDbService class contains a stub implementation of a service
similar to the OpenAiService class you worked on previously in this
module. In contrast, this class uses the .NET SDK for Azure Cosmos DB,
which works slightly different.

There are a few key requirements to tackle in this exercise:

- Import the .NET SDK for Azure Cosmos DB for NoSQL

- Add the Azure Cosmos DB for NoSQL endpoint and key to the application
  settings

- Modify the service class with various members and a client instance

## Task 1: Import the .NET SDK

The [Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos) NuGet
package is a typed library that simplifies the process of accessing
Azure Cosmos DB for NoSQL from a .NET application.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in"
alt="A screenshot of a computer program Description automatically generated" />

2.  Import the Microsoft.Azure.Cosmos package from NuGet with dotnet add
    package.

> BashCopy
>
> dotnet add package Microsoft.Azure.Cosmos

<img src="./media/image69.png"
style="width:6.49167in;height:3.90833in" />

3.  Build the .NET project one more time.

> BashCopy
>
> <span class="mark">dotnet build</span>

<img src="./media/image70.png" style="width:6.5in;height:5.93333in" />

4.  Close the terminal.

## Task 2: Add application settings

Use the appsettings.Development.json file again to provide current
values for the Azure Cosmos DB for NoSQL endpoint and key.

1.  Open the **appsettings.Development.json** file.

2.  Within the file, create another new JSON object with a placeholder
    property for CosmosDb settings.

3.  Within the CosmosDb property, create two new properties for
    the Endpoint and Key. Use the Azure Cosmos DB endpoint and key
    settings you recorded earlier in this lab.

> JSONCopy
>
> {
>
> "OpenAi": {
>
> "Endpoint": "\<your-azure-openai-endpoint\>",
>
> "Key": "\<your-azure-openai-key\>"
>
> },
>
> "CosmosDb": {
>
> "Endpoint": "\<your-azure-cosmos-db-endpoint\>",
>
> "Key": "\<your-azure-cosmos-db-key\>"
>
> }
>
> }

<img src="./media/image71.png"
style="width:5.86667in;height:3.83333in" />

** Note:** The key in this example is fictitious.

4.  Save the **appsettings.Development.json** file.

## Task 3: Add required members and a client instance

Finally, implement the class variables and client required to access
Azure Cosmos DB for NoSQL using the client. For this step, use the SDK's
client classes to implement an instance of type Container in
the CosmosDbService class.

1.  Open the **Services/CosmosDbService.cs** file.

> <img src="./media/image72.png" style="width:6.49167in;height:4.475in" />

2.  Add using directives for the following namespaces.

    - Microsoft.Azure.Cosmos

    <!-- -->

    - Microsoft.Azure.Cosmos.Fluent

> C#Copy
>
> <span class="mark">using Microsoft.Azure.Cosmos;</span>
>
> <span class="mark">using Microsoft.Azure.Cosmos.Fluent;</span>

3.  Within the CosmosDbService class, add a new Container-typed variable
    named \_container.

> C#Copy
>
> <span class="mark">private readonly Container \_container;</span>

4.  Within the constructor,
    add ArgumentNullException.ThrowIfNullOrEmpty checks to throw an
    error if either the endpoint or key parameters are null.

> C#Copy
>
> <span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(endpoint);</span>
>
> <span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(key);</span>

5.  Now, create a variable named options of
    type [CosmosSerializationOptions](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.cosmosserializationoptions).
    Set the PropertyNamingPolicy property of the variable
    to CosmosPropertyNamingPolicy.CamelCase.

> C#Copy
>
> <span class="mark">CosmosSerializationOptions options = new()</span>
>
> <span class="mark">{</span>
>
> <span class="mark">PropertyNamingPolicy =
> CosmosPropertyNamingPolicy.CamelCase</span>
>
> <span class="mark">};</span>

** **

**Note:** Setting this property will ensure that the JSON produced by
the SDK is both serialized and deserialized in *camel case* regardless
of how it's corresponding property is cased in the .NET class.

6.  Create a new instance of
    type [CosmosClient](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) named client using
    the [CosmosClientBuilder](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.fluent.cosmosclientbuilder) class,
    endpoint, key, and serialization options you specified earlier.

> C#Copy
>
> <span class="mark">CosmosClient client = new
> CosmosClientBuilder(endpoint, key)</span>
>
> <span class="mark">.WithSerializerOptions(options)</span>
>
> <span class="mark">.Build();</span>

7.  Create a new nullable variable of type Database named database by
    calling the GetDatabase method of the client variable.

> C#Copy
>
> <span class="mark">Database? database =
> client?.GetDatabase(databaseName);</span>

8.  Create another nullable variable named container of
    type Container by calling the GetContainer method of the database
    variable.

> C#Copy
>
> <span class="mark">Container? container =
> database?.GetContainer(containerName);</span>

9.  Finally, assign the constructor's container variable to the
    class' \_container variable only if it's not null. If it's null,
    throw an ArgumentException.

> C#Copy
>
> <span class="mark">\_container = container ??</span>
>
> <span class="mark">throw new ArgumentException("Unable to connect to
> existing Azure Cosmos DB container or database.");</span>

<img src="./media/image73.png"
style="width:7.33973in;height:5.0125in" />

10. Save the **Services/CosmosDbService.cs** file.

## Task 4: Check your work

At this point, your constructor should include enough logic to create a
container instance that the rest of the service uses. Since the class
doesn't do anything with the container yet, there's no point in running
the web application, but there's value in building the application to
make sure your code doesn't have any omissions or errors.

1.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in" />

2.  Build the .NET project.

> BashCopy
>
> <span class="mark">dotnet build</span>

<img src="./media/image74.png"
style="width:6.49167in;height:5.44167in" />

3.  Observe the build output and check to make sure there aren't any
    build errors.

4.  Close the terminal.

# Exercise 6- Implement the Azure Cosmos DB for NoSQL service

The Azure Cosmos DB service (CosmosDbService) manages querying,
creating, deleting, and updating sessions and messages in your AI
assistant application. To manage all of these operations, the service is
required to implement multiple methods for each potential operation
using various features of the .NET SDK.

There are multiple key requirements to tackle in this exercise:

- Implement operations to create a session or message

- Implement queries to retrieve multiple sessions or messages

- Implement an operation to update a single session or batch update
  multiple messages

- Implement an operation to query and delete multiple related sessions
  and messages

## Task 1: Create a session or message

Azure Cosmos DB for NoSQL stores data in JSON format allowing us to
store many types of data in a single container. This application stores
both a chat *"session"* with the AI assistant and the
individual *"messages"* within each session. With the API for NoSQL, the
application can store both types of data in the same container and then
differentiate between these types using a simple type field.

1.  Open the **Services/CosmosDbService.cs** file.

2.  Within the InsertSessionAsync method, remove any existing
    placeholder code:

> C#Copy
>
> <span class="mark">public async Task\<Session\>
> InsertSessionAsync(Session session)</span>
>
> <span class="mark">{</span>
>
> <span class="mark">}</span>

3.  Create a new variable named partitionKey of
    type [PartitionKey](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.partitionkey) using
    the current session's SessionId property as the parameter.

> C#Copy
>
> <span class="mark">PartitionKey partitionKey =
> new(session.SessionId);</span>

4.  Invoke the CreateItemAsync method of the container passing in
    the session parameter and partitionKey variable. Return the response
    as the result of the InsertSessionAsync method.

> C#Copy
>
> <span class="mark">return await
> \_container.CreateItemAsync\<Session\>(</span>
>
> <span class="mark">item: session,</span>
>
> <span class="mark">partitionKey: partitionKey</span>
>
> <span class="mark">);</span>

5.  Within the InsertMessageAsync method, remove any existing
    placeholder code:

> public async Task\<Message\> InsertMessageAsync(Message message)
>
> {
>
> }

6.  Create a PartitionKey variable using session.SessionId as the value
    of the partition key.

> C#Copy
>
> <span class="mark">PartitionKey partitionKey =
> new(message.SessionId);</span>

7.  Create a new message variable named newMessage with
    the Timestamp property updated to the current UTC timestamp.

> C#Copy
>
> <span class="mark">Message newMessage = message with { TimeStamp =
> DateTime.UtcNow };</span>

8.  Invoke CreateItemAsync passing in both the new message and partition
    key variables. Return the response as the result
    of InsertMessageAsync.

> C#Copy
>
> <span class="mark">return await
> \_container.CreateItemAsync\<Message\>(</span>
>
> <span class="mark">item: newMessage,</span>
>
> <span class="mark">partitionKey: partitionKey</span>
>
> <span class="mark">);</span>

<img src="./media/image75.png" style="width:6.5in;height:4.875in" />

9.  Save the **Services/CosmosDbService.cs** file.

## Task 2: Retrieve multiple sessions or messages

There are two main use cases where the application needs to retrieve
multiple items from our container. First, the application retrieves all
sessions for the current user by filtering the items to ones where type
= Session. Second, the application retrieves all messages for a session
by performing a similar filter where type = Session & sessionId =
\<current-session-id\>. Implement both queries here using the .NET SDK
and a feed iterator.

1.  Within the GetSessionsAsync method, remove any existing placeholder
    code:

> <span class="mark">public async Task\<List\<Session\>\>
> GetSessionsAsync()</span>
>
> <span class="mark">{</span>
>
> <span class="mark">}</span>

2.  Create a new variable named query of
    type [QueryDefinition](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.querydefinition) with
    the SQL query SELECT DISTINCT \* FROM c WHERE c.type = @type. Use
    the fluent WithParameter method to assign the name of
    the Session class as the value for the parameter.

> C#Copy
>
> <span class="mark">QueryDefinition query = new QueryDefinition("SELECT
> DISTINCT \* FROM c WHERE c.type = @type")</span>
>
> <span class="mark">.WithParameter("@type", nameof(Session));</span>

3.  Invoke the generic GetItemQueryIterator\<\> method on
    the \_container variable passing in the generic type Session and
    the query variable as a parameter. Store the result in a variable of
    type FeedIterator\<Session\> named response.

> C#Copy
>
> <span class="mark">FeedIterator\<Session\> response =
> \_container.GetItemQueryIterator\<Session\>(query);</span>

4.  Create a new generic list variable named output.

> C#Copy
>
> <span class="mark">List\<Session\> output = new();</span>

5.  Create a *while loop* that runs until response.HasMoreResults is no
    longer true.

> C#Copy
>
> <span class="mark">while (response.HasMoreResults)</span>
>
> <span class="mark">{</span>
>
> <span class="mark">}</span>

** Note:** Using a while loop here will effectively loop through all
pages of your response until there are no pages left.

6.  Within the while loop, asynchronously get the next page of results
    by invoking ReadNextAsync on the response variable and then add
    those results to the list variable named output.

> C#Copy
>
> <span class="mark">FeedResponse\<Session\> results = await
> response.ReadNextAsync();</span>
>
> <span class="mark">output.AddRange(results);</span>

7.  Outside the while loop, return the output variable with a list of
    sessions as the result of the GetSessionsAsync method.

> C#Copy
>
> <span class="mark">return output;</span>

8.  Within the GetSessionMessagesAsync method, remove any existing
    placeholder code:

> C#Copy
>
> <span class="mark">public async Task\<List\<Message\>\>
> GetSessionMessagesAsync(string sessionId)</span>
>
> <span class="mark">{</span>
>
> <span class="mark">}</span>

9.  Create a query variable of type QueryDefinition. Use the SQL
    query SELECT \* FROM c WHERE c.sessionId = @sessionId AND c.type
    = @type. Use the fluent WithParameter method to assign
    the @sessionId parameter to the session identifier passed in as a
    parameter, and the @type parameter to the name of the Message class.

> C#Copy
>
> QueryDefinition query = new QueryDefinition("SELECT \* FROM c WHERE
> c.sessionId = @sessionId AND c.type = @type")
>
> .WithParameter("@sessionId", sessionId)
>
> .WithParameter("@type", nameof(Message));

10. Create a FeedIterator\<Message\> using the query variable and
    the GetItemQueryIterator\<\> method.

> C#Copy
>
> <span class="mark">FeedIterator\<Message\> response =
> \_container.GetItemQueryIterator\<Message\>(query);</span>

11. Use a *while loop* to iterate through all pages of results and store
    the results in a single List\<Message\> variable named output.

> C#Copy
>
> <span class="mark">List\<Message\> output = new();</span>
>
> <span class="mark">while (response.HasMoreResults)</span>
>
> <span class="mark">{</span>
>
> <span class="mark">FeedResponse\<Message\> results = await
> response.ReadNextAsync();</span>
>
> <span class="mark">output.AddRange(results);</span>
>
> <span class="mark">}</span>

12. Return the output variable as the result of
    the GetSessionMessagesAsync method.

> C#Copy
>
> <span class="mark">return output;</span>

<img src="./media/image76.png"
style="width:6.49167in;height:4.71667in" />

13. Save the **Services/CosmosDbService.cs** file.

## Task 3: Update one or more sessions or messages

There are scenarios when either a single session requires an update or
more than one message requires an update. For the first scenario, use
the ReplaceItemAsync method of the SDK to replace an existing item with
a modified version. For the second scenario, use the transactional batch
capability of the SDK to modify multiple messages in a single batch.

1.  Within the UpdateSessionAsync method, remove any existing
    placeholder code:

> <span class="mark">public async Task\<Session\>
> UpdateSessionAsync(Session session)</span>
>
> <span class="mark">{</span>
>
> <span class="mark">}</span>

2.  Create a PartitionKey variable using session.SessionId as the value
    of the partition key.

> C#Copy
>
> <span class="mark">PartitionKey partitionKey =
> new(session.SessionId);</span>

3.  Invoke ReplaceItemAsync passing in the new message, message's unique
    identifier and partition key. Return the response as the result
    of UpdateSessionAsync.

> C#Copy
>
> <span class="mark">return await \_container.ReplaceItemAsync(</span>
>
> <span class="mark">item: session,</span>
>
> <span class="mark">id: session.Id,</span>
>
> <span class="mark">partitionKey: partitionKey</span>
>
> <span class="mark">);</span>

4.  Within the UpsertSessionBatchAsync method, remove any existing
    placeholder code:

> <span class="mark">public async Task UpsertSessionBatchAsync(params
> dynamic\[\] messages)</span>
>
> <span class="mark">{</span>
>
> <span class="mark">}</span>

5.  Use language-integrated query (LINQ) to validate that all messages
    contain a single session identifier (SessionId). If any of the
    messages contain a different value, throw an ArgumentException.

> C#Copy
>
> <span class="mark">if (messages.Select(m =\>
> m.SessionId).Distinct().Count() \> 1)</span>
>
> <span class="mark">{</span>
>
> <span class="mark">throw new ArgumentException("All items must have
> the same partition key.");</span>
>
> <span class="mark">}</span>

6.  Create a new PartitionKey variable using the SessionId property of
    the first message.

> C#Copy
>
> <span class="mark">PartitionKey partitionKey =
> new(messages.First().SessionId);</span>

** Note:** Remember, you can safely assume that all messages have the
same session identifier if the application has moved to this point in
the method's code.

7.  Create a new variable named batch of
    type [TransactionalBatch](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cosmos.transactionalbatch) by
    invoking the CreateTransactionalBatch method of
    the \_container variable. Pass in the current partition key variable
    as the partition key to use for the batch operations.

> C#Copy
>
> <span class="mark">TransactionalBatch batch =
> \_container.CreateTransactionalBatch(partitionKey);</span>
>
> ** **

8.  Iterate over each message in the messages array using a *foreach
    loop*.

> C#Copy
>
> foreach (var message in messages)
>
> {
>
> }

9.  Within the foreach loop, add each message as an **upsert** operation
    to the batch.

> C#Copy
>
> batch.UpsertItem(
>
> item: message
>
> );

** Note: Upsert** tells Azure Cosmos DB to determine, server-side,
whether an item should be replaced or updated. Azure Cosmos DB will make
this determination with the id and partition key of each item.

10. Outside of the foreach loop, asynchronously invoke
    the ExecuteAsync method of the batch to execute all operations
    within the batch.

> C#Copy
>
> <span class="mark">await batch.ExecuteAsync();</span>

<img src="./media/image77.png" style="width:6.5in;height:5.45833in" />

11. Save the **Services/CosmosDbService.cs** file.

## Task 4: Remove a session and all related messages

Finally, combine the query and transactional batch functionality to
remove multiple items. In this example, get the session item and all
related messages by querying for all items with a specific session
identifier regardless of type. Then, create a transactional batch to
delete all matched items as a single transaction.

1.  Within the DeleteSessionAndMessagesAsync method, remove any existing
    placeholder code:

> C#Copy
>
> public async Task DeleteSessionAndMessagesAsync(string sessionId)
>
> {
>
> }

2.  Create a variable named partitionKey of type PartitionKey using
    the sesionId string value passed in as a parameter to this method.

> C#Copy
>
> PartitionKey partitionKey = new(sessionId);

3.  Using the same sessionId method parameter, build
    a QueryDefinition object that finds all items that match the session
    identifier. Use a query parameter for the sessionId and ensure that
    you don't filter the query on the type of item.

> C#Copy
>
> QueryDefinition query = new QueryDefinition("SELECT VALUE c.id FROM c
> WHERE c.sessionId = @sessionId")
>
> .WithParameter("@sessionId", sessionId);

** Note:** If you apply a type filter in this query, you may
inadvertently miss related messages or sessions that should be bulk
removed as part of this operation.

4.  Create a new FeedIterator\<string\> using GetItemQueryIterator and
    the query you built.

> C#Copy
>
> FeedIterator\<string\> response =
> \_container.GetItemQueryIterator\<string\>(query);

1.  Create
    a TransactionalBatch named batch using CreateTransactionalBatch and
    the partition key variable.

> C#Copy
>
> TransactionalBatch batch =
> \_container.CreateTransactionalBatch(partitionKey);

2.  Create a *while loop* to iterate through all pages of results.
    Within the while loop, get the next page of results and use
    a *foreach loop* to iterate through all item identifiers per page.
    Within the foreach loop, add a batch operation to delete the item
    using batch.DeleteItem.

> C#Copy
>
> while (response.HasMoreResults)
>
> {
>
> FeedResponse\<string\> results = await response.ReadNextAsync();
>
> foreach (var itemId in results)
>
> {
>
> batch.DeleteItem(
>
> id: itemId
>
> );
>
> }
>
> }

3.  After the while loop, execute the batch using batch.ExecuteAsync.

> C#Copy
>
> await batch.ExecuteAsync();

<img src="./media/image78.png"
style="width:6.49167in;height:5.10833in" />

4.  Save the **Services/CosmosDbService.cs** file.

## Note: Reference code

<span class="mark">using Cosmos.Chat.GPT.Models;</span>

<span class="mark">using Microsoft.Azure.Cosmos;</span>

<span class="mark">using Microsoft.Azure.Cosmos.Fluent;</span>

<span class="mark">namespace Cosmos.Chat.GPT.Services;</span>

<span class="mark">public class CosmosDbService</span>

<span class="mark">{</span>

<span class="mark">private readonly Container \_container;</span>

<span class="mark">public CosmosDbService(string endpoint, string key,
string databaseName, string containerName)</span>

<span class="mark">{</span>

<span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(databaseName);</span>

<span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(containerName);</span>

<span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(endpoint);</span>

<span class="mark">ArgumentNullException.ThrowIfNullOrEmpty(key);</span>

<span class="mark">CosmosSerializationOptions options = new()</span>

<span class="mark">{</span>

<span class="mark">PropertyNamingPolicy =
CosmosPropertyNamingPolicy.CamelCase</span>

<span class="mark">};</span>

<span class="mark">CosmosClient client = new
CosmosClientBuilder(endpoint, key)</span>

<span class="mark">.WithSerializerOptions(options)</span>

<span class="mark">.Build();</span>

<span class="mark">Database? database =
client?.GetDatabase(databaseName);</span>

<span class="mark">Container? container =
database?.GetContainer(containerName);</span>

<span class="mark">\_container = container ??</span>

<span class="mark">throw new ArgumentException("Unable to connect to
existing Azure Cosmos DB container or database.");</span>

<span class="mark">}</span>

<span class="mark">public async Task\<Session\>
InsertSessionAsync(Session session)</span>

<span class="mark">{</span>

<span class="mark">PartitionKey partitionKey =
new(session.SessionId);</span>

<span class="mark">return await
\_container.CreateItemAsync\<Session\>(</span>

<span class="mark">item: session,</span>

<span class="mark">partitionKey: partitionKey</span>

<span class="mark">);</span>

<span class="mark">}</span>

<span class="mark">public async Task\<Message\>
InsertMessageAsync(Message message)</span>

<span class="mark">{</span>

<span class="mark">PartitionKey partitionKey =
new(message.SessionId);</span>

<span class="mark">Message newMessage = message with { TimeStamp =
DateTime.UtcNow };</span>

<span class="mark">return await
\_container.CreateItemAsync\<Message\>(</span>

<span class="mark">item: newMessage,</span>

<span class="mark">partitionKey: partitionKey</span>

<span class="mark">);</span>

<span class="mark">}</span>

<span class="mark">public async Task\<List\<Session\>\>
GetSessionsAsync()</span>

<span class="mark">{</span>

<span class="mark">QueryDefinition query = new QueryDefinition("SELECT
DISTINCT \* FROM c WHERE c.type = @type")</span>

<span class="mark">.WithParameter("@type", nameof(Session));</span>

<span class="mark">FeedIterator\<Session\> response =
\_container.GetItemQueryIterator\<Session\>(query);</span>

<span class="mark">List\<Session\> output = new();</span>

<span class="mark">while (response.HasMoreResults)</span>

<span class="mark">{</span>

<span class="mark">FeedResponse\<Session\> results = await
response.ReadNextAsync();</span>

<span class="mark">output.AddRange(results);</span>

<span class="mark">}</span>

<span class="mark">return output;</span>

<span class="mark">}</span>

<span class="mark">public async Task\<List\<Message\>\>
GetSessionMessagesAsync(string sessionId)</span>

<span class="mark">{</span>

<span class="mark">QueryDefinition query = new QueryDefinition("SELECT
\* FROM c WHERE c.sessionId = @sessionId AND c.type = @type")</span>

<span class="mark">.WithParameter("@sessionId", sessionId)</span>

<span class="mark">.WithParameter("@type", nameof(Message));</span>

<span class="mark">FeedIterator\<Message\> response =
\_container.GetItemQueryIterator\<Message\>(query);</span>

<span class="mark">List\<Message\> output = new();</span>

<span class="mark">while (response.HasMoreResults)</span>

<span class="mark">{</span>

<span class="mark">FeedResponse\<Message\> results = await
response.ReadNextAsync();</span>

<span class="mark">output.AddRange(results);</span>

<span class="mark">}</span>

<span class="mark">return output;</span>

<span class="mark">}</span>

<span class="mark">public async Task\<Session\>
UpdateSessionAsync(Session session)</span>

<span class="mark">{</span>

<span class="mark">PartitionKey partitionKey =
new(session.SessionId);</span>

<span class="mark">return await \_container.ReplaceItemAsync(</span>

<span class="mark">item: session,</span>

<span class="mark">id: session.Id,</span>

<span class="mark">partitionKey: partitionKey</span>

<span class="mark">);</span>

<span class="mark">}</span>

<span class="mark">public async Task UpsertSessionBatchAsync(params
dynamic\[\] messages)</span>

<span class="mark">{</span>

<span class="mark">if (messages.Select(m =\>
m.SessionId).Distinct().Count() \> 1)</span>

<span class="mark">{</span>

<span class="mark">throw new ArgumentException("All items must have the
same partition key.");</span>

<span class="mark">}</span>

<span class="mark">PartitionKey partitionKey =
new(messages.First().SessionId);</span>

<span class="mark">TransactionalBatch batch =
\_container.CreateTransactionalBatch(partitionKey);</span>

<span class="mark">foreach (var message in messages)</span>

<span class="mark">{</span>

<span class="mark">batch.UpsertItem(</span>

<span class="mark">item: message</span>

<span class="mark">);</span>

<span class="mark">}</span>

<span class="mark">await batch.ExecuteAsync();</span>

<span class="mark">}</span>

<span class="mark">public async Task
DeleteSessionAndMessagesAsync(string sessionId)</span>

<span class="mark">{</span>

<span class="mark">PartitionKey partitionKey = new(sessionId);</span>

<span class="mark">QueryDefinition query = new QueryDefinition("SELECT
VALUE c.id FROM c WHERE c.sessionId = @sessionId")</span>

<span class="mark">.WithParameter("@sessionId", sessionId);</span>

<span class="mark">FeedIterator\<string\> response =
\_container.GetItemQueryIterator\<string\>(query);</span>

<span class="mark">TransactionalBatch batch =
\_container.CreateTransactionalBatch(partitionKey);</span>

<span class="mark">while (response.HasMoreResults)</span>

<span class="mark">{</span>

<span class="mark">FeedResponse\<string\> results = await
response.ReadNextAsync();</span>

<span class="mark">foreach (var itemId in results)</span>

<span class="mark">{</span>

<span class="mark">batch.DeleteItem(</span>

<span class="mark">id: itemId</span>

<span class="mark">);</span>

<span class="mark">}</span>

<span class="mark">}</span>

<span class="mark">await batch.ExecuteAsync();</span>

<span class="mark">}</span>

<span class="mark">}</span>

## Task 5: Check your work

Now your application has a full implementation of Azure OpenAI and Azure
Cosmos DB. You can test the application end-to-end by debugging the
solution.

5.  In the **Visual Studio Code** editor, click on **Terminal**, open a
    **New Terminal**.

<img src="./media/image26.png" style="width:6.5in;height:4.66667in"
alt="A screenshot of a computer program Description automatically generated" />

6.  Build the .NET project.

> BashCopy
>
> <span class="mark">dotnet build</span>

<img src="./media/image79.png" style="width:6.5in;height:3.58194in" />

7.  Start the application with hot reloads enabled using dotnet watch.

> BashCopy
>
> <span class="mark">dotnet watch run --non-interactive</span>

<img src="./media/image80.png"
style="width:6.49167in;height:4.11667in" />

8.  Visual Studio Code launches the in-tool simple browser again with
    the web application running. In the web application, create a new
    chat session and ask the AI assistant a question. Then, close the
    running web application.

<!-- -->

11. Paste the following text in the text box and click on the **Send**
    icon.

**CodeCopy**

**How many wins does it take to promote to the Premier League?**

<img src="./media/image81.png"
style="width:7.37575in;height:4.7375in" />

<img src="./media/image82.png"
style="width:5.87917in;height:3.58486in" />

12. Paste the following text in the text box and click on the **Send**
    icon.

**CodeCopy**

> **<span class="mark">What is Azure OpenAI?</span>**

<img src="./media/image83.png" style="width:6.3375in;height:4.1875in" />

<img src="./media/image84.png"
style="width:6.49167in;height:4.25833in" />

13. Close the terminal. Now, open a new terminal.

14. Start the application one more time with hot reloads enabled
    using dotnet watch.

> BashCopy
>
> <span class="mark">dotnet watch run --non-interactive</span>

15. Visual Studio Code launches the in-tool simple browser yet again
    with the web application running. For this iteration, observe that
    your chat sessions are persisted between debugging sessions.

<img src="./media/image85.png"
style="width:7.35029in;height:4.8625in" />

16. Close the terminal.

## Task 6: Clean up resource group

1.  Open a new browser and enter the following URL in the address bar:
    <https://portal.azure.com/> to open the Azure Portal.

2.  Click on the **Portal Menu**, then select **Resource group.**

<img src="./media/image10.png" style="width:6.49167in;height:3.4in"
alt="A screenshot of a computer Description automatically generated" />

3.  Select the **mslearn-cosmos-openai** resource group.

<img src="./media/image11.png"
style="width:4.93333in;height:4.28333in" />

4.  In the Resource group page, navigate to command bar and click on
    **Delete resource group**.

<img src="./media/image86.png"
style="width:6.49167in;height:3.29167in" />

5.  In the **Delete Resource group** pane that appears on the right
    side, enter the **resource group name** and click on **Delete**
    button.

<img src="./media/image87.png" style="width:5.80884in;height:7.00061in"
alt="A screenshot of a computer Description automatically generated" />

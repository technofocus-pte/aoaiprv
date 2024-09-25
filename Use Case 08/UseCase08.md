# Use case 6-Build a chat bot using Azure OpenAI, Azure Cosmos DB for NoSQL, and Blazor

In this use case, you will connect a Blazor web application to Azure
Cosmos DB for NoSQL and Azure OpenAI using .NET software development
kits. Your code manages and queries items in an API for NoSQL container.
Your code also sends prompts to Azure OpenAI and parses the responses.

**Lab duration:** 45 minutes

**Lab Type:** Instructor led

**Objective**

- To set up the development environment for Blazor, PostgreSQL, and
  OpenAI.

- To create a Blazor project and design a responsive chat interface.

- To configure PostgreSQL database on Azure and connect it to the Blazor
  app.

- To integrate Azure OpenAI for enhanced chat functionalities.

- To deploy the Blazor application and PostgreSQL database on Azure.

- To test the application in order to ensure seamless interaction
  between components.

- To monitor and troubleshoot the deployed application on Azure.

**Key Technologies Used**: Azure Cosmos DB for NoSQL, Azure OpenAI

## **Exercise 1: Deploy the infrastructure and complete the initial setup**

To complete this project, you need an Azure Cosmos DB for NoSQL account
and an Azure OpenAI account. To streamline this process, deploy a Bicep
template to Azure with both of these accounts.

### **Task 1: Deploy infrastructure from template**

1.  Open a new browser and enter the following URL in the address
    bar: +++https://portal.azure.com/+++ to open the Azure Portal.

<img src="./media/image1.jpeg" style="width:6.5in;height:3.24306in"
alt="A screenshot of a computer Description automatically generated" />

2.  In the Azure portal, click on the **\[\>\_\] (Cloud Shell)** button
    at the top of the page to the right of the search box. A Cloud Shell
    pane will open at the bottom of the portal. The first time you open
    the Cloud Shell, you may be prompted to choose the type of shell you
    want to use (**Bash** or **PowerShell**). Select **Bash**. If you
    don't see this option, then skip this step.

<img src="./media/image2.jpeg" style="width:6.5in;height:3.79931in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image3.jpeg" style="width:6.5in;height:3.25in"
alt="A screenshot of a computer Description automatically generated" />

3.  In **You have no storage mounted** dialog box, click on the **Create
    storage.**

<img src="./media/image4.jpeg" style="width:6.5in;height:2.35694in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image5.jpeg" style="width:6.5in;height:2.71528in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image6.jpeg" style="width:6.5in;height:2.49653in"
alt="A close-up of a computer screen Description automatically generated" />

4.  Ensure the type of shell indicated on the top left of the Cloud
    Shell pane is switched to **Bash**. If it's **PowerShell**, switch
    to **Bash** by using the drop-down menu.

<img src="./media/image7.jpeg" style="width:6.5in;height:6.11528in"
alt="A screenshot of a computer Description automatically generated" />

5.  Once the terminal starts, click on **Manage files -\> Upload**.

<img src="./media/image8.jpeg" style="width:6.5in;height:2.01875in"
alt="A screenshot of a computer Description automatically generated" />

6.  Select **azuredeploy.JSON** file from the path **C:\Labfiles\Build
    and Test a custom chat application Using Azure Cosmos DB and
    AzureOpenAI** and select **Open**.

<img src="./media/image9.jpeg" style="width:6.5in;height:4.24167in"
alt="A screenshot of a computer Description automatically generated" />

You should get a success message for the file upload.

<img src="./media/image10.jpeg" style="width:5.55556in;height:1.58333in"
alt="A white background with black text Description automatically generated" />

7.  Create a new shell variable named **resourceGroupName** with the
    name of the Azure resource group that you create
    (mslearn-cosmos-openai).

resourceGroupName="mslearn-cosmos-openai"

<img src="./media/image11.jpeg" style="width:6.5in;height:3.27014in"
alt="A screenshot of a computer Description automatically generated" />

8.  Create a resource group using the **az group create** command. Then,
    execute the following command

az group create --name \$resourceGroupName --location "uksouth"

<img src="./media/image12.jpeg" style="width:6.5in;height:2.49861in"
alt="A screenshot of a computer Description automatically generated" />

9.  Deploy the **azuredeploy.json** template file to the resource group
    using az group deployment create. Then, execute the following
    command.

az deployment group create --resource-group \$resourceGroupName --name
zero-touch-deployment --template-file azuredeploy.json

**Note:** This deployment can take approximately 5-10 minutes.

<img src="./media/image13.jpeg" style="width:6.5in;height:3.55694in"
alt="A screenshot of a computer screen Description automatically generated" />

<img src="./media/image14.jpeg" style="width:6.5in;height:4.21042in"
alt="A screenshot of a computer Description automatically generated" />

### **Task 2: Get Azure Cosmos DB for NoSQL and Azure OpenAI account credentials**

The above deployment has deployed Azure Cosmos DB for NoSQL and Azure
OpenAI accounts and then stored their credentials in the Azure App
Service web app's configuration. Now, you have the choice of using the
Azure portal or Azure CLI to retrieve the credentials for each service.

1.  From the Azure portal Home page, click on **Resource groups.**

<img src="./media/image15.jpeg" style="width:6.5in;height:3.42222in"
alt="A screenshot of a computer Description automatically generated" />

2.  Select the **mslearn-cosmos-openai** resource group.

<img src="./media/image16.jpeg" style="width:6.5in;height:5.65208in"
alt="A screenshot of a computer Description automatically generated" />

3.  On the **Resource Groups** page, expand the **Essentials** panel and
    observe the **Deployments** header. The status for the deployment
    should be **Succeeded** at this point.

<img src="./media/image17.jpeg" style="width:6.5in;height:2.25694in"
alt="A screenshot of a computer Description automatically generated" />

4.  Now, select the **Azure Cosmos DB** account to navigate to the
    resource's page.

<img src="./media/image18.jpeg" style="width:6.5in;height:3.74514in"
alt="A screenshot of a computer Description automatically generated" />

5.  Select the **Keys** option in the **Settings** section of the
    resource navigation menu. Record the value of
    the **URI** and **PRIMARY KEY** fields. You use these values later.

<img src="./media/image19.jpeg" style="width:6.5in;height:2.75833in"
alt="A screenshot of a computer Description automatically generated" />

6.  Return to the **Resource Groups** page. Select the **Azure
    OpenAI** account.

<img src="./media/image20.jpeg" style="width:6.5in;height:4.53125in"
alt="A screenshot of a computer Description automatically generated" />

7.  In your **Azure Open AI** window, navigate to the **Resource
    Management** section, and click on **Keys and Endpoints**.

<img src="./media/image21.jpeg" style="width:6.5in;height:4.91389in"
alt="A screenshot of a computer Description automatically generated" />

8.  In **Keys and Endpoints** page, copy **KEY1,** (*You can use either
    KEY1 or KEY2)* and **Endpoint** and then **Save** the notepad to use
    the information in the upcoming tasks.

<img src="./media/image22.jpeg" style="width:6.5in;height:3.90486in"
alt="A screenshot of a computer Description automatically generated" />

### **Task 3: Run the Docker**

1.  In your Windows search box, type Docker , then click on **Docker
    Desktop**.

<img src="./media/image23.jpeg" style="width:6.5in;height:5.82778in"
alt="A screenshot of a computer Description automatically generated" />

2.  Run the Docker Desktop.

<img src="./media/image24.jpeg" style="width:6.5in;height:3.68958in"
alt="A screenshot of a computer Description automatically generated" />

## **Exercise 2 - Setup and build the starter application**

1.  From the VM searchbar, search for Visual Studio and select **Visual
    Studio Code**.

2.  Click on **File** -\> **Open Folder**

<img src="./media/image25.jpeg" style="width:6.5in;height:4.47222in"
alt="A screenshot of a computer Description automatically generated" />

3.  Select **cosmosdb-chatgpt** from **C:\LabFiles** and click
    on **Select Folder**.

<img src="./media/image26.jpeg" style="width:6.5in;height:4.13542in"
alt="A screenshot of a computer Description automatically generated" />

4.  Click on **Yes, I trust the authors** option in the **Do you trust
    the authors dialog**.

<img src="./media/image27.jpeg" style="width:6.5in;height:4.39583in"
alt="A screenshot of a computer Description automatically generated" />

5.  If there is an already open terminal, delete it.

<img src="./media/image28.png" style="width:4.58357in;height:1.70148in"
alt="A screenshot of a computer Description automatically generated" />

6.  In the **Visual Studio Code** editor, click on **Terminal**, open
    a **New Terminal**.

<img src="./media/image29.jpeg" style="width:6.5in;height:4.67917in"
alt="A screenshot of a computer Description automatically generated" />

7.  In a .NET application, it's common to use the configuration
    providers to inject new settings into your application. For this
    application, use the **appsettings.Development.json** file to
    provide the most current values for the Azure OpenAI endpoint and
    key.

8.  Open the **appsettings.Development.JSON** file. Replace the already
    existing values for uri and key values of **Azure Cosmos
    DB** and **Azure OpenAI** resources in the file with the values that
    we saved earlier.

<img src="./media/image30.jpeg" style="width:6.5in;height:2.53542in"
alt="A screenshot of a computer Description automatically generated" />

9.  **Build** the .NET project by executing the below command.

dotnet build

<img src="./media/image31.jpeg" style="width:6.5in;height:1.80556in"
alt="A screen shot of a computer Description automatically generated" />

## **Exercise 3: Understand the code**

### Task 1: Add required members and a client instance

1.  Open the **Services/OpenAiService.cs** file. This file implements
    the class variables required to use the Azure OpenAI client. It
    implements a few static prompts and create a new instance of the
    OpenAIClient class.

2.  This code block creates a new string variable named
    \_systemPromptText with a static block of text to send to the AI
    assistant before each prompt.

> <span class="mark">private readonly string \_systemPrompt = @"</span>
>
> <span class="mark">You are an AI assistant that helps people find
> information.</span>
>
> <span class="mark">Provide concise answers that are polite and
> professional." + Environment.NewLine;</span>

3.  This code block creates another new string variable named
    \_summarizePrompt with a static block of text to send to the AI
    assistant with instructions on how to summarize a conversation.

> <span class="mark">private readonly string \_summarizePrompt =
> @"</span>
>
> <span class="mark">Summarize this prompt in one or two words to use as
> a label in a button on a web page.</span>
>
> <span class="mark">Do not use any punctuation." +
> Environment.NewLine;</span>

4.  This code block creates a new instance of the OpenAIClient class
    using the endpoint to build a Uri and the key to build an
    AzureKeyCredential.

<span class="mark">Uri uri = new(endpoint);</span>

<span class="mark">AzureKeyCredential credential = new(key);</span>

<span class="mark">\_client = new(</span>

<span class="mark">endpoint: uri,</span>

<span class="mark">keyCredential: credential</span>

<span class="mark">);</span>

### **Task 2: Ask the AI model a question**

First, implement a question-answer conversation by sending a system
prompt, a question, and session ID so the AI model can provide an answer
in the context of the current conversation. Make sure you measure the
number of tokens it takes to parse the prompt and return a response (or
completion in this context).

1.  This code block creates a new variable named options of type
    ChatCompletionsOptions. Adds the two message variables to the
    Messages list and sets the value of User to the sessionId
    constructor parameter.

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
> <span class="mark">new ChatRequestUserMessage(userPrompt)</span>
>
> <span class="mark">},</span>
>
> <span class="mark">User = sessionId,</span>
>
> <span class="mark">MaxTokens = 4000,</span>
>
> <span class="mark">Temperature = 0.3f,</span>
>
> <span class="mark">NucleusSamplingFactor = 0.5f,</span>
>
> <span class="mark">FrequencyPenalty = 0,</span>
>
> <span class="mark">PresencePenalty = 0</span>
>
> <span class="mark">};</span>

2.  The GetChatCompletionsAsync method of the Azure OpenAI client
    variable (\_client) is invoked Asynchronously. The result is stored
    in a variable named completions of type ChatCompletions.

> <span class="mark">Response\<ChatCompletions\> completionsResponse =
> await_client.GetChatCompletionsAsync(options);</span>
>
> <span class="mark">ChatCompletions completions =
> completionsResponse.Value;</span>

3.  Finally, the below block of code, returns a tuple as the result of
    the GetChatCompletionAsync method with the content of the completion
    as a string, the number of tokens associated with the prompt, and
    the number of tokens for the response.

> <span class="mark">return (</span>
>
> <span class="mark">completionText:
> completions.Choices\[0\].Message.Content,</span>
>
> <span class="mark">completionTokens:
> completions.Usage.CompletionTokens</span>
>
> <span class="mark">);</span>

### **Task 3: Ask the AI model to summarize a conversation**

Now, send the AI model a different system prompt, your current
conversation, and session ID so the AI model can summarize the
conversation in a couple of words.

1.  The below code creates a ChatCompletionsOptions variable named
    options with the two message variables in the Messages list, User
    set to the sessionId constructor parameter, MaxTokens set to 200,
    and the remaining properties.

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

2.  The below code invokes the \_client.GetChatCompletionsAsync
    asynchronously with the model name (\_modelName) and the options
    variable as parameter and stores the result in a variable named
    completions of type ChatCompletions. It returns the content of the
    completion as a string as the result of the SummarizeAsync method.

> <span class="mark">Response\<ChatCompletions\> completionsResponse =
> await \_client.GetChatCompletionsAsync(options);</span>
>
> <span class="mark">ChatCompletions completions =
> completionsResponse.Value;</span>
>
> <span class="mark">string completionText =
> completions.Choices\[0\].Message.Content;</span>
>
> <span class="mark">return completionText;</span>

<img src="./media/image32.jpeg" style="width:6.5in;height:4.95486in"
alt="A screenshot of a computer program Description automatically generated" />

### **Task 4 - Connect to Azure Cosmos DB for NoSQL**

The CosmosDbService class contains a stub implementation of a service
similar to the OpenAiService class you worked on previously in this
module. In contrast, this class uses the .NET SDK for Azure Cosmos DB,
which works slightly different.

This section exaplins the implementation of the class variables and
client required to access Azure Cosmos DB for NoSQL using the client.

1.  Open the **Services/CosmosDbService.cs** file.

<img src="./media/image33.jpeg" style="width:6.5in;height:4.49236in"
alt="A screenshot of a computer program Description automatically generated" />

2.  The below code creates a variable named options of type

<span class="mark">CosmosSerializationOptions options = new()</span>

<span class="mark">{</span>

<span class="mark">PropertyNamingPolicy =
CosmosPropertyNamingPolicy.CamelCase</span>

<span class="mark">};</span>

**Note:** Setting this property will ensure that the JSON produced by
the SDK is both serialized and deserialized in camel case regardless of
how it's corresponding property is cased in the .NET class.

3.  The below code creates a new instance of type CosmosClient named
    client using the CosmosClientBuilder class, endpoint, key, and
    serialization options you specified earlier.

> <span class="mark">CosmosClient client = new
> CosmosClientBuilder(endpoint, key)</span>
>
> <span class="mark">.WithSerializerOptions(options)</span>
>
> <span class="mark">.Build();</span>

4.  The below code create a new nullable variable of type Database named
    database by calling the GetDatabase method of the client variable.

> <span class="mark">Database? database =
> client?.GetDatabase(databaseName);</span>

5.  The below code assigns the constructor's container variable to the
    class'

> **\_container = container ??**
>
> **throw new ArgumentException("Unable to connect to existing Azure
> Cosmos DB container or database.");**

<img src="./media/image34.jpeg" style="width:6.5in;height:4.44931in"
alt="A screenshot of a computer program Description automatically generated" />

### **Task 5 - Implement the Azure Cosmos DB for NoSQL service**

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

Azure Cosmos DB for NoSQL stores data in JSON format allowing us to
store many types of data in a single container. This application stores
both a chat "session" with the AI assistant and the individual
"messages" within each session. With the API for NoSQL, the application
can store both types of data in the same container and then
differentiate between these types using a simple type field.

1.  Open the **Services/CosmosDbService.cs** file.

2.  The below code creates a new variable named partitionKey of type
    PartitionKey using the current session's SessionId property as the
    parameter.

> <span class="mark">PartitionKey partitionKey =
> new(session.SessionId);</span>

3.  The below code invokes the CreateItemAsync method of the container
    passing in the session parameter and partitionKey variable. Returns
    the response as the result of the InsertSessionAsync method.

> <span class="mark">return await
> \_container.CreateItemAsync\<Session\>(</span>
>
> <span class="mark">item: session,</span>
>
> <span class="mark">partitionKey: partitionKey</span>
>
> <span class="mark">);</span>

4.  The below code creates a PartitionKey variable using
    session.SessionId as the value of the partition key.Creates a new
    message variable named newMessage with the Timestamp property
    updated to the current UTC timestamp. Invoke the CreateItemAsync
    passing in both the new message and partition key variables. Return
    the response as the result of InsertMessageAsync.

> <span class="mark">PartitionKey partitionKey =
> new(message.SessionId);</span>
>
> <span class="mark">Message newMessage = message with { TimeStamp =
> DateTime.UtcNow };</span>
>
> <span class="mark">return await
> \_container.CreateItemAsync\<Message\>(</span>
>
> <span class="mark">item: newMessage,</span>
>
> <span class="mark">partitionKey: partitionKey</span>
>
> <span class="mark">);</span>

<img src="./media/image35.jpeg" style="width:6.5in;height:4.88264in"
alt="A screenshot of a computer program Description automatically generated" />

### **Task 6: Retrieve multiple sessions or messages**

There are two main use cases where the application needs to retrieve
multiple items from our container. First, the application retrieves all
sessions for the current user by filtering the items to ones where type
= Session. Second, the application retrieves all messages for a session
by performing a similar filter where type = Session & sessionId = . Both
queries are here implemented using the .NET SDK and a feed iterator.

1.  The below code creates a new variable named query of type
    QueryDefinition. It uses the fluent WithParameter method to assign
    the name of the Session class as the value for the parameter. Then
    invokes the generic GetItemQueryIterator\<\> method on the
    \_container variable passing in the generic type Session and the
    query variable as a parameter. Store the result in a variable of
    type FeedIterator named response.

> <span class="mark">QueryDefinition query = new QueryDefinition("SELECT
> DISTINCT \* FROM c WHERE c.type = @type")</span>
>
> <span class="mark">.WithParameter("@type", nameof(Session));</span>
>
> <span class="mark">FeedIterator\<Session\> response =
> \_container.GetItemQueryIterator\<Session\>(query);</span>

2.  The below code within the while loop, asynchronously get the next
    page of results by invoking ReadNextAsync on the response variable
    and then add those results to the list variable named output.
    Outside the while loop, the output variable is returned with a list
    of sessions as the result of the GetSessionsAsync method.

> <span class="mark">FeedResponse\<Session\> results = await
> response.ReadNextAsync();</span>
>
> <span class="mark">output.AddRange(results);</span>
>
> <span class="mark">return output;</span>

3.  The below code uses the fluent WithParameter method to assign the
    @sessionId parameter to the session identifier passed in as a
    parameter, and the @type parameter to the name of the Message class.

<span class="mark">QueryDefinition query = new QueryDefinition("SELECT
\* FROM c WHERE c.sessionId = @sessionId AND c.type = @type")</span>

<span class="mark">.WithParameter("@sessionId", sessionId)</span>

<span class="mark">.WithParameter("@type", nameof(Message));</span>

4.  Create a FeedIterator\< Message \> using the query variable and the
    GetItemQueryIterator\<\> method.

FeedIterator\<Message\> response = \_container.GetItemQueryIterator\<Message\>(query);

<img src="./media/image36.jpeg" style="width:6.5in;height:4.725in"
alt="A screenshot of a computer program Description automatically generated" />

## **Exercise 4: Execute the app**

Now your application has a full implementation of Azure OpenAI and Azure
Cosmos DB. You can test the application end-to-end by debugging the
solution.

1.  From the **Visual Studio Code Terminal**, build the project using
    the below command.

+++dotnet build+++

<img src="./media/image37.jpeg" style="width:6.5in;height:3.58333in"
alt="A screenshot of a computer Description automatically generated" />

2.  Start the application with hot reloads enabled using dotnet watch.

+++dotnet watch run --non-interactive+++

<img src="./media/image38.jpeg" style="width:6.5in;height:4.13889in"
alt="A screenshot of a computer Description automatically generated" />

3.  Visual Studio Code launches the in-tool simple browser with the web
    application running. In the web application, create a new chat
    session by clicking on **+ Create New Chat** and ask the AI
    assistant a question. Then, close the running web application.

<img src="./media/image39.png" style="width:6.5in;height:2.43958in"
alt="A screenshot of a chat box Description automatically generated" />

4.  Paste the following text in the text box and click on
    the **Send** icon.

+++How many wins does it take to promote to the Premier League?+++

<img src="./media/image40.jpeg" style="width:6.5in;height:4.19306in"
alt="A screenshot of a chat Description automatically generated" />

<img src="./media/image41.jpeg" style="width:6.5in;height:3.98194in"
alt="A screenshot of a computer Description automatically generated" />

5.  Paste the following text in the text box and click on
    the **Send** icon.

+++What is Azure OpenAI?+++

<img src="./media/image42.jpeg" style="width:6.5in;height:4.30486in"
alt="A screenshot of a chat Description automatically generated" />

<img src="./media/image43.jpeg" style="width:6.5in;height:4.28056in"
alt="A screenshot of a chat Description automatically generated" />

6.  Close the terminal.

## **Exercise 5: Clean up resource group**

1.  Open a new browser and enter the following URL in the address
    bar: +++https://portal.azure.com/+++ to open the Azure Portal.

2.  Click on the **Portal Menu**, then select **Resource group.**

<img src="./media/image15.jpeg" style="width:6.5in;height:3.42222in"
alt="A screenshot of a computer Description automatically generated" />

3.  Select the **mslearn-cosmos-openai** resource group.

<img src="./media/image16.jpeg" style="width:6.5in;height:5.65208in"
alt="A screenshot of a computer Description automatically generated" />

4.  In the Resource group page, navigate to command bar and click
    on **Delete resource group**.

<img src="./media/image44.jpeg" style="width:6.5in;height:3.31667in"
alt="A screenshot of a computer Description automatically generated" />

5.  In the **Delete Resource group** pane that appears on the right
    side, enter the **resource group name** and click
    on **Delete** button.

<img src="./media/image45.jpeg" style="width:6.5in;height:7.82986in"
alt="A screenshot of a computer Description automatically generated" />

6.  Once the Resource group is deleted, from the Azure portal home page,
    search for +++**Azure AI Services**+++ and select it.

<img src="./media/image46.png" style="width:6.26806in;height:4.14236in"
alt="A screenshot of a computer Description automatically generated" />

7.  Select **Azure OpenAI** from the left pane and then select **Manage
    deleted resources**.

<img src="./media/image47.png" style="width:6.26806in;height:3.73889in"
alt="A screenshot of a computer Description automatically generated" />

8.  Select the resource that gets listed there and then click on
    **Purge**.

<img src="./media/image48.png" style="width:4.00021in;height:5.03498in"
alt="A screenshot of a computer Description automatically generated" />

9.  Click on **Yes**.

<img src="./media/image49.png" style="width:5.85447in;height:2.04177in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image50.png" style="width:5.97947in;height:3.43073in"
alt="A screenshot of a delete Description automatically generated" />

**Summary**

This lab provided a comprehensive guide to building, deploying, and
testing a custom chat application using Blazor, PostgreSQL, and Azure
OpenAI. In this lab, you've learned to set up the necessary development
environment, created and designed a Blazor-based chat interface,
configured and connected a PostgreSQL database on Azure, integrated
Azure OpenAI for enhanced functionalities, and finally deployed and
tested the application on Azure. This hands-on experience equipped you
with the skills to develop and manage modern web applications using
cutting-edge technologies and cloud services

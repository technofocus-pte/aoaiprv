# Lab 02- Exploring Azure AI Studio Playground

**Introduction**

You can use the Azure AI Studio Playground for text completions, viewing
python, json, C#, and curl code samples prefilled according to your
selected settings, providing your app the ability to hear and speak by
pairing Azure OpenAI Service with Azure AI Speech to enable richer
interactions, etc. You can use Azure OpenAI Service and Azure AI Speech
to:

- Speak to the assistant via speech to text.

- Hear the assistant's response via text to speech.

The speech to text and text to speech features can be used together or
separately in the Azure AI Studio playground. You can also use the
playground to test your chat model before deploying it.

**Objectives**

- To explore Azure AI Studio by creating and deploying a Speech
  resource, setting up projects, and deploying an Azure OpenAI model for
  text completions.

- To enable voice interactions in the Azure AI Studio playground by
  pairing Azure OpenAI with Speech services, conducting chat sessions,
  and customizing the AI assistant's behavior.

- To review and extract code samples for Azure OpenAI and Speech
  services, gaining insights into integrating speech-to-text and
  text-to-speech functionalities in applications.

## Task 1: Create a Speech resource in the Azure portal

1.  Open your browser, navigate to the address bar, and paste the
    following URL:
    <https://portal.azure.com/#create/Microsoft.CognitiveServicesSpeechServices>
    then press the **Enter** button.

<img src="./media/image1.png" style="width:6.5in;height:4.0375in" />

2.  On the **Create Speech Services** page, enter the following
    information, then click on **Review+create** button.

| **Field** | **Description** |
|----|----|
| **Subscription** | Select your Azure OpenAI subscription |
| **Resource group** | Select your Resource group (that you have created in **Lab 1**) |
| **Region** | East US |
| **Name** | SpeechChat-testXX (XX can be unique number) |
| **Pricing Tier** | Standard S0 |

<img src="./media/image2.png" style="width:6.5in;height:6.61667in"
alt="A screenshot of a speech service Description automatically generated" />

3.  Once the Validation is passed, click on the **Create** button.

<img src="./media/image3.png" style="width:6.5in;height:7.43333in"
alt="A screenshot of a computer Description automatically generated" />

4.  Wait for few minutes until the deployment is completed.

<img src="./media/image4.png" style="width:6.09458in;height:2.99585in"
alt="A screenshot of a computer Description automatically generated" />

## **Task 2: Create the project using Azure AI Studio**

1.  After the deployment is completed, click on **Home** at the top left
    corner of the page to go back to Azure portal. In the Azure portal,
    navigate and click on **Resource groups** under **Azure services**.

<img src="./media/image5.png" style="width:6.5in;height:3.75833in"
alt="A screenshot of a computer Description automatically generated" />

> <img src="./media/image6.png" style="width:6.2678in;height:4.42094in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Select the resource group that you’ve created in **Lab \#1**.

> <img src="./media/image7.png"
> style="width:5.75833in;height:3.90833in" />

3.  In the **AOAI-RGXX Resource group** page, navigate and click on
    **Azure-openai-testXX** as shown in the below image.

> <img src="./media/image8.png"
> style="width:6.49167in;height:3.07917in" />

4.  In **Azure-openai-testXX** page, click on **Overview** in the
    left-sided navigation menu, scroll down and click on **Explore Azure
    AI Studio** button as shown in the below image.

> <img src="./media/image9.png"
> style="width:6.49167in;height:4.08333in" />

5.  On **Azure AI Preview** window, **Welcome to Azure AI Studio
    Preview** dialog box appear. Navigate and click on **Sign in**
    button on the right side. Then, navigate to **Welcome to Azure AI
    Studio Preview** dialog box and click on **Create now** button.

> <img src="./media/image10.png" style="width:6.5in;height:3.61667in" />
>
> <img src="./media/image11.png" style="width:6.5in;height:5.18542in"
> alt="A screenshot of a computer Description automatically generated" />

6.  Now, you’re directed to the **Azure AI Studio** home page,

> <img src="./media/image12.png" style="width:6.59871in;height:3.12381in"
> alt="A screenshot of a computer Description automatically generated" />

## **Task 3: Hear and speak with chat models in the Azure AI Studio playground**

Give your app the ability to hear and speak by pairing Azure OpenAI
Service with Azure AI Speech to enable richer interactions.

The speech to text and text to speech features can be used together or
separately in the Azure AI Studio playground. You can use the playground
to test your chat model before deploying it.

In this chat session, you use both speech to text and text to speech.
You use the speech to text feature to speak to the assistant, and the
text to speech feature to hear the assistant's response.

1.  In the **Azure AI Studio Preview** page, under **Build** tab,
    navigate to **Components** section and click on **Deployments**.

> <img src="./media/image13.png" style="width:6.13333in;height:4.475in" />

2.  In the **Deployments** window, drop down the **+Create** and select
    Real-time endpoint.

> <img src="./media/image14.png"
> style="width:6.39167in;height:4.99167in" />

3.  In the **Select a model** dialog box, navigate and carefully select
    **gpt-4**, then click on **Confirm** button.

<img src="./media/image15.png"
style="width:4.63333in;height:5.14167in" />

4.  In the **Deploy model** dialog box, under the **Deployment name**
    field, ensure that **gpt-4** and model version is **0125-preview**
    is selected, then click on the **Deploy** button.

> <img src="./media/image16.png" style="width:4.65in;height:3.58333in"
> alt="A screenshot of a computer Description automatically generated" />

5.  **gpt-4** deployment is successful.

> <img src="./media/image17.png" style="width:6.5in;height:4.35903in" />

6.  In **gpt-4** pane, click on **Open in Playground** button.

> <img src="./media/image18.png"
> style="width:6.49167in;height:4.63333in" />

7.  Click on the dropdown beside **Mode** and select **Chat**. Navigate
    to **Configuration** section and ensure that **gpt-4** is selected
    under **Deployment**.

> <img src="./media/image19.png" style="width:6.49167in;height:3.6in" />

8.  Now, navigate to the Chat session section and click on **Playground
    Settings**.

<img src="./media/image20.png" style="width:6.5in;height:3.925in" />

** Note:** You should also see the options to select the microphone or
speaker buttons. If you select either of these buttons but haven't yet
enabled speech to text or text to speech, you are prompted to enable
them in **Playground Settings**.

9.  On the **Playground Settings** page, provide the following
    information and then click on the **Save** button.

| **Language** | Select the language locale and voice you want to use for speaking and hearing. (In this lab, we are selecting **English**). |
|----|----|
| **Subscription** | Select your Azure OpenAI subscription |
| **Speech resource** | Select your speech resource group that you’ve created in **Task \#1**. |
| **Voice configuration** | Emma |

- **Select the check box**-I acknowledge that spoken chat will incur
  usage to my subscription.

- Select **Enable speech to text** and **Enable text to speech**.

**Note**: Optionally, you can enter some sample text and
select **Play** to try the voice.

> <img src="./media/image21.png"
> style="width:6.20833in;height:7.13333in" />

10. Select the microphone button and speak to the assistant. For
    example, you can say "**Do you know where I can get an Xbox**".

<img src="./media/image22.png" style="width:6.48333in;height:3.175in" />

7.  In case, use your microphone dialog box appears, then click on the
    **Allow** button.

<img src="./media/image23.png" style="width:4.91667in;height:3.93333in"
alt="A screenshot of a computer Description automatically generated" />

8.  Click on the **Send** button (represented by right arrow) to send
    your message to the assistant. The assistant's response is displayed
    in the chat session pane.

<img src="./media/image24.png"
style="width:6.49167in;height:3.01667in" />

<img src="./media/image25.png" style="width:6.5in;height:3in" />

** Note:** If the speaker button is turned on, you'll hear the
assistant's response. If the speaker button is turned off, you won't
hear the assistant's response, but the response will still be displayed
in the chat session pane.

9.  Select the microphone button and speak to the assistant. You can say
    " **How do the capabilities of Azure OpenAI compare to OpenAI?”**

10. Click on the **Send** button (represented by right arrow) to send
    your message to the assistant. The assistant's response is displayed
    in the chat session pane.

<img src="./media/image26.png"
style="width:7.39127in;height:3.42083in" />

<img src="./media/image27.png" style="width:6.5in;height:3.16667in" />

11. Navigate to **Assistant setup** section. You can change the system
    prompt to change the assistant's response format or style. Paste the
    following content under **System message** box, then click on
    **Apply changes** as shown in the below image.

> Copy
>
> <span class="mark">"You're an AI assistant that helps people find
> information. Answers shouldn't be longer than 20 words because you are
> on a phone. You could use 'um' or 'let me see' to make it more natural
> and add some disfluency."</span>

<img src="./media/image28.png" style="width:6.45in;height:2.90833in" />

12. In the **Update system message?** dialog box, click on the
    **Continue** button**.**

> <img src="./media/image29.png"
> style="width:3.51528in;height:2.67431in" />

13. Select the microphone button and speak to the assistant. You can say
    "**Do you know where I can get an Xbox?”**

14. Click on the Send button (represented by right arrow) to send your
    message to the assistant. The assistant's response is displayed in
    the chat session pane.

<img src="./media/image30.png" style="width:6.45in;height:2.99167in" />

<img src="./media/image31.png" style="width:6.5in;height:3.01667in" />

15. Select the **View Code** button to view and copy the sample code,
    which includes configuration for Azure OpenAI and Speech services.
    You can use the sample code to enable speech to text and text to
    speech in your application.

<img src="./media/image32.png" style="width:6.5in;height:3.8125in"
alt="Screenshot of viewing the code in the playground." />

## Task 4: Clean up resources

To avoid incurring unnecessary Azure costs, you should delete the
resources you created in this quick start if they're no longer needed.
To manage resources, you can use the [Azure
portal](https://portal.azure.com/?azure-portal=true).

1.  To delete the storage account, navigate to **Azure portal Home**
    page, click on **Resource groups**.

> <img src="./media/image6.png" style="width:6.5in;height:4.58472in"
> alt="A screenshot of a computer Description automatically generated" />

2.  Click on the resource group that you’ve created.

> <img src="./media/image33.png" style="width:6.49167in;height:4.15833in"
> alt="A screenshot of a computer Description automatically generated" />

3.  Carefully select all resources except Azure Open AI service that you
    have created in **Lab \#1**.

**Note**: Don’t select Azure OpenAI service.

<img src="./media/image34.png"
style="width:6.49167in;height:3.74167in" />

4.  In the Resource group page, navigate to
    <span class="mark">the</span> command bar and click on **Delete**.

**Important Note**: Don’t click on **Delete resource group**. If you
don’t see the **Delete** option in the command bar, then click on the
horizontal ellipses.

<img src="./media/image35.png"
style="width:7.0375in;height:3.21611in" />

5.  In the **Delete Resources** pane that appears on the right side,
    navigate to **Enter “delete” to confirm deletion** field, type
    **delete**, then click on the **Delete** button.

<img src="./media/image36.png"
style="width:5.91667in;height:6.99167in" />

6.  On **Delete confirmation** dialog box, click on **Delete** button.

> <img src="./media/image37.png" style="width:5.06711in;height:3.50447in"
> alt="A screenshot of a computer Description automatically generated" />

7.  Click on the bell icon, you’ll see the notification – **Executed
    delete command on 4 selected items.**

**Summary**

This lab focuses on hands-on exploration of Azure AI Studio and Azure
Cognitive Services for Speech and OpenAI integration. In this lab,
you’ve created and deployed resources, developed and tested text
completions, and engaged in chat sessions with AI models. At the end of
the lab, you’ve deleted the resources to avoid incurring unnecessary
Azure costs. In this lab, you’ve acquired practical skills in AI model
deployment, customization, and integration with speech capabilities,
making it a comprehensive learning experience in Azure AI technologies.

**Important Note: Please do not delete the Resource Group. If deleted,
you’ll not be able to proceed with the next lab or create a new Resource
Group.**

# 🚨 Lab 05: Create a custom agent using natural language with Copilot

## 🕵️‍♂️ CODENAME: `OPERATION AGENT FORGE`

> **⏱️ Operation Time Window:** `~75 minutes`

## 🎯 Lab Brief

Welcome back, Agent Maker. This lab puts you in the command seat of the most powerful capability in Copilot Studio - creating a custom agent from scratch using only natural language… and supercharging it with your own data.

This isn’t just another chatbot. You’re building a knowledge empowered digital coworker - one that can reason, respond, and reference real enterprise info.

Your weapon of choice? Natural language. Your lab? Design, train, and test a fully customized helpdesk agent that answers IT questions using SharePoint, uploaded files, or company URLs.

Let’s build your agent from the ground up.

## 🔎 Objectives

In this lab, you’ll learn:

1. Understanding what custom agents are and how they differ from pre-built templates
1. Creating agents using natural language prompts and conversational design with Copilot
1. Grounding agents with enterprise knowledge sources including SharePoint, documents, and websites
1. Learning about generative orchestration and how agents dynamically search and respond using multiple data sources
1. Building and testing a fully functional IT helpdesk agent that can answer questions from your own data

##
## 🧪 Lab 05: Create a custom agent in Copilot Studio

We're now going to learn how to create a custom agent that can chat over your data

### ✨ Use case

We'll use the same use case from [Lab 03 - Create a declarative agent for Microsoft 365 Copilot](../Day1/lab03.md#use-case-scenario)

**As an** employee

**I want to** get quick and accurate help from the IT helpdesk agent for issues like device problems, network troubleshooting, printer setup

**So that I can** stay productive and resolve technical issues without delays

Let's begin!

### ✨ Prerequisites

- **SharePoint site**

We'll be using the **Contoso IT** SharePoint site from [Lab 00 - Course Setup - Step 3: Create new SharePoint site](../Day1/lab00.md#step-4-create-new-sharepoint-site).

If you have not set up the **Contoso IT** SharePoint site, please head back to [Lesson 00 - Course Setup - Step 3: Create new SharePoint site](../Day1/lab00.md#step-4-create-new-sharepoint-site).

- **Solution**

We'll be using the **Contoso Helpdesk Agent** solution from [Lesson 04 - Creating a Solution for your agent](../04-creating-a-solution/index.md#41-create-a-solution-publisher).

If you have not set up the **Contoso Agent** solution, please head back to [Lesson 04 - Creating a Solution for your agent](../04-creating-a-solution/index.md#41-create-a-solution-publisher).

### 6.1 Use natural language to create an agent with Copilot

> [!WARNING] Copilot questions may differ across sessions
>
> The Copilot conversational creation experience can vary each time where the provided questions for guidance may be slightly different than previously.

1. Navigate to the Home page of Copilot Studio and in the field, enter the following prompt which describes the IT help desk agent. The prompt includes the goal of the agent, the context, the expected tasks and format of the agent's response.

    ```text
    You are an IT help desk agent. Your goal is to assist users with their IT issues. You can access information from our company's knowledge base at https://support.microsoft.com/en-us. Your responses should be polite and helpful. If a user reports a slow computer, ask about the age of the device, current software versions, and if they've recently installed any new programs. If a user is experiencing trouble logging into their email, guide them through password reset procedures. You should be concise and informative, using step-by-step instructions with bullet points when appropriate.
    ```

    ![Enter prompt](./assets/6.1_01_Prompt.png)

1. The conversational creation experience with Copilot will next load. You'll see Copilot is in progress of responding to you.

    ![Copilot conversational creation experience](./assets/6.1_02_ConversationalCreationExperienceLoads.png)

1. Copilot confirms the agent has been set up with the instructions provided, and is asking for confirmation on the name of the agent. We'll ask Copilot to name our agent as,

    ```text
    Contoso Helpdesk Agent
    ```

    ![Rename the agent](./assets/6.1_03_AgentName.png)

1. Copilot performs the request and we'll see that the name of the agent has been updated in the agent pane. Copilot next asks us to refine the instructions. It's asking how we should respond to particular issues and we'll request that it acknowledges the issue, provide examples of topics to answer, and format the response as bullet points.

    Copy and paste the following, and submit the request to Copilot.

    ```text
    Prioritize urgent requests. Examples of IT issues or scenarios to help with: device problems, network connectivity, log in issues. When troubleshooting, first acknowledge their issue and respond with empathy, then provide step by step guidance using bullet points and ask if they require further assistance.
    ```

    ![Refine agent instructions](./assets/6.1_04_RefineInstructions.png)

1. The instructions of the agent will be updated after Copilot has received the request. Notice how on the right hand side pane, that starter prompts have now appeared. These were formed based on our instructions.

    Next, Copilot is asking for public websites to ground the agent's knowledge.

    Copy and paste the following, and submit the request to Copilot.

    ```text
    https://support.microsoft.com
    ```

    ![Add publicly accessible website](./assets/6.1_05_KnowledgeSource.png)

1. The public website will be added as a knowledge source. Copilot is asking if additional knowledge sources are to be added. We don't need to add additional public websites.

    Copy and paste the following, and submit the request to Copilot.

    ```text
    Proceed with setup
    ```

    ![Proceed with setup](./assets/6.1_06_ProceedWithSetup.png)

1. Copilot confirms the setup of our Contoso Helpdesk Agent is complete but we'll add one more modification, we're going to request that our agent does not answer HR related questions. This lets our agent know that it should not answer HR related questions asked by users.

    Copy and paste the following, and submit the request to Copilot.

    ```text
    Do not provide assistance to questions related to HR, examples are: What is my vacation leave balance? How many sick days do I have? What's the URL to our payroll portal? 
    ```

    ![Do not answer HR related questions](./assets/6.1_07_DoNotTalkAbout.png)

1. The instructions will be updated to not provide assistance with questions related to HR. We don't need to make further updates, our agent is ready to be created.

    ![Agent instructions updated](./assets/6.1_08_AgentInstructionsUpdated.png)

1. Before we create our agent, let's do a couple of things.

    First, select the **Configure** tab to view the agent details defined from our conversation with Copilot. This is where you'll see the Name, Description, Instructions, Knowledge and Suggested/Starter prompts.

    ![View agent details](./assets/6.1_09_ViewAgentDetails.png)

1. Secondly, let's test our agent. Copy and paste the following, and submit the question to our agent.

    ```text
    How can I check the warranty status of my Surface?
    ```

    ![Test agent](./assets/6.1_10_TestAgent.png)

1. The response to the question will then display where the answers are in the format of a step-by-step guide using bullet points. Great, our agent works! 🙌🏻

    ![Agent Response](./assets/6.1_11_AgentResponse.png)

1. Lastly, we'll double check the solution that our agent will be created in, is the solution we created and selected as the preferred solution in [Lesson 04 - Create a new solution](../04-creating-a-solution/index.md#42-create-a-new-solution).

    Select the **ellipsis icon (...)** and select **Update Advanced Settings**.

    ![Update Advanced Settings](./assets/6.1_12_UpdateAdvancedSettings.png)

1. The **Advanced Settings** modal will appear and we can see our solution created from earlier is selected by default. This is due to selecting our solution as the preferred solution in [Lesson 04 - Create a new solution](../04-creating-a-solution/index.md#42-create-a-new-solution).

    Select **Cancel.**

    ![View of Advanced Settings](./assets/6.1_13_AdvancedSettings.png)

1. Let's now create our custom agent! Select **Create**.

    ![Select Create](./assets/6.1_14_CreateAgent.png)

1. Copilot Studio will begin provisioning our agent.

    ![Setting up agent](./assets/6.1_15_SettingUpAgent.png)

1. Once our agent has been provisioned, we can see the details of the agent reflect what we requested during our Copilot conversational creation experience. Scroll down to review the agent where you'll see the name, description, instructions, the knowledge sources and the suggested prompts. The orchestration mode is enabled by default and the default model is used for the response model of the agent.

    ![Agent created](./assets/6.1_16_AgentCreated.png)

    ![Knowledge sources](./assets/6.1_17_KnowledgeSources.png)

    ![Suggested prompts](./assets/6.1_18_SuggestedPrompts.png)

1. Let's now test our newly created agent. In the **Test** pane on the right hand side, select the **Activity Map** icon.

    ![Select Activity Map](./assets/6.1_19_ActivityMap.png)

1. Enter the following question in the **Test** pane.

    ```text
    How do I find my Windows 11 product key?
    ```

    ![Test newly created agent](./assets/6.1_20_TestAgent.png)

1. The Activity map will then load which shows us in real-time what path the agent is processing. In this scenario, our agent has understood the question and searches the knowledge sources. Currently we have one source which is the public website we added earlier using Copilot, which is what the agent is reviewing.

    ![Reviewing knowledge sources](./assets/6.1_21_ReviewingSources.png)

1. Our agent then responds with answers that are outlined as bullet points, as defined in the instructions. The response has references to the web pages that the agent formed its response from. This enables users to verify the source of the answer.

    ![References in response](./assets/6.1_22_Response.png)

1. You can also review the response and its sources by scrolling down the **Knowledge modal** in the Activity map.

    ![Referenced sources](./assets/6.1_23_ReferencedSources.png)

Congratulations! You've built your first custom agent with Copilot in Copilot Studio 🙌🏻

### 6.2 Add an internal knowledge source using a SharePoint site

Previously with Copilot, we added a public website as an external knowledge source for our agent during the conversational creation experience. We're now going to add an internal knowledge source using a SharePoint site. This will be the SharePoint site you created during [Lesson 00 - Course Setup](../00-course-setup/index.md#step-4-create-new-sharepoint-site).

1. Select **+ Add knowledge**.

    ![Select Add knowledge](./assets/6.2_01_AddKnowledge.png)

1. Select **SharePoint**.

    ![Select SharePoint](./assets/6.2_02_SelectSharePoint.png)

1. Paste in the **address of the SharePoint site** created in [Lesson 00 - Course Setup](../00-course-setup/index.md#step-4-create-new-sharepoint-site) in the SharePoint URL field and select **Add**.

    ![Enter SharePoint site URL](./assets/6.2_03_AddSharePointURL.png)

1. Update the **name** of the SharePoint site to `Contoso IT` and select **Add**.

    ![Update SharePoint site name](./assets/6.2_04_UpdateNameAddToAgent.png)

1. The SharePoint site has now been added as a knowledge source with a status of _Ready_. The Status column will show whether the knowledge source has been loaded/connected to successfully, or if there is an issue.

    ![SharePoint site status](./assets/6.2_05_SharePointStatus.png)

### 6.3 Add an internal knowledge source by uploading a document

We'll now add another internal knowledge source by uploading a document directly to our agent.

1. Select **Add knowledge**.

    ![Select Add knowledge](./assets/6.3_01_AddKnowledge.png)

1. Select **Upload file** or **Select to browse**.

    ![Select upload files](./assets/6.3_02_UploadFile.png)

1. Download this [sample file](https://raw.githubusercontent.com/microsoft/agent-academy/refs/heads/main/docs/recruit/06-create-agent-from-conversation/assets/Contoso_Guest_WiFi_Connection_Guide.docx) and select it in your File Explorer. Select **Open**.

    ![Select document](./assets/6.3_03_SelectFile.png)

1. The file has been selected for upload. Select **Add to agent** next.

    ![Select Add to Agent](./assets/6.3_04_AddToAgent.png)

1. The document will be in the process of being added to the agent. Wait until the upload has completed, do not close the browser window. The status of the document will initially show as _In progress_, wait until the status has been updated to **Ready** before testing your agent.

    ![File status](./assets/6.3_05_FileStatus.png)

Let's now test our agent!

### 6.4 Test agent

We'll test our three knowledge sources by asking questions to our Contoso Helpdesk Agent.

1. Select the **refresh** icon in the test pane, followed by selecting the **activity map** icon.

      ![Refresh icon](./assets/6.4_01_RefreshAndActivityMap.png)

1. Enter the following question to test our public website (external) knowledge source.

      ```text
      How can I find the serial number on my Surface device?
      ```

      ![Enter prompt to test website knowledge source](./assets/6.4_02_TestQuestion1.png)

1. You'll next see the agent reviewing the knowledge sources and providing a response using the website knowledge source.

      ![Web page referenced in response](./assets/6.4_03_ReviewingSources.png)

1. A response will be returned an notice how there are references to the web page it formed its answer from. If you scroll down the knowledge modal in the activity map, you'll see the other knowledge sources the agent searched, which is the SharePoint site and the uploaded file.

    However these were not used as in the **Referenced sources** section, the website knowledge source was only referenced. The answer was grounded using the website knowledge source. If you select the references, you'll be directed to the web page.

    ![Knowledge sources referenced and searched](./assets/6.4_04_ReferencedSources.png)

1. Let's now test both our SharePoint site knowledge source and document knowledge source in a single message. Enter the following question.

    ```text
    How can I access our company Contoso VPN? How do guests connect to the Contoso Guest wifi?
    ```

    ![Test SharePoint and document knowledge sources](./assets/6.4_05_TestQuestion2.png)

1. Once again you'll see the agent reviewing the three knowledge sources to generate a response to the questions our single message. The agent responds to both questions in a single message, and separately references the SharePoint page and document of where it generated its response from.

    In the knowledge modal in the activity map, you'll see the SharePoint site and document used as the reference sources. You have full visibility of what knowledge sources were used to answer both questions.

    ![Knowledge sources referenced](./assets/6.4_06_ReferencedSources.png)

1. It's always good to verify the generated response is correct. Select the SharePoint site reference and the FAQs SharePoint page will load where you can scroll down to review the VPN instructions.

    ![Review SharePoint page](./assets/6.4_07_VerifySharePoint.png)

1. Next, select the document reference and a modal will appear with the text from the document that reflects the answer.

    ![Review document](./assets/6.4_08_VerifyDocument.png)

The agent can answer multiple questions in a single message, and search the knowledge sources + reference the knowledge sources in its response. Make sure to always verify the response is correct by reviewing the references.

## ✅ Lab Complete

Congratulations! 👏🏻 You've learnt how to use natural language to create your own custom agent that can chat over your data from three different knowledge sources 🙌🏻

This is the end of **Lab 06 - Create an agent with Copilot**, select the link below to move to the next lesson. Your custom agent created in this lab will be used in the next lesson's lab.

⏭️ [Move to **Add a new Topic with trigger** lesson](../07-add-new-topic-with-trigger/index.md)

Welcome to the elite. You now know how to forge digital agents that speak your language, reference your data, and support your team. Keep going—your lab’s just getting started.

## 📚 Tactical Resources

🔗 [Quickstart: Create and deploy an agent](https://learn.microsoft.com/microsoft-copilot-studio/fundamentals-get-started?context=%2Fmicrosoft-365-copilot%2Fextensibility%2Fcontext/?WT.mc_id=power-172617-ebenitez)

🔗 [Create and delete agents](https://learn.microsoft.com/microsoft-copilot-studio/authoring-first-bot?WT.mc_id=power-172617-ebenitez)

🔗 [Key concepts - Authoring agents](https://learn.microsoft.com/microsoft-copilot-studio/authoring-fundamentals/?WT.mc_id=power-172617-ebenitez)

📺 [Create a custom agent using natural language](https://aka.ms/ai-in-action/copilot-studio/ep1)

📺 [Add knowledge to your agents](https://aka.ms/ai-in-action/copilot-studio/ep2)

<!-- markdownlint-disable-next-line MD033 -->
<img src="https://m365-visitor-stats.azurewebsites.net/agent-academy/recruit/06-create-agent-from-conversation" alt="Analytics" />
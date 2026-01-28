---
prev:
  text: 'Multi-Agent Systems'
  link: '/operative/03-multi-agent'
next:
  text: 'Understanding Agent Models'
  link: '/operative/05-model-selection'
---

# 🚨 Mission 04: Add Event Triggers to act autonomously

## 🕵️‍♂️ CODENAME: `OPERATION SIGNAL POINT`

> **⏱️ Operation Time Window:** `~45 minutes`

## 🎯 Mission Brief

Welcome back, Agent. In [Mission 03](../Lab%208/index.md) - you learned how to build an Application Intake child agent and an Interview Prep connected agent to broaden your main Hiring Agent's capabilities.

Your assignment, should you choose to accept it, is **Operation Signal Point** - diving deeper into **event triggers** - elevating your agent system from reactive to **autonomous operation**. You'll transform your agents from waiting for human input to proactively responding to external events and taking intelligent action without supervision.

Think of it as upgrading from agents that _answer questions_ to agents that _anticipate needs_ and _act independently_. Through event triggers and automated workflows, your Hiring Agent will detect incoming resume emails, process attachments automatically, store data in Dataverse, and notify your HR recruitment team via Microsoft Teams - all while you focus on higher-value tasks.

Welcome to the world where automation meets intelligence.

## 🔎 Objectives

In this mission, you'll learn:

1. How event triggers enable autonomous agent behavior without user interaction
1. The differences between interactive and autonomous agents in Copilot Studio
1. How to create event triggers that automatically process email attachments and upload files to Dataverse
1. How to build agent flows that post adaptive cards to Teams channels for notifications
1. How to pass data between event triggers and agent flows for end-to-end automation

## 🤔 What is an Event trigger?

**Event triggers** let an agent _act_ on _its_ own when something happens in another system - no user message required. When the configured event fires - such as "new SharePoint item," "new email," "Planner task assigned," or even a time‑based recurrence, a connector sends a trigger payload to your agent. The agent then follows your instructions to decide which actions or topics to call.

### Key characteristics

- **Autonomous activation:**
      - Unlike topic triggers that start when a user types to the agent, event triggers fire from external events, enabling proactive behavior.

- **Payload-driven:**
      - Each event delivers a payload (variables + optional instructions) through a connector. The agent uses your defined instructions and the payload to choose what to do next.
      - For example, _call a topic_ or _execute actions defined by Tools_.

- **Examples out-of-the-box:**
      - SharePoint/OneDrive file or item created
      - Planner task completed/assigned
      - Microsoft Forms response submitted
      - Recurrence/schedule

    Availability depends on your organization's data policies configured in Power Automate.

- **Requires generative orchestration:**
      - Event triggers are available only when generative orchestration is enabled for the agent.

- **Billing/usage:**
      - Each trigger delivery counts as a message toward Copilot Studio capacity.
      - For example a 10‑minute recurrence sends a message every 10 minutes.

- **Auth model and setup:**
      - You add triggers within the agent Overview, under _Triggers_. Authentication for the trigger connector uses the agent maker's account ("agent author authentication").
      - You can edit trigger parameters and payload in the Power Automate maker portal.

- **Testing & observability:**
      - You can test triggers from the agent's test pane and inspect behavior with the activity map before publishing.

> [!NOTE] TL;DR for developers
>
> Think of event triggers as **webhook-like signals** that push a structured payload into your agent, letting it _initiate_ work and chain actions across systems - without waiting for a user to ask.

### Topic triggers - how they differ

Topic triggers control _when a topic runs_, usually in response to a user message.

- In generative orchestration, the default trigger is **By agent** - the planner chooses a topic whose name/description best matches the user's message.
- In classic orchestration, the default is **Phrases** - the planner chooses a topic when one or several trigger phrases best match the user's message.

Other trigger types include `Message received`, `Event received`, `Activity received`, `Conversation update`, `Invoke received`, `On redirect`, `Inactivity`, and `Plan complete`.

> [!NOTE] Core difference
>
> Topic triggers are _conversation activity_ starters inside the chat.
>
> Event triggers are system _event_ starters delivered via connectors that can run the agent without any conversation at all.

### Quick guide of Topic trigger vs Event trigger

- **Topic trigger:** User (or chat activity) said/did X ➡️ run Topic T.
- **Event trigger:** SharePoint/Planner/Email/Timer fired with payload P ➡️ agent evaluates instructions ➡️ call Actions/Topics accordingly.

## 🏓 Interactive agent vs Autonomous agent - comparison

Now that you know the difference between event triggers and topics triggers, let's next learn about the difference between an interactive agent vs an autonomous agent.

In Copilot Studio terms, "interactive" maps to agents that primarily engage via **topics** in a chat or channel. "Autonomous" maps to agents that also leverage **event triggers** to run without user input.

The following table summarizes their differences and similarities.

| Dimension                           | Interactive agent     | Autonomous agent                                                                                              |
|-------------------------------------|-----------------------|---------------------------------------------------------------------------------------------------------------|
| How it starts                       | User (or chat activity) triggers a topic. Example: By agent, Phrases, Message received.   | External event trigger sends a payload via connector to the agent. Example: SharePoint, Planner, email, schedule, etc. |
| Primary use                         | Q&A, guided workflows, request-driven actions in chat - Teams, web, etc.  | Proactive operations and background automation - react to system changes and then notify, file, or orchestrate tasks. |
| Trigger surface                     | Topic triggers: By agent / Phrases / Message received / Activity types / Invoke / Inactivity / Plan complete | Event triggers library via connectors; payload includes event data + optional instructions. |
| Planner (generative orchestration)  | Strongly leveraged for By agent and Plan complete triggers to select/sequence topics. | Required for event triggers; the agent uses instructions + payload to decide which actions/topics to call. |
| Typical example                     | User asks "What's our refund policy?" → Topic runs, queries knowledge, response. | New Planner task assigned → Event trigger fires → Agent posts a Teams message, updates a record, or calls a topic. |
| Setup path                          | Create topics, define trigger type, author dialog/actions; publish to channels. | Add event trigger (Overview → Triggers), authenticate connector with agent author credentials, configure payload/instructions; test via test pane; publish. |
| Auth and governance                 | Runs under channel/auth context; topic triggers respond to chat activities in allowed channels. | Trigger availability depends on Power Automate data policies; connectors run under the agent maker's account. |
| Observability                       | Test topics within Copilot Studio, inspect conversation transcripts/activities. | Use Test trigger and activity map to validate execution before publishing, monitor activity after publishing. |
| Capacity impact                     | Each user message/agent response is a message consuming capacity. | Each event delivery is also a message, plus any subsequent actions. Example: a 10‑minute recurrence = 6 messages/hour |

### When to use which?

- Choose **topic triggers (interactive)** when users initiate the agent conversation - FAQ, guided intake, or command‑style tasks inside chat. The planner's By agent trigger reduces manual phrase curation.
- Add **event triggers (autonomous)** when the agent should start the conversation or take action itself - on updates in SharePoint/Dataverse, incoming email, or on a schedule. This moves you from reactive to proactive operations.

## 🧪 Lab 04 - Automating candidate application emails

We're next going to add an event trigger to the **Hiring Agent** and build an agent flow in the child **Application Intake Agent** to handle further processing for autonomy.

### ✨ Use case scenario

**As an** HR Recruiter

**I want to** be notified when an email with a resume arrives in my Inbox and is automatically uploaded to Dataverse

**So that I can** stay notified of resumes sent by email for applications automatically uploaded to Dataverse

We'll be achieving this using two techniques

1. An event trigger for when the email arrives,
    1. Check the `contentType` of the file equals `PDF` as the format type.
    1. Extract the file and upload to Dataverse using actions through the Dataverse connector.
    1. Then send a prompt to the agent for further processing by passing input parameters from the Dataverse actions.

1. An agent flow will be added to the child **Application Intake Agent** which is invoked by the prompt in the event trigger.
    1. Use the input parameters passed from the prompt of the event trigger in an adaptive card posted to a channel in Microsoft Teams to notify the HR Recruitment team. The adaptive card will have a link to the Dataverse row which can be viewed in the **Hiring Agent**.

### ✨ Prerequisites to complete this mission

To complete this lab you will need to:

- **Have completed [Mission 01](../Lab%206/index.md) and [Mission 03](../Lab%208/index.md)** and have your Hiring Agent ready.
- You'll also need access to **Microsoft Teams** to complete the second lab exercise of posting an adaptive card to Microsoft Teams.

### 🧪 Lab 4.1 - Automate uploading resumes to Dataverse received by email

1. In the Hiring Agent, scroll down in the **Overview tab** to the **Triggers and Channels** section and select **+ Add**.

    ![Add trigger to agent](assets/03_addTrigger.png)

1. A list of triggers will appear. Select **When a new email arrives (V3)** and select **Next**.

    ![Select When a new email arrives (V3) trigger](assets/03_selectTrigger.png)

1. We'll now see the **Trigger name** and the **Sign in** connection references for the apps listed. Rename the trigger name to the following:

    ```text
    When a new email arrives from an applicant
    ```

    NOTE: Make sure you see a green check by each of the connection references for the apps listed.

1. The final step is to set the input properties of the trigger. Update the following properties:

     | Property | How to Set | Details |
     |----------|------------|---------|
     | **Include Attachments (Optional)** | Dropdown | Yes |
     | **Subject Filter (Optional)** | Type/Enter with keyboard | Application |
     | **Only with Attachments (Optional)** | Dropdown | Yes |

    Select **Create trigger**.

Continue with the remaining steps from the full lab to complete the event trigger and Teams notification setup.

## ✅ Mission Complete

Congratulations! 👏🏻 Excellent work, Operative.

✅ Event trigger: you've created an event trigger that passes Dataverse parameter values to an agent flow.
✅ Built an agent flow: consumes the Dataverse parameter values to post an adaptive card to a channel in Microsoft Teams to alert the HR recruitment team.
✅ Updated child agent instructions: to invoke the flow once the event trigger has completed.

This enables the **Hiring Agent** to work autonomously whenever resumes are received as email attachments and notify the HR recruitment team for manual review.

⏭️ Move to mission [**Understanding Agent Models**](../Lab%2010/index.md)

## 📚 Tactical Resources

📖 [Make your agent autonomous in Copilot Studio](https://learn.microsoft.com/training/modules/autonomous-agents-online-workshop/?WT.mc_id=power-188561-ebenitez)

📖 [Add an event trigger](https://learn.microsoft.com/microsoft-copilot-studio/authoring-trigger-event?WT.mc_id=power-188561-ebenitez)

📖 [Use agent flows with your agent](https://learn.microsoft.com/microsoft-copilot-studio/advanced-flow?WT.mc_id=power-188561-ebenitez)

📖 [Power Automate triggers introduction](https://learn.microsoft.com/power-automate/triggers-introduction?WT.mc_id=power-188561-ebenitez)

📖 [Using Power Automate flows with agents](https://learn.microsoft.com/microsoft-copilot-studio/advanced-flow-create?WT.mc_id=power-188561-ebenitez)

📖 [Data loss prevention for Copilot Studio](https://learn.microsoft.com/microsoft-copilot-studio/admin-data-loss-prevention?WT.mc_id=power-188561-ebenitez)

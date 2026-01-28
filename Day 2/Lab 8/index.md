---
prev:
  text: 'Authoring Agent Instructions'
  link: '/operative/02-agent-instructions'
next:
  text: 'Add Event Triggers'
  link: '/operative/04-automate-triggers'
---

# 🚨 Mission 03: Multi-Agent Systems

## 🕵️‍♂️ CODENAME: `OPERATION SYMPHONY`

> **⏱️ Operation Time Window:** `~45 minutes`

## 🎯 Mission Brief

Welcome back, Agent. In Mission 01, you built your main Hiring Agent giving you a solid foundation for managing recruitment workflows. But one agent can only do so much.

Your assignment, should you choose to accept it, is **Operation Symphony** - transforming your single agent into a **multi-agent system**: an orchestrated team of specialized agents that work together to handle complex hiring challenges. Think of it as upgrading from a solo operator to commanding a specialized task force.

Like a symphony orchestra where each musician plays their part in perfect harmony, you'll add two critical specialists to your existing Hiring Agent: an Application Intake Agent to process resumes automatically, and an Interview Prep Agent to create comprehensive interview materials. These agents will work together seamlessly under your main orchestrator.

## 🔎 Objectives

In this mission, you'll learn:

1. When to use **child agents** vs **connected agents**
1. How to design **multi-agent architectures** that scale
1. Creating **child agents** for focused tasks
1. Establishing **communication patterns** between agents
1. Building the Application Intake Agent and Interview Prep Agent

## 🧠 What are connected agents?

In Copilot Studio, you're not limited to building single, monolithic agents. You can create **multi-agent systems** - networks of specialized agents that work together to handle complex workflows.

Think of it like a real-world organization: instead of one person doing everything, you have specialists who excel at specific tasks and collaborate when needed.

### Why multi-agent systems matter

- **Scalability:** Each agent can be developed, tested, and maintained independently by different teams.
- **Specialization:** Agents can focus on what they do best. Perhaps one for data processing, another for user interaction, another for decision-making.
- **Flexibility:** You can mix and match agents, reuse them across projects, and evolve your system incrementally.
- **Maintainability:** Changes to one agent don't necessarily affect others, making updates safer and easier.

### Real-world example: Hiring process

Consider our hiring workflow - multiple agents might work together with the following responsibilities:

- **Resume intake** requires document parsing and data extraction skills
- **Scoring** involves evaluating candidate resumes and matching them to job requirements
- **Interview preparation** needs deep reasoning about candidate fit
- **Candidate communication** requires empathetic communication abilities

Rather than building one massive agent that tries to handle all these different skills, you can create specialized agents for each area and orchestrate them together.

## 🔗 Child agents vs connected agents: The key difference

Copilot Studio offers two ways to build multi-agent systems, each with distinct use cases:

### ↘️ Child agents

Child agents are **lightweight specialists** that live within your main agent. Think of them as specialized teams within the same department.

#### Key technical details

- Child agents live within the parent agent and have a single configuration page.
- Tools and Knowledge are **stored at the parent** agent, but configured to be "Available to" the child agent.
- Child agents **share the topics** of their parent agent. Topics can be referenced by the child agent instructions.
- Child agents **don't need separate publishing** - they're automatically available within their parent agent once created. This makes testing easier because changes to the parent and child agents can be performed in the **same shared workspace**.

#### Use child agents when

- A single team manages the entire solution
- You want to logically organize tools and knowledge into sub-agents
- You don't need separate authentication or deployment for each agent
- The agents won't be published separately or used independently
- You don't need to reuse agents across multiple solutions

**Example:** An IT helpdesk agent with child agents for:

- Password reset procedures
- Hardware troubleshooting
- Software installation guides

### 🔀 Connected agents

Connected agents are **full-fledged, independent agents** that your main agent can collaborate with. Think of them as separate departments working together on a project.

#### Key technical details

- Connected agents have **their own topics** and conversation flows. They operate independently with their own settings, logic, and deployment lifecycle.
- Connected agents **must be published** before they can be added to and used by other agents.
- During testing, changes to the connected agent must be published before they can be used by the calling agent.

#### Use connected agents when

- Multiple teams develop and maintain different agents independently
- Agents need their own settings, authentication, and deployment channels
- You want to publish and maintain agents separately with independent application lifecycle management (ALM) for each agent
- Agents should be reusable across multiple solutions

**Example:** A customer service system that connects to:

- A separate billing agent maintained by the finance team
- A separate technical support agent maintained by the product team
- A separate returns agent maintained by the operations team

> [!TIP]
> You can mix both approaches! For example, your main agent could connect to external agents from other teams while also having its own child agents for specialized internal tasks.

## 🎯 Multi-agent architecture patterns

When designing multi-agent systems, several patterns emerge based on how agents interact:

| Pattern           | Description                                                                                                                                                         | Best For                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Hub and Spoke** | A main orchestrator agent coordinates with multiple specialized agents. The orchestrator handles user interaction and delegates tasks to child or connected agents. | Complex workflows where one agent coordinates specialized tasks                                |
| **Pipeline**      | Agents pass work sequentially from one to the next, each adding value before passing to the next stage.                                                             | Linear processes like application processing (intake -> screening -> interview -> decision)    |
| **Collaborative** | Agents work together simultaneously on different aspects of the same problem, sharing context and results.                                                          | Complex analysis requiring multiple perspectives or expertise areas                            |

> [!TIP]
> You may even have a hybrid of two or more of these patterns.

## 💬 Agent communication and context sharing

When agents work together, they need to share information effectively. Here's how this works in Copilot Studio:

### Conversation history

By default, when a main agent calls a child or connected agent, it can pass along the **conversation history**. This gives the specialist agent full context about what the user has been discussing.

You can disable this for security or performance reasons - for example, if the specialist agent only needs to complete a specific task without needing the full conversation context. This can be a good defense against **data leakage**.

### Explicit instructions

Your main agent can give **specific instructions** to child or connected agents. For example: "Process this resume and summarize their skills for the Senior Developer role."

### Return values

Agents can return structured information back to the calling agent, allowing the main agent to use that information in subsequent steps or share it with other agents.

### Dataverse integration

For more complex scenarios, agents can share information through **Dataverse** or other data stores, allowing for persistent context sharing across multiple interactions.

## 🧪 Lab 3.1: Adding the Application Intake Agent

Ready to put theory into practice? Let's add our first child agent to your existing Hiring Agent.

### Prerequisites to complete this mission

To complete this mission you need to:

- **Have completed [Mission 01](../Lab%206/index.md)** and have your Hiring Agent ready

### 3.1.1 Solution setup

1. Inside Copilot Studio, select the ellipsis (...) below Tools in the left hand navigation.
1. Select **Solutions**.
    ![Select Solutions](./assets/2-select-solutions.png)
1. Locate your Operative solution, select the **ellipsis (...)** next to it, and choose **Set preferred solution**. Select **Apply** in the dialogue box that pops up. This will ensure that all your work will be added to this solution.
    ![Set Preferred Solution](./assets/2-select-preferred-solution.png)

### 3.1.2 Configure your Hiring Agent agent instructions

1. **Navigate** to Copilot Studio. Ensure your environment is selected in the top right **Environment Picker**.

1. Open your **Hiring Agent** from Mission 01

1. Select **Edit** in the **Instructions** section of the **Overview** tab of the agent.

    ![Edit Instructions](./assets/02-editinstructions.png)

    Copy and paste the following instructions in the instructions input:

    ```text
    You are the central orchestrator for the hiring process. You coordinate activities, provide summaries, and delegate work to specialized agents.
    ```

1. Select **Save**
    ![Hiring Agent Instructions](./assets/2-hiring-agent-instructions.png)

1. Select the **Settings** button in the top right of the screen

    ![Settings](./assets/02_settingsbtn.png)

1. Review the page and ensure the following settings are applied:

    | Setting | Value |
    | ------- | ----- |
    | Use generative AI orchestration for your agent's responses | **Yes** |
    | Deep Reasoning | **Off** |
    | Let other agents connect to and use this one | **On** |
    | Continue using retired models | **Off** |
    | Content Moderation | **Moderate** |
    | Collect user reactions to agent messages | **On** |
    | Use general knowledge | **Off** |
    | Use information from the Web | **Off** |
    | File uploads | **On** |
    | Code Interpreter | **Off** |

    ![Use Generative Orchestration](./assets/2-gen-orchestration.png)
    ![Moderation Setting](./assets/2-set-medium-moderation.png)

1. Click **Save**

    ![Knowledge and Web settings](./assets/2-settings-knowledge-web.png)

1. Click the **X** in the upper right hand corner to close out of the settings menu

    ![Close settings](./assets/02_closesettings.png)

### 3.1.3 Add the Application Intake child agent

1. **Navigate** to the **Agents** tab within your Hiring Agent (this is where you'll add specialist agents) and select **Add**.

    ![Add Button](./assets/02_agentsadd.png)

1. Select **New child agent**.

    ![Add Child Agent](./assets/02_newchildagent.png)

1. **Name** your agent ```Application Intake Agent```

1. Select **The agent chooses** - Based on description in the **When will this be used?** dropdown. These options are similar to the triggers that can be configured for topics.

1. Set the **Description** to be :

    ```text
    Processes incoming resumes and stores candidates in the system
    ```

    ![Application Intake Agent Description](./assets/02_agentnamedesc.png)

1. Expand **Advanced**, and set the Priority to be `10000`. This will ensure that later the Interview Agent will be used to answer general questions before this one. A condition could be set here as well such as ensuring that there is at least one attachment.

    ![Priority](./assets/02_priority.png)

1. Ensure that the toggle **Web Search** is set to **Disabled**. This is because we only want to use information provided by the parent agent.

1. Select **Save**

    ![Web Search](./assets/02_websearchdisabled.png)

### 3.1.4 Configure Resume Upload agent flow

Agents can't perform any actions without being given tools or topics.

We're using **Agent Flow tools** rather than Topics for the *Upload Resume* step because this multi-step backend process requires deterministic execution and integration with external systems. While Topics are best for guiding the conversational dialog, Agent Flows provide the structured automation needed to reliably handle file processing, data validation, and database upserts (insert new or update existing) without depending on user interaction.

1. Locate the **Tools** section inside the Application Intake Agent page.
   **Important:** This isn't the Tools tab of the parent agent, but can be found if you scroll down underneath the child agent instructions.

1. Select **+ Add**
   ![Add Tool](./assets/02_addtool.png)

1. Select **+ New tool** ![Add new tool](./assets/2-new-tool-2.png)

1. Select **Agent flow**.
    The Agent Flow designer will open, this is where we will add the upload resume logic.
    ![Add Agent Flow](./assets/2-add-agent-flow.png)

1. Select the **When an agent calls the flow** node, and select **+ Add an input**

    ![Add Input](./assets/02_flowaddinput.png)

1. Add inputs for each of the following Parameters listed in the table below. Select the appropriate input type as shown in the table and be sure to add both the name and the description. It's important to include the description because it will help the agent know what to fill in the input.

    | Type | Name            | Description                                                                                                                                                   |
    | ---- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | File | ```Resume```    | ```The Resume PDF file```                                                                                                                                     |
    | Text | ```Message```   | ```Extract a cover letter style message from the context. The message must be less than 2000 characters.```                                                   |
    | Text | ```UserEmail``` | ```The email address that the Resume originated from. This will be the user uploading the resume in chat, or the from email address if received by email.```  |

    ![Configure input parameters](./assets/2-upload-resume-trigger.png)

Continue with the remaining steps from the full lab instructions to complete the multi-agent system setup.

## 🎉  Mission Complete

Excellent work, Agent! **Operation Symphony** is now complete. You've successfully transformed your single Hiring Agent into a sophisticated multi-agent orchestra with specialized capabilities.

Here's what you've accomplished in this mission:

**✅ Multi-agent architecture mastery**
You now understand when to use child agents vs connected agents and how to design systems that scale.

**✅ Application Intake child agent**
You've added a specialized child agent to your Hiring Agent that processes resumes, extracts candidate data, and stores information in Dataverse.

**✅ Interview Prep connected agent**
You've built a reusable connected agent for interview preparation and successfully connected it to your Hiring Agent.

**✅ Agent communication**
You've seen how your main agent can coordinate with specialist agents, share context, and orchestrate complex workflows.

**✅ Foundation for autonomy**
Your enhanced hiring system is now ready for the advanced features we'll add in upcoming missions: autonomous triggers, content moderation, and deep reasoning.

🚀**Next up:** In your next mission, you'll learn how to configure your agent to autonomously process resumes from emails!

⏩ Move to [Mission 04](../Lab%209/index.md): Automate your agent with triggers

## 📚 Tactical Resources

📖 [Add other agents (preview)](https://learn.microsoft.com/microsoft-copilot-studio/authoring-add-other-agents?WT.mc_id=power-182762-scottdurow)

📖 [Add tools to custom agents](https://learn.microsoft.com/microsoft-copilot-studio/advanced-plugin-actions?WT.mc_id=power-182762-scottdurow)

📖 [Work with Dataverse in Copilot Studio](https://learn.microsoft.com/microsoft-copilot-studio/knowledge-add-dataverse?WT.mc_id=power-182762-scottdurow)

📖 [Agent flows overview](https://learn.microsoft.com/microsoft-copilot-studio/flows-overview?WT.mc_id=power-182762-scottdurow)

📖 [Create a solution](https://learn.microsoft.com/power-platform/alm/solution-concepts-alm?WT.mc_id=power-182762-scottdurow)

📖 [Power Platform solution ALM guide](https://learn.microsoft.com/power-platform/alm/overview-alm?WT.mc_id=power-182762-scottdurow)

📺 [Agent-to-agent collaboration in Copilot Studio](https://youtu.be/d-oD3pApHAg?si=rwIHKhJTkjSvhTHw)

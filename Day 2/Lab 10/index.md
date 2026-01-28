---
prev:
  text: 'Add Event Triggers'
  link: '/operative/04-automate-triggers'
next:
  text: 'AI Safety and Content Moderation'
  link: '/operative/06-ai-safety'
---

# 🚨 Mission 05: Understanding Agent Models

## 🕵️‍♂️ CODENAME: `OPERATION ARCHETYPE`

> **⏱️ Operation Time Window:** `~45 minutes`

## 🎯 Mission Brief

Welcome back, Agent. In [Mission 02](../Lab%207/index.md), you learned how strong instructions shape agent behavior.

Now it's time to choose the brain.

In **Operation Archetype**, you'll learn how to select the right AI model for your agent and how to test model changes to see the impact on response quality, structure, and depth. Different models can respond faster or slower, be more concise or more detailed, and handle complex reasoning differently.

By the end of this mission, you'll be able to confidently choose a model based on your scenario and validate that choice by comparing results.

## 🔎 Objectives

In this mission, you'll learn:

1. How to understand and select the optimal AI model for your agent's use case
1. How to compare different model capabilities and performance characteristics
1. How to switch your agent's model
1. How to test and evaluate differences in output when you change models

## 🤔 What is the Agent Model?

The _agent model_ is the underlying generative AI engine powering your Copilot agent's responses. Copilot Studio lets you select which model your agent uses, enabling you to leverage different strengths (speed, output quality, cost, etc.) depending on your scenario. The model you choose determines how your agent thinks and responds, for example, one model may respond faster, another may produce more detailed answers, while another might excel at complex reasoning.

### 🎭 Why it matters

Selecting the appropriate model ensures your agent performs optimally for your use case. Each available model has distinct capabilities and specializations, so aligning the model with your requirements (such as quick replies vs. deep analysis) can improve user satisfaction and manage costs.

### 🪁 Available models

Copilot Studio supports OpenAI models and Anthropic models. Each model will have a category tag and an availability tag.

#### Model use categories

Different models are designed for specific tasks. Selecting the right model improves your agent's performance. For instance, use a Deep model for complex decision-making or a General model for broad, conversational topics.

| Tag | Description | Strengths | Latency | Cost | Reasoning depth |
| ------- | ---------- | ---------- | ------------- | ----------- | ----------- |
| **Deep** | Optimized for deliberate, multi-step reasoning and tool-supported workflows. | Complex analytics, multi-hop reasoning, policy and contract analysis, troubleshooting with multi-system steps, and synthesis of long documents with citations | Highest | Highest | Multi-step, tool-rich |
| **Auto** | Optimized for coverage across mixed workloads; routes queries dynamically. | Helpdesk and employee agents with mixed intents, blending knowledge and actions, and tier‑0 customer support with unpredictable complexity | Variable | Variable | Multi-step, tool-rich |
| **General** | Optimized for speed and cost on everyday chat and light grounding. | Drafting, rewriting, summarizing, and translation, FAQ-style grounded answers, and simple action automation | Lowest | Lowest | Shallow-to-moderate |

#### Model availability

Models are released in stages. You can explore cutting-edge options like Experimental or Preview models, or stick with a stable, fully tested Generally Available model.

| Tag | Description |
| ----- | ------------- |
| **Experimental** | Used for experimentation, and not recommended for production use. Subject to preview terms, and can have limitations on availability and quality. |
| **Preview** | Will eventually become a generally available model, but currently not recommended for production use. Subject to preview terms, and can have limitations on availability and quality. |
| **No tag** | Generally available. You can use this model for scaled and production use. |
| **Default** | The default model for all agents, and usually the best performing generally available model. The default model is periodically upgraded as new, more capable models become generally available. |
| **Retired** | When a new model becomes the default model, the old default model is retired. You can still use the retired model for up to one month after retirement. |

#### OpenAI models

AI capabilities evolve rapidly, and Copilot Studio keeps up by offering a range of Azure OpenAI models. As of 2025, the primary models to choose from include OpenAI's GPT-4.1, and the latest GPT-5 previews.

| Model Version | Category | Availability | Key Strengths | Ideal Use Cases |
| ------- | ---------- | ---------- | ------------- | ----------- |
| **GPT‑4o** | General | Retired | Fast, versatile responses; supports text and image input; cost-effective balance of speed and accuracy. | Routine Q&A; summarizing support chats or calls; quick content drafts; tasks combining text with visuals. |
| **GPT-4.1** | General | Default | Higher accuracy and reasoning than GPT-4o; excellent at complex text analysis (text-only model). | Analyzing detailed documents (policies, reports); complex knowledge-base Q&A; scenarios where precision is critical. |
| **GPT‑5 Chat** | General | Preview | Advanced conversational abilities with strong context retention; produces human-like dialogue. | Employee self-service chatbots; IT/HR helpdesk assistants; interactive agents requiring natural, human-like responses. |
| **GPT‑5 Auto** | Auto | General | Optimized for orchestrating multi-step workflows; can automate actions across systems (not just chit-chat). | End-to-end process automation (e.g. ticket creation to resolution); multi-step task sequences across apps; "digital project manager" scenarios. |
| **GPT‑5 Reasoning** | Deep | Preview | Latest model optimized for complex reasoning (trained up to Oct 2024) - High scores in document understanding and response accuracy | Advanced reasoning tasks where top-tier analytical capability is required (such as extensive planning, interpreting complex data). |
| **GPT‑5.1 Chat** | General | Experimental | Latest experimental conversational model with broad task proficiency; improves on context awareness and responsiveness. | General-purpose Q&A and dialogue tasks leveraging the newest model's capabilities; versatile chatbot scenarios where enhanced performance is beneficial. |
| **GPT‑5.1 Reasoning** | Deep | Experimental | Experimental top-tier reasoning model offering maximum depth and accuracy for complex tasks. | Ultra-complex analytical queries or decision support requiring the highest precision (e.g. intricate strategic planning, high-stakes data analysis). |

> [!WARNING]
>
> - Experimental/preview models (like GPT-5 Chat) are accessible for testing new capabilities before they're production-ready. They may have limited testing and higher variability in performance.
> - They are not recommended for production use because of possible instability (variable quality, latency, or even time-outs). Always review any _Preview_ model's limitations and consider using them only in non-critical environments.

#### Anthropic models (external)

Currently there are two Anthropic models which are currently under Preview, they are accessible in early release environments.

- **Claude Sonnet 4.5** is Anthropic's newest, coding and agent-focused model.
- **Claude Opus 4.1** is a reasoning-focused model.

| Model Version | Status | Key Strengths | Ideal Use Cases |
| ------- | ---------- | ------------- | ----------- |
| **Claude Sonnet 4.5** | Experimental | Excels at code-related tasks and complex "agent" workflows; strong at tool use and step-by-step reasoning. | Advanced software development assistance (code generation & debugging); building multi-step autonomous agents; tasks requiring integration with external tools or systems. |
| **Claude Opus 4.1** | Experimental | Specialized for intensive analysis and structured problem-solving. | In-depth data analysis and research projects; complex reasoning scenarios (e.g. compliance auditing, elaborate planning) where thoroughness is paramount. |

> [!WARNING]
>
> - It's important to note that these are external models. Anthropic models are hosted outside Microsoft and are subject to Anthropic terms and data handling, which need to be reviewed and accepted before makers can use them.

### 🔧 Changing and updating the model of your agent

By default, a new Copilot agent starts on the GPT-4o model, which is optimized as a balanced choice for most scenarios.

You can switch the agent's primary model anytime via the agent's **Settings** page ➡️ **Model** section in the **Generative AI** tab, using a simple dropdown to pick from available models.

![Agent models available](./assets/5.0_01_AgentModels.png)

This flexibility allows you to experiment with different models even after your agent is built.

## 🔐 Admin controls for AI model selection

It's worth noting that not every copilot environment allows all model choices by default. There are organization-level settings that tenant administrators control:

- **Enable Anthropic models to be used within your organization**: An admin with the **Global administrator** role needs to enable (allow) anthropic models in the Microsoft 365 Admin Center.

- **Allow Preview (Experimental) models to be used in Copilot Studio environments**: An admin can toggle whether preview and experimental AI models are available in a given environment.

- **Move data across regions**: Because experimental models may not run in the same regional data centers as standard models, enabling them often requires allowing cross-region data movement.

| Admin Setting | Effect on Model selection | Setting location |
| ---------- | ------------ | ------------ |
| **Allow Anthropic models** | When **Allowed**, users can connect to the Anthropic external models for agents built in Copilot Studio. | Microsoft 365 Admin Center |
| **Allow Preview & Experimental Models** | When **ON**, makers can choose preview/experimental AI models for their agents. | Power Platform admin center |
| **Move Data Across Regions** | Required to be **ON** if experimental models are enabled. | Power Platform admin center |

## 🧪 Lab 05 - Model selection for the Interview Agent

In this lab, you'll compare responses from two different models by asking the same questions and observing differences in:

- Depth
- Structure
- Tone
- Specificity

Let's compare the responses of the GPT-4.1 default model with the GPT 5.1 Chat experimental model.

1. Start a new test session in the **Hiring Agent** and enter the following question below. Use a **Resume Number** value from your existing active resumes in the **Hiring Hub** model-driven app.

    ```text
    Summarize resume RXXXXX
    ```

    ![Enter first question for GPT-4.1 default model](assets/5.1_01_GPT-4.1DefaultModel.png)

1. A summary of the resume will next be displayed and we can see it's in the output of bullet points by headings.

1. We'll ask another question for suggestions of interview questions to ask based on the evaluation criteria of a job role. Enter the question below.

    ```text
    Can you provide suggestions of questions to ask in an interview for the Power Platform developer role (Job role number J1004) based on its associated evaluation criteria? Can you also please provide what the answers may be for each question?
    ```

1. The returned response lists interview questions in numbered format. Each question is followed by a `Model Answer`. Notice how the answer is in the point of view of the candidate.

1. Let's now change the agent's model. In the **Overview** tab select the **chevron** icon and from the list of **OpenAI** models, select **GPT-5.1 Chat**.

    ![Select GPT-5.1 Chat](assets/5.1_05_SelectGPT-5.1Chat.png)

1. A confirmation message will appear shortly to inform you that the agent model has been updated. Let's now test the responses of this model by starting a new test session.

1. Enter the same questions and compare the responses. Notice how the GPT-5.1 Chat model:
    - Provides shorter, more concise responses
    - Organizes output under main headers and subsections
    - Uses different formatting like "Strong Answer Indicators"

## ✅ Mission Complete

Congratulations! 👏🏻 Excellent work, Operative.

You learned about the differences in the available models and how it affects your agent output. This enables the **Interview Agent** to be equipped in answering questions and inquiries using the power of the selected model.

## 📚 Tactical Resources

📖 [Multi-agent orchestration and more: Copilot Studio announcements](https://www.microsoft.com/microsoft-copilot/blog/copilot-studio/multi-agent-orchestration-maker-controls-and-more-microsoft-copilot-studio-announcements-at-microsoft-build-2025/#copilot-studio-enhancements)

📖 [Choose an external model as the primary AI model](https://learn.microsoft.com/microsoft-copilot-studio/authoring-select-external-response-model?WT.mc_id=power-188561-ebenitez)

📖 [Connect to Anthropic's AI models](https://learn.microsoft.com/copilot/microsoft-365/connect-to-ai-models?WT.mc_id=power-188561-ebenitez)

📖 [Allow external large language models (LLMs) for generative responses](https://learn.microsoft.com/power-platform/admin/allow-llm-generative-responses?WT.mc_id=power-188561-ebenitez)

📖 [Move data across regions for Copilots and generative AI features](https://learn.microsoft.com/power-platform/admin/geographical-availability-copilot?tabs=new#copilots-and-generative-ai-features-that-depend-on-data-movement-across-regions?WT.mc_id=power-188561-ebenitez)

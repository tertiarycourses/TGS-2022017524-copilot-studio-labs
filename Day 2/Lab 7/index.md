---
prev:
  text: 'Get Started with the Hiring Agent'
  link: '/operative/01-get-started'
next:
  text: 'Multi-Agent Systems'
  link: '/operative/03-multi-agent'
---

# 🚨 Mission 02: Authoring Agent Instructions

## 🕵️‍♂️ CODENAME: `OPERATION CLEAR DIRECTIVE`

> **⏱️ Operation Time Window:** `~30 minutes – intel only, no fieldwork required`

## 🎯 Mission Brief

Welcome back, Agent. In Mission 01, you deployed your Hiring Agent - but an agent without clear instructions is like a soldier without orders. In this mission, you'll learn the art of writing effective instructions that shape how your agent thinks, responds, and behaves.

Strong instructions are the foundation of reliable agent behavior. They determine which tools your agent uses, how it populates inputs, and how it formulates responses to users. Master this skill, and your agents will operate with precision.

## 🔎 Objectives

In this mission, you'll learn:

1. Why instructions matter for agent behavior and decision-making
1. How to write clear, effective instructions that guide your agent
1. Best practices for tool descriptions and when to use them
1. How to structure instructions for multi-agent scenarios
1. Testing and refining your instructions for optimal performance

## 🧠 Why Instructions Matter

Instructions are the core guidance system for your agent. They tell your agent:

- **What role to play** - Define the agent's persona and expertise area
- **How to respond** - Set the tone, format, and level of detail
- **When to use tools** - Guide the agent on which tools to call and when
- **What boundaries to respect** - Establish guardrails and topic restrictions
- **How to handle edge cases** - Provide guidance for ambiguous situations

> [!IMPORTANT]
> Instructions must be grounded in the tools, topics, and knowledge sources configured for your agent. You can't instruct an agent to do something if it doesn't have the capability to do it.

## 📝 Essential Components of Instructions

When authoring agent instructions, include these key elements:

### 1. Role Definition

Start by clearly defining who the agent is:

```text
You are the central orchestrator for the hiring process. You coordinate activities, provide summaries, and delegate work to specialized agents.
```

### 2. Tool Selection Guidance

Direct agents toward appropriate resources using `/` references:

```text
When a user uploads a resume, use the /Resume Upload tool to process it.
```

### 3. Input Hints

Specify how to populate tool parameters based on available context:

```text
Extract a cover letter style message from the context. The message must be less than 2000 characters.
```

### 4. Response Formatting

Dictate output structure for consistency:

```text
Always format job application summaries as:
- Candidate Name
- Applied Position
- Key Qualifications (bullet points)
- Recommendation
```

### 5. Behavioral Constraints

Establish guardrails limiting scope or topics:

```text
Never contact candidates directly. All candidate communication must go through the HR team.
```

## 📋 Description Best Practices

Quality descriptions enable proper tool selection. When writing descriptions for tools, topics, and agents:

| Do | Don't |
|---|---|
| Use straightforward, jargon-free language | Use technical terms users won't recognize |
| Write in active voice | Write in passive voice |
| Keep it concise (1-2 sentences) | Write lengthy paragraphs |
| Include keywords matching user intent | Use vague, generic descriptions |
| Use distinct, specific names | Use similar names that could overlap |
| Test to prevent overlap | Assume descriptions won't conflict |

### Good Description Examples

```text
Processes incoming resumes and stores candidates in the system
```

```text
Generates interview questions based on job requirements and candidate background
```

### Poor Description Examples

```text
This tool can answer questions
```

```text
Handles stuff related to hiring
```

## 🏗️ Structural Framework

Effective instructions follow this pattern:

1. **Overview of agent role** - Who is this agent and what's its purpose?
2. **Sequential process steps** - What steps should the agent follow?
3. **Inter-agent collaboration points** - When should it hand off to other agents?
4. **Safety/compliance requirements** - What must it always/never do?
5. **Feedback and escalation mechanisms** - How should it handle failures?

### Example Instruction Structure

```text
You are the Application Intake Agent. Your role is to process incoming resumes and create candidate records.

Process for Resume Upload via Chat:
1. Upload Resume
   - Trigger only if /System.Activity.Attachments contains exactly one new resume
   - If more than one file, instruct the user to upload one at a time and stop
   - Call /Upload Resume once. Never upload more than once for the same message

2. Post-Upload
   - Always output the [ResumeNumber] (R#####)
   - Confirm successful processing to the user

Constraints:
- Only process PDF files
- Never modify existing candidate records without explicit instruction
- Escalate to the Hiring Agent if unsure about job role matching
```

## ✅ Testing Your Instructions

After writing instructions, always test them:

1. **Open the Test pane** in Copilot Studio
2. **Try various scenarios** - happy path, edge cases, error conditions
3. **Check the Activity Map** to see which tools and agents were invoked
4. **Refine instructions** based on unexpected behavior
5. **Repeat** until behavior is consistent

> [!TIP]
> If the agent isn't calling the expected tool, check your tool descriptions for overlap or ambiguity. The agent selects tools based on how well descriptions match the user's intent.

## 🎉 Mission Complete

You've now learned the fundamentals of authoring agent instructions. These skills will be essential as you build more complex multi-agent systems in the upcoming missions.

Key takeaways:
- ✅ Instructions shape every aspect of agent behavior
- ✅ Clear role definitions prevent confusion
- ✅ Tool descriptions must be specific and distinct
- ✅ Structured instructions improve consistency
- ✅ Testing reveals gaps and opportunities for refinement

Next up is [Mission 03](../Lab%208/index.md): Multi-Agent Systems - where you'll put these instruction skills to work coordinating multiple specialized agents!

## 📚 Tactical Resources

📖 [Write effective agent instructions](https://learn.microsoft.com/microsoft-copilot-studio/authoring-agent-instructions)

📖 [Best practices for topic descriptions](https://learn.microsoft.com/microsoft-copilot-studio/guidance/topic-descriptions-best-practices)

📖 [Test your agent](https://learn.microsoft.com/microsoft-copilot-studio/authoring-test-bot)

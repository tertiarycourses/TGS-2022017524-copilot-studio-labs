# Lab 4: Create Your First Copilot Studio Agent

## Lab Title
Create, Configure, and Test Your First Business Agent

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a new agent in Copilot Studio
2. Write clear **instructions** that shape the agent's behavior
3. Add a simple **knowledge** source so the agent can answer questions
4. Test the agent in the built-in **test pane**
5. Publish the agent (optional)

## Prerequisites
- Completed [Lab 0](../../Day%201/Lab%200%20-%20Environment%20Setup/index.md) (Copilot Studio trial active)
- Read [Module 3](../Module%203%20-%20Business%20Agents%20Concepts.md)
- Signed in at https://copilotstudio.microsoft.com (same environment as Power Automate)

## Scenario
You'll build a friendly **Company Helpdesk** agent that answers basic questions about a fictional company. This teaches the Copilot Studio interface before you build data-capturing agents in Labs 5–6.

---

## Step-by-Step Guide

### Step 1: Create the agent (~10 minutes)
1. Go to **https://copilotstudio.microsoft.com** and confirm the **environment** (top-right) matches the one from Lab 0.
2. In the left menu, select **Create** → **New agent**.
3. Copilot Studio may open a **conversational setup** ("Describe your agent"). You can either chat to describe it, or select **Skip to configure** to fill the form directly. Choose **Skip to configure**.
4. Fill in:
   - **Name:** `Company Helpdesk`
   - **Description:** `Answers general questions about ACME Pte Ltd for staff and customers.`
   - **Instructions:** paste the following:
     ```
     You are the Company Helpdesk agent for ACME Pte Ltd.
     Be friendly, concise, and professional.
     Answer questions about our products, opening hours, and contact details.
     If you do not know an answer, politely say so and suggest emailing help@acme.example.
     Keep replies to 2-3 sentences.
     ```
5. Select **Create**. The agent's overview page opens.

> **Instructions** are the heart of the agent — they tell the AI how to behave. Clear instructions = predictable agent.

### Step 2: Explore the agent workspace (~5 minutes)
Across the top you'll see tabs (the exact labels may vary slightly by version):
- **Overview** — summary and quick settings
- **Knowledge** — documents/websites the agent can use
- **Topics** — scripted conversation flows
- **Tools / Actions** — flows and connectors the agent can call
- **Test** (right side panel) — chat with your agent as you build

Spend a minute clicking through these tabs.

### Step 3: Add a knowledge source (~10 minutes)
Give the agent something to answer from.

1. Open the **Knowledge** tab → **Add knowledge**.
2. The simplest option is a **public website**. Choose **Public website** and enter a relevant URL, e.g. your company site or `https://learn.microsoft.com/microsoft-copilot-studio/`.
   - *Alternatively*, upload a short PDF or Word doc with company FAQs (e.g. opening hours, contact email).
3. Select **Add**. Wait for the source status to show **Ready**.

> Knowledge lets the agent ground its answers in real content instead of guessing.

### Step 4: Test the agent (~10 minutes)
1. Open the **Test** pane (right side). If it's not visible, select **Test** at the top-right.
2. Type a few questions:
   - `What can you help me with?`
   - `What are your opening hours?`
   - `How do I contact support?`
3. Observe how the agent uses your **instructions** (tone, length) and **knowledge** (facts).
4. If a reply is off, refine the **Instructions** (Step 1) and select **Save**, then re-test. Iterating on instructions is normal.

> **Tip:** Use the **Activity / Activity map** (if shown) to see *why* the agent answered the way it did.

### Step 5: Publish the agent (optional) (~5 minutes)
1. Select **Publish** (top-right) → **Publish**.
2. After publishing, open the **Channels** tab to see where it can be deployed (Teams, a demo website, etc.). You don't need to deploy it now — publishing simply makes the latest version live for testing.

---

## Checkpoint
- ✅ An agent named **Company Helpdesk** with custom instructions
- ✅ At least one **knowledge** source marked **Ready**
- ✅ Sensible answers in the **Test** pane

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Agent ignores instructions | Make instructions specific and **Save**; re-open the Test pane (refresh it). |
| Knowledge source stuck "processing" | Wait a minute; very large sites take longer. Try a smaller page or a PDF. |
| Generic / unhelpful answers | Add a knowledge source and tighten the instructions. |
| Wrong environment | Switch environment (top-right) so it matches your Power Automate flows. |

## Key Takeaways
- An agent is shaped mainly by its **instructions**.
- **Knowledge** grounds answers in real content.
- The **Test pane** is your build-and-iterate loop.

## Duration
~35 minutes

## Next Steps
Proceed to [Lab 5: Sales Enquiry Assistant](../Lab%205%20-%20Sales%20Enquiry%20Assistant/index.md).

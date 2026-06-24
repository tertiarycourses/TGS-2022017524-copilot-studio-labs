# Lab 8: Add Tools and Actions to Your Agent

## Lab Title
Give Your Agent Tools — Connectors, Prebuilt Actions, and Flows

## Lab Objectives
By the end of this lab, you will be able to:
1. Explain what **Tools/Actions** are and how they differ from **Knowledge**
2. Add a **prebuilt connector action** as a tool (e.g. Send an email V2) and create its connection
3. Write a clear tool **name and description** that tells the agent *when* to use the tool
4. Set tool **inputs**, either as fixed values or filled by AI from the conversation
5. (Alternative) Add a **Power Automate flow** as a tool
6. Test the agent actually **performing an action**, and read the **Activity map**

## Prerequisites
- Completed [Lab 6](../Lab%206%20-%20Create%20Your%20First%20Agent/index.md) and [Lab 7](../Lab%207%20-%20Add%20Knowledge%20to%20Your%20Agent/index.md)
- A working **Office 365 Outlook** connection (a mailbox-enabled account you can sign in with)

## Scenario
So far your **Company Helpdesk** agent can *answer* questions (using Knowledge). But staff at **ACME Pte Ltd** also want it to *do* things — for example, email the support team when someone needs help escalated.

**Knowledge lets an agent answer; Tools let it act.** In this lab you will give your agent a tool so a chat conversation can trigger real work, such as sending an email. This is the bridge to the end-to-end agent-plus-flow workflows you will build in Day 3.

> **Knowledge vs Tools:**
> - **Knowledge** = read and answer from your documents (Lab 7).
> - **Tools/Actions** = perform actions in other systems — send an email, create a record, run a Power Automate flow (this lab).

---

## Step-by-Step Guide

### Step 1: Open the Tools tab (~5 minutes)

1. Go to **https://copilotstudio.microsoft.com** and confirm the **environment selector** (top-right) shows **NUS Copilot Sandbox** — the same environment as your Power Automate flows.
2. Open your **Company Helpdesk** agent from Lab 6.
3. Select the **Tools** tab (in some versions this is labelled **Actions**).
4. Select **+ Add a tool**. You will see options grouped by type, such as:
   - **Connector** / **Prebuilt action** — ready-made actions from connectors like Office 365 Outlook, Excel, Teams.
   - **Flow** — a Power Automate flow you build or already have.
   - **Prompt** — an AI prompt that returns text.

> **⚠️ Warning:** Tools and the flows they call must live in the **same environment** as the agent. If your flow was built in a different environment, the agent will not be able to see or call it.

### Step 2: Add a prebuilt connector action (~10 minutes)

You will add a "send an email" action directly as a tool.

1. Select **+ Add a tool**, then choose **Connector** (or **Add an action**).
2. In the search box, type `Send an email` and select **Send an email (V2)** under **Office 365 Outlook**.
3. If you are prompted to **sign in / create a connection**, do so now using a **mailbox-enabled account** (an account that can actually send email). Approve any consent prompt.
4. The action is added to your tools list. Open it to see its **inputs**: **To**, **Subject**, and **Body**.

> **⚠️ Warning:** If you ever see an **Unauthorized** error when the tool runs, the connection is broken or signed in with the wrong account. Open the tool's **connection** settings and **reconnect** with a mailbox-enabled account.

### Step 3: Name and describe the tool (~5 minutes)

The description is the most important part — it is how the agent decides **when** to call this tool.

1. Open the tool and set a clear **name** and **description**, for example:
   - **Name:** `Send notification email`
   - **Description:** `Use this to email a summary to the support team when the user asks to escalate an issue or notify someone.`
2. Be specific. A vague description like `sends email` makes the agent unsure when to use it; a precise description makes it reliable.

> **Tip:** The agent reads the tool **description** the way you would read a label. If the label clearly says what the tool is for, the agent picks it at the right moment.

### Step 4: Configure the tool's inputs (~7 minutes)

Decide how each input (To, Subject, Body) gets its value. You have two choices per input:

1. **Fixed value** — you type the value once and it never changes. Good for **To**: set it to your own email so test messages go to you, e.g. `you@yourcompany.com`.
2. **Filled by AI** (dynamic) — the agent fills the value from the conversation. Choose **Fill using AI** (or **Dynamically**) for **Subject** and **Body** so the agent writes them based on what the user said.

> **Tip:** For your first test, set **To** as a **fixed** value (your own inbox). That way you can confirm the email actually arrives without risking sending it to the wrong person.

### Step 5: (Alternative path) Add a Power Automate flow as a tool (~10 minutes)

A single connector action is fine for one step. For **multi-step** work (e.g. log a row *and* email *and* post to Teams), use a Power Automate flow instead.

1. Select **+ Add a tool**, then choose **New Agent flow** (or pick an existing flow).
2. Power Automate opens with the trigger **When an agent calls the flow** already in place.
3. Add the **inputs** the agent will pass to the flow — for example a text input named `summary`.
4. Add the actions the flow should perform (for example **Send an email (V2)**, or **Add a row** to a table).
5. Add a **Respond to the agent** action at the end and return a result, for example a `status` of `Done`.
6. **Save** and **Publish** the flow, then return to the agent. Map the flow's inputs to conversation values (fixed or filled by AI), just like in Step 4.

> **Tip:** Every flow used as a tool follows the same three-part shape: **When an agent calls the flow** (trigger) → do the work → **Respond to the agent** (give a result back). You will reuse this pattern throughout Day 3.

### Step 6: Test the agent performing the action (~8 minutes)

1. Open the **Test** pane and select **Refresh** at the top so it picks up the new tool.
2. Type a message that should trigger the tool, for example:
   - `Please email the support team that I need help with order 123.`
3. Watch the agent decide to **call the tool**. If it asks for confirmation or shows a connection prompt, approve it.
4. Confirm the action really happened — check that the email arrived in the inbox you set in Step 4.
5. Open the **Activity map** (a diagram of the conversation, if shown) to see the tool being called and the exact data that was passed into it. This is the best way to understand *why* the agent did what it did.

> **Tip:** If the email does not arrive, check three things in order: the connection (Unauthorized?), the **To** address, and whether the agent actually chose the tool (look at the Activity map).

### Step 7: Refine the tool (~5 minutes)

1. **Agent never calls the tool?** Improve the tool **description** to clearly state the trigger situations, and add an example trigger phrase in the agent's **Instructions** (e.g. *"When a user asks to notify or escalate, use the Send notification email tool."*).
2. **Agent calls the tool with the wrong data?** Tighten the input setup — use a fixed value where the data should never change, or add a clearer hint for the AI-filled inputs.
3. **Save**, refresh the Test pane, and test again.

---

## Checkpoint
You have successfully completed this lab when:
- ✅ A **tool** (a connector action and/or a flow) is added to your agent
- ✅ The tool has a clear **name and description** that tells the agent when to use it
- ✅ The tool's **connection** is signed in with a mailbox-enabled account (no Unauthorized error)
- ✅ The agent **performs the action** during a test conversation (e.g. the email arrives)
- ✅ You found the tool call in the **Activity map**

## Troubleshooting
| Problem | Cause | Solution |
|---------|-------|----------|
| Agent never calls the tool | Description too vague | Rewrite the **description** to name the exact situations; add a trigger example in **Instructions**. |
| Connection / Unauthorized error | Broken connection or wrong account | Open the tool's connection and **reconnect** with a **mailbox-enabled** account. |
| Email never arrives | Wrong recipient or tool not called | Check the **To** value, confirm the connection, and verify the tool ran in the **Activity map**. |
| Wrong data sent to the tool | AI filled inputs incorrectly | Use **fixed values** where data shouldn't change, or add clearer input hints; test again. |
| Tool not listed after adding | Wrong environment, or not refreshed | Confirm the agent and flow are in the **same environment** (NUS Copilot Sandbox); refresh the page. |
| Flow tool fails to return | No response step | Make sure the flow ends with **Respond to the agent**, then re-publish it. |

## Key Takeaways
- **Tools/Actions** let an agent *act* — using connectors, prebuilt actions, or full Power Automate flows.
- The tool **description** is what makes the agent call the right tool at the right time — write it carefully.
- Inputs can be **fixed** or **filled by AI** from the conversation; use fixed values for anything that must not change.
- A flow used as a tool always goes **When an agent calls the flow → do the work → Respond to the agent**.
- A broken connection causes an **Unauthorized** error — reconnect with a mailbox-enabled account.
- Flows-as-tools are the foundation of the end-to-end workflows you build in Day 3.

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 9: Sales Enquiry Assistant](../Lab%209%20-%20Sales%20Enquiry%20Assistant/index.md).

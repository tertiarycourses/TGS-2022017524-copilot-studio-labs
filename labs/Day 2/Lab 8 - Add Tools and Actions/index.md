# Lab 8: Add Tools and Actions to Your Agent

## Lab Title
Give Your Agent Tools — Connectors, Prebuilt Actions, and Flows

## Lab Objectives
By the end of this lab, you will be able to:
1. Explain what **Tools/Actions** are and how they differ from **Knowledge**
2. Add a **prebuilt connector action** as a tool (e.g. Send an email V2) and create its connection
3. Write a clear tool **name and description** that tells the agent *when* to use the tool
4. Set tool **inputs**, either as fixed values or filled by AI from the conversation
5. (Alternative) Add a **multi-step Power Automate agent flow** as a tool (using **Add a row into a table**), and **disable a competing tool** so the agent calls the right one
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
4. Select **+ Add a tool**. Microsoft groups tools into several **core tool types**:
   - **Prebuilt / custom connector action** — a single ready-made operation from a connector like Office 365 Outlook, Excel, or Teams (you use this in Steps 2–4).
   - **Agent flow** — a multi-step Power Automate flow with conditions and logic, used as one tool (you use this in Step 5).
   - **Prompt** — a single-turn AI prompt that returns text.
   - **REST API / MCP tool / Computer use** — connect to web services, a Model Context Protocol server, or GUI automation (advanced; out of scope here).

> **How the agent picks a tool:** With **generative orchestration**, the agent chooses *which* tool to call at runtime **based purely on each tool's name and description** — there are no fixed trigger phrases. That is why a clear, intent-rich **description** (Step 3) is the single most important thing you write, and why two tools with overlapping descriptions confuse the agent (see Step 5a).

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

### Step 5: (Alternative path) Add a Power Automate flow as a tool (~15 minutes)

A single connector action (Steps 2–4) is perfect for **one** step. But real business work is usually **multi-step** — you often need to *log a record* **and** *notify someone* **and** *return a result* in one go. A single connector tool cannot do that; a **Power Automate agent flow** can. In this step you will build a flow that **logs a support request to a table**, then add that flow to the agent as a second tool.

> **Why a different action here?** In Steps 2–4 your agent already learned to *send an email* with a single connector tool. To show what a flow adds, this step uses a **different** action — **Add a row into a table** — so the flow *records* the request instead of emailing it. (Do **not** add another *Send an email* action here; that would just duplicate the tool you already built and confuse the agent about which one to call.)

#### Step 5a — Turn OFF the connector tool from Step 4 first (do not skip)

If you leave the **Send notification email** connector tool (Steps 2–4) **enabled** while you add and test the new flow tool, your agent now has **two** tools that both look like "do something with the user's request." The orchestrator may keep choosing the old email tool and never call your new flow — making it look like the flow is broken when it is not. Disable the old tool so this exercise has exactly **one** active tool to reason about.

1. In your agent, open the **Tools** tab.
2. Find the **Send notification email** tool you added in Steps 2–4.
3. Select its **… (More actions)** menu and turn the tool **Off** (toggle/disable it). *Do not delete it* — you will switch it back on later.
4. Confirm the tool now shows as **Off / Disabled** in the list before continuing.

> **⚠️ Warning:** This was the step most learners discovered was missing. With **both** tools on, the agent often fires the Step 4 email tool instead of the new flow, and the flow appears to "do nothing." Turning the connector tool **Off** isolates the flow so you can confirm it works.

#### Step 5b — Create the agent flow

1. In Copilot Studio's left navigation, select **Tools**, then **+ New tool** → choose the **Agent flow** tile. *(From inside the agent you can instead use the **Tools** tab → **+ Add a tool** → **New Agent flow**.)*
2. Power Automate opens with two steps already in place: the trigger **When an agent calls the flow** and a **Respond to the agent** action. Every agent flow follows this three-part shape: **trigger → do the work → respond**.

#### Step 5c — Define the flow's input

1. Select the trigger **When an agent calls the flow**, then **+ Add an input**.
2. Choose **Text**, name it `Request summary`, and give it the hint `A short summary of the support request`. This is the value the agent will pass in from the conversation.
3. Open the **Overview** tab → **Details** → **Edit**, set **Flow name** to `Log support request` and **Description** to `Logs a support request as a new row in the requests table`, then **Save**.

#### Step 5d — Add the work: "Add a row into a table" (the only action here)

1. Back on the **Designer** tab, select the **+** between the trigger and **Respond to the agent** to insert an action.
2. Search for `Excel`, choose **Excel Online (Business)**, then the action **Add a row into a table** (reuse the workbook and table from Lab 2, or any table with a `Request` column).
3. Map the row's **Request** column to the trigger's `Request summary` input using **Dynamic content**.

> **Reminder:** Add **a row into a table** here — **not** a *Send an email* action. The email path was already covered by the connector tool in Steps 2–4.

#### Step 5e — Respond to the agent

1. Select the **Respond to the agent** node, then **+ Add an output**.
2. Choose **Text**, name it `status`, and set its value to `Logged` (or use **Dynamic content** to return the new row's ID). The flow **must** end here, or the agent never gets a result back.

#### Step 5f — Publish

1. Select **Save draft**, then **Publish**.
2. Return to **Tools** and confirm the flow's status is **Ready**.

#### Step 5g — Add the flow to the agent and map its input

1. In the agent, open the **Tools** tab → **+ Add a tool**, apply the **Workflows** filter, select **Log support request**, then **Add and configure**.
2. Set a clear **Description**: `Records a support request to the requests table when the user asks to log or file an issue.`
3. Under **Additional details**, review **When this tool may be used**, **Ask the end user before running**, and **Credentials to use** (end-user credentials, with a sign-in prompt like `Please sign in to log the request`).
4. Under **Inputs**, for the `Request summary` input set **Fill using** → **Dynamically fill with AI** so the agent writes the summary from the conversation (or **Custom value** to bind a variable), just like the fixed-vs-AI choice in Step 4.
5. Under **Completion**, set **After running** → **Write the response with generative AI** so the agent confirms the result in natural language. **Save**.

> **Tip:** Every flow used as a tool follows the same three-part shape: **When an agent calls the flow** (trigger) → **do the work** → **Respond to the agent** (give a result back). You will reuse this pattern throughout Day 3.

### Step 6: Test the agent performing the action (~8 minutes)

1. Open the **Test** pane and select **Refresh** at the top so it picks up the new flow tool.
2. Type a message that should trigger the flow, for example:
   - `Please log a support request: I need help with order 123.`
3. Watch the agent decide to **call the Log support request flow**. If it asks for confirmation or shows a sign-in prompt, approve it.
4. Confirm the action really happened — open your table and check that a **new row** was added with the request summary.
5. Open the **Activity map** (a diagram of the conversation, if shown) to see the tool being called and the exact data passed into it. This is the best way to understand *why* the agent did what it did.
6. **Switch the email tool back on:** return to the **Tools** tab and turn the **Send notification email** tool (Steps 2–4) back **On**. With both tools live and clearly described, the agent can now *log* a request **and** *email* support — choosing each by its **description**.

> **Tip:** If the flow does nothing, check three things in order: is the **Send notification email** tool still **Off** during the isolation test, did the flow **Publish** to status **Ready**, and did the agent actually choose the flow (look at the **Activity map**)?

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
| Flow tool fails to return | No response step | Make sure the flow ends with **Respond to the agent** with an output, then re-publish it. |
| Agent calls the old email tool, never the flow | Two competing tools both enabled | Turn the **Send notification email** connector tool **Off** while you test the flow (Step 5a), then test again. |
| Flow shows up but status isn't **Ready** | Not published | **Save draft** then **Publish** the flow; the **Tools** list must show status **Ready** before the agent can call it. |

## Key Takeaways
- **Tools/Actions** let an agent *act* — using connectors, prebuilt actions, or full Power Automate flows.
- The tool **description** is what makes the agent call the right tool at the right time — write it carefully.
- Inputs can be **fixed** or **filled by AI** from the conversation; use fixed values for anything that must not change.
- A flow used as a tool always goes **When an agent calls the flow → do the work → Respond to the agent**.
- Use a **flow** (not a single connector action) when the work is **multi-step** — e.g. **Add a row into a table** to log a record and return a result.
- When two tools overlap, the agent may pick the wrong one — **turn off** the competing tool while you test, then re-enable it once each tool has a precise description.
- A broken connection causes an **Unauthorized** error — reconnect with a mailbox-enabled account.
- Flows-as-tools are the foundation of the end-to-end workflows you build in Day 3.

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 9: Sales Enquiry Assistant](../Lab%209%20-%20Sales%20Enquiry%20Assistant/index.md).

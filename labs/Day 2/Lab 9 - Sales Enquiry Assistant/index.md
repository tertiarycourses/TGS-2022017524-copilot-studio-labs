# Lab 9: Sales Enquiry Assistant

## Lab Title
Build a Sales Enquiry Assistant that Captures Structured Data

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a Copilot Studio **agent** from scratch in the correct environment
2. Build a **topic** and set its **trigger** so the agent knows when to run it — a **description** for generative orchestration (default), or **trigger phrases** for classic orchestration
3. Add **Ask a question** nodes that save answers into named **variables**
4. Choose the right **Identify** type so text and numbers are captured cleanly
5. Return a tidy **structured summary** that inserts every captured variable
6. Understand how these variables will later feed a Power Automate flow (Lab 10 and Day 3)

## Prerequisites
- Completed [Lab 6](../Lab%206%20-%20Create%20Your%20First%20Agent/index.md)
- Read [Module 3](../Module%203%20-%20Business%20Agents%20Concepts.md), especially *Prompt design for structured outputs*

> **Tip:** Sign in to Copilot Studio at [https://copilotstudio.microsoft.com](https://copilotstudio.microsoft.com) and confirm the environment shown at the **top-right** says **NUS Copilot Sandbox** before you start. Every lab on Day 2 must be built in this same environment, otherwise your agent and your flow will not be able to see each other later.

## Scenario
You work at **ACME Pte Ltd**. The sales team complains that enquiries arrive in inconsistent formats — some by email, some by phone notes — so details get lost. Your job is to build a **Sales Enquiry Assistant** agent that walks a customer through a short set of questions and captures **name, company, product, and quantity** as separate, named pieces of data. The result is a clean **structured summary** — exactly the kind of tidy data a Power Automate flow can log and route automatically in the next lab.

---

## Step-by-Step Guide

### Step 1: Create the agent (~5 minutes)
1. In the left navigation, select **Create**, then select **New agent**.
2. A conversational setup screen may appear. Look for the **Skip to configure** button (top-right of that panel) and select it so you can fill in the details directly.
3. Fill in the configuration fields:
   - **Name:** `Sales Enquiry Assistant`
   - **Description:** `Captures sales enquiries (name, company, product, quantity) as structured data for ACME Pte Ltd.`
   - **Instructions:**
     ```
     You are a Sales Enquiry Assistant for ACME Pte Ltd.
     Your job is to collect a customer's enquiry details: full name, company,
     product of interest, and quantity.
     Collect one item at a time and be polite and concise.
     Do not answer unrelated questions; gently steer back to capturing the enquiry.
     ```
4. Select the **Create** button (top-right). Wait a few seconds while the agent is provisioned.

> **Tip:** If **Create** is greyed out, the **Name** field is usually empty. Every agent needs a name before it can be created.

### Step 2: Create the "New Sales Enquiry" topic (~10 minutes)

> **⚠️ Read this first — the latest Copilot Studio works differently.** New agents now use **generative orchestration** by default. In this mode a topic is triggered by its **name and description** — the agent *chooses* the topic when the user's message matches that description — **not** by a fixed list of "Phrases". The old phrase list still exists, but it's now called **User says a phrase** and only appears if you deliberately switch the trigger type. This lab uses the modern **description-based** trigger (recommended and easiest); the phrase option is shown at the end of this step.

1. Open your **Sales Enquiry Assistant** agent, then in the agent's top menu select **Topics**. *(If you don't see it, select **⋯ More** and choose **Topics**.)*
2. Select **+ Add a topic**, then choose **From blank**. A blank canvas opens with a single **Trigger** node at the top. *(You may also see **Create from description with Copilot** — ignore it for this lab so you build the steps yourself.)*
3. On the canvas toolbar, select **Details** to open the **Topic details** panel, then set:
   - **Name:** `New Sales Enquiry`  *(don't use a full stop/period in a topic name)*
   - **Description:** `Use this topic when the customer wants to make a sales enquiry, ask for a quote, or say they are interested in buying a product. It collects the customer's name, company, product, and quantity.`

   Close the panel. This **Description** is what makes the agent pick this topic, so keep it specific.
4. Select the **Trigger** node once. For a generative-orchestration agent it reads **The agent chooses** — that is correct, and it uses the description from step 3. **You do not need to add any phrases.**
5. Select **Save** (top-right of the canvas).

> **Tip:** The agent matches on *meaning*, not exact wording. A clear, specific **Description** is what makes the topic fire reliably — write it the way you'd explain to a colleague *when* this topic should be used.

**(Optional) Want exact trigger phrases instead?** Only if your agent uses **classic orchestration**, or you specifically want the topic to fire on set phrases:
   1. Hover over the **Trigger** node and select the **Change trigger** icon.
   2. Choose **User says a phrase**.
   3. Add example phrases (aim for 5–10), each on its own line: `I want to make an enquiry`, `I'd like a quote`, `new sales enquiry`, `I'm interested in a product`.
   4. Select **Save**.

### Step 3: Capture the customer's name and company (~10 minutes)
1. Under the **Trigger** node, select the **Add node** icon (**+**), then choose **Ask a question**. A **Question** node appears.
2. Configure the question node:
   - **Ask a question (message):** `Sure, I can help with that! What is your full name?`
   - **Identify:** open this dropdown and choose **User's entire response**. This captures the whole reply as plain text (good for names).
   - **Save user response as:** Copilot Studio creates a variable automatically. Select the variable name and rename it to `customerName`.
3. Select the **Add node** icon (**+**) below that node and add a second **Ask a question** node for the company:
   - **Ask a question (message):** `Thanks! Which company are you with?`
   - **Identify:** **User's entire response**
   - **Save user response as:** rename the variable to `company`

> **Tip:** Rename variables right away. A clear name like `customerName` is much easier to find later than the default `Var1`, especially when you map it to a flow in Lab 10.

### Step 4: Capture the product and quantity (~10 minutes)
1. Add another **Ask a question** node for the product:
   - **Ask a question (message):** `Which product are you interested in?`
   - **Identify:** **User's entire response**
   - **Save user response as:** `product`
2. Add a final **Ask a question** node for the quantity:
   - **Ask a question (message):** `How many units would you like?`
   - **Identify:** open the dropdown and choose **Number**. This forces the answer to be a real number, so it can be used in calculations and stored as a number later.
   - **Save user response as:** `quantity`

> **⚠️ Warning:** Make sure quantity uses **Identify = Number**, not "User's entire response". If you leave it as text, `quantity` becomes a word like "twenty-five" instead of `25`, and the Excel/flow steps in Lab 10 will store messy data.

> **Tip:** Capturing into four separate named variables (`customerName`, `company`, `product`, `quantity`) is what makes the output **structured** — each piece of data is isolated and reusable. A single blob of free text could not be logged into separate spreadsheet columns.

### Step 5: Confirm and summarize (~10 minutes)
1. Select the **Add node** icon (**+**) below the quantity question and choose **Send a message**. A **Message** node appears.
2. Type the summary text below. Wherever you see a curly-brace variable, do **not** type it as plain text — instead place your cursor there, select the **{x}** (Insert variable) button on the node, and pick the matching variable from the list:
   ```
   Thank you! Here is a summary of your enquiry:
   • Name: {customerName}
   • Company: {company}
   • Product: {product}
   • Quantity: {quantity}
   A sales representative from ACME will contact you within 1 business day.
   ```
3. Select **Save**.

> **⚠️ Warning:** If you type `{customerName}` as literal text, the customer will literally see the words "{customerName}". You must insert it through the **{x}** button so it shows up as a coloured variable token.

### Step 6: Test the assistant (~10 minutes)
1. Open the **Test** pane on the right (if it was already open, select the **Refresh** / restart icon so it picks up your latest changes).
2. Type a message that starts an enquiry, e.g. `I'd like a quote`. The agent should recognise this from your topic **Description** and start the **New Sales Enquiry** topic.
3. Answer each question in turn:
   - Name: `Mei Ling`
   - Company: `BrightTech`
   - Product: `Air Fryer Pro`
   - Quantity: `25`
4. Confirm the agent returns the structured summary with all four values filled in correctly.
5. Now test the **unhappy path**: start the topic again, and when asked for quantity, type the word `twenty-five` instead of a number. Because **Identify** is set to **Number**, the agent should **re-ask** the question. Type `25` and confirm it then accepts it.

> **Tip:** The re-ask behaviour is a feature, not a bug. It guarantees `quantity` is always a clean number before it reaches a flow.

---

## Checkpoint
You are ready to move on when all of the following are true:
- ✅ An agent named **Sales Enquiry Assistant** exists in the **NUS Copilot Sandbox** environment
- ✅ It has a **New Sales Enquiry** topic with a clear **trigger** — a description (**The agent chooses**) or trigger phrases
- ✅ Four variables are captured: `customerName`, `company`, `product`, and `quantity` (Number)
- ✅ A structured summary with all four values is returned during testing
- ✅ Typing text for the quantity causes the agent to re-ask

## Troubleshooting
| Problem | Solution |
|---------|----------|
| I can't find a "Phrases" trigger type | New agents use **generative orchestration**, so the trigger is **The agent chooses** (description-based). Either write a clear topic **Description**, or hover the **Trigger** node → **Change trigger** → **User says a phrase** to add phrases. |
| Topic doesn't trigger when I type | Make the topic **Description** more specific about *when* to use it (or add more varied phrases if using **User says a phrase**). Type something close in meaning; re-test after **Save**. |
| Variable shows as blank in the summary | You probably typed the variable name as text. Delete it and re-insert it using the **{x}** button. Also confirm the **Save user response as** name matches. |
| Summary shows literal `{customerName}` text | Same cause — insert variables via **{x}**, do not type curly braces by hand. |
| Quantity answer is rejected or re-asked forever | Set the quantity question's **Identify** to **Number** and answer with digits like `25`, not spelled-out words. |
| Test pane shows old behaviour | Select the **Refresh / restart** icon at the top of the Test pane to reload the latest version of the topic. |
| Agent answers off-topic questions | Tighten the **Instructions** to say it must steer back to capturing the enquiry. |

## Key Takeaways
- **Topics** are triggered by a **description** (**The agent chooses**, generative orchestration — the default) or by **trigger phrases** (**User says a phrase**, classic orchestration).
- **Ask a question** nodes capture answers into named **variables**, which is the foundation of structured data.
- The **Identify** type matters: use **User's entire response** for free text and **Number** for numeric answers.
- A confirmation summary builds user trust and lets you visually verify the captured data before any automation runs.
- Clean, separated variables here are what make the agent-to-flow integration in Lab 10 possible.

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 10: Procurement Request Workflow](../Lab%2010%20-%20Procurement%20Request%20Workflow/index.md), where you'll connect a capturing agent to a Power Automate flow for the first time.

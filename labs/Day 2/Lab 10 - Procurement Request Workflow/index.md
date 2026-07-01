# Lab 10: Procurement Request Workflow

## Lab Title
Connect a Procurement Agent to a Power Automate Flow

## Lab Objectives
By the end of this lab, you will be able to:
1. Prepare an Excel **table** so a flow can log structured rows into it
2. Build an agent topic that captures a procurement request as named **variables**
3. Create an **agent flow** in Power Automate triggered **when an agent calls the flow**
4. Define flow **inputs** and map agent variables into them
5. Have the flow **log the request to Excel** and **email the procurement team** in one run
6. Return a confirmation from the flow back to the agent with **Respond to the agent**

## Prerequisites
- Completed [Lab 9](../Lab%209%20-%20Sales%20Enquiry%20Assistant/index.md) (capturing variables)
- Completed Day 1 Labs 1–2 (email + Excel actions)

> **⚠️ Warning:** Your agent (Copilot Studio) and your flow (Power Automate) must live in the **same environment — NUS Copilot Sandbox**. If they are in different environments, the agent will not be able to find or call its flow. Before you begin, open both [Copilot Studio](https://copilotstudio.microsoft.com) and [Power Automate](https://make.powerautomate.com) and confirm the **top-right environment picker** shows **NUS Copilot Sandbox** in each.

## Scenario
At **ACME Pte Ltd**, staff currently email the procurement team to request supplies, and someone manually copies each request into a spreadsheet. You'll replace that with an agent. When a staff member finishes their request, the agent **automatically logs** it to a shared spreadsheet **and emails** the procurement team — no manual copying, no missed requests. This is your first true **agent + flow** integration: the agent gathers the data, and a Power Automate flow does the real work.

---

## Step-by-Step Guide

### Step 1: Prepare the procurement log in Excel (~5 minutes)
1. In Excel (saved to **OneDrive for Business**, not your local PC), create a new workbook and name it `Procurement Log`.
2. In **row 1**, type these six headers, one per cell from A1 to F1: `Date`, `Requester`, `Item`, `Quantity`, `Reason`, `Status`.
3. Select the range **A1:F1**, then go to the **Insert** tab and select **Table**. In the dialog, tick **My table has headers** and select **OK**.
4. With the table selected, open the **Table Design** tab. In the **Table Name** box (far left), replace the default name with `ProcurementTable`. Press **Enter**.
5. Save and close the workbook.

> **⚠️ Warning:** The file must be in **OneDrive for Business** (or SharePoint), not on your local hard drive. A flow's Excel actions can only see files stored in the cloud. The exact table name `ProcurementTable` matters — the flow will look for it by name.

### Step 2: Create the agent and capture the request (~10 minutes)
1. In Copilot Studio, select **Create**, then **New agent**, then **Skip to configure**:
   - **Name:** `Procurement Assistant`
   - **Description:** `Captures staff purchase requests for ACME Pte Ltd and submits them for processing.`
   - **Instructions:**
     ```
     You are a Procurement Assistant for ACME Pte Ltd.
     Collect a staff member's purchase request: requester name, item, quantity,
     and reason. Collect one item at a time, be concise, then confirm the request
     has been submitted.
     ```
   - Select **Create**.
2. Open the **Topics** tab, select **+ Add a topic**, then **From blank**. On the toolbar select **Details** and set the **Name** to `New Procurement Request`.
3. Give the topic a clear **trigger** so the agent knows when to run it:
   - **Latest Copilot Studio (generative orchestration — default):** the **Trigger** node reads **The agent chooses**. In the **Details** panel, set the **Description** to `Use this topic when a staff member wants to raise a procurement or purchase request to buy supplies. It collects their name, item, quantity, and reason.` No phrases are needed.
   - **(Optional) Classic orchestration / exact phrases:** hover the **Trigger** node → **Change trigger** → **User says a phrase**, then add phrases such as `procurement request`, `I need to buy something`, `I want to order supplies`, `raise a purchase request`.
4. Add four **Ask a question** nodes in order, using the **Add node** icon (**+**) each time. For each, set the **Identify** type and rename the **Save user response as** variable exactly as shown:
   - Question `What is your name?` → Identify **User's entire response** → save as `requester`
   - Question `What item do you need?` → Identify **User's entire response** → save as `item`
   - Question `How many do you need?` → Identify **Number** → save as `quantity`
   - Question `What is the reason for this request?` → Identify **User's entire response** → save as `reason`
5. Select **Save**.

> **⚠️ Warning:** Set the quantity question's **Identify** to **Number**. If it stays as text, the Excel **Quantity** column will store words instead of numbers.

### Step 3: Create the agent flow (~15 minutes)
1. Still in the **New Procurement Request** topic, select the **+** node after the last question, choose **Add a tool**, then **New Agent flow**.
   - *(Alternatively, from the agent's **Tools** tab, select **Add a tool**, then **New agent flow**.)*
2. Power Automate opens in a new tab with the trigger already added: **When an agent calls the flow**.
3. Confirm the Power Automate environment picker (top-right) reads **NUS Copilot Sandbox**.
4. On the **When an agent calls the flow** trigger, select **+ Add an input** and create four inputs. Choose the matching type and name each one exactly:
   - Type **Text**, name `requester`
   - Type **Text**, name `item`
   - Type **Number**, name `quantity`
   - Type **Text**, name `reason`

> **Tip:** Keeping flow input names identical to your topic variable names (`requester`, `item`, `quantity`, `reason`) makes the mapping step later much less confusing.

### Step 4: Add the flow actions — log to Excel and email (~15 minutes)
**Action 1 — Add a row into a table (Excel Online Business):**
1. Below the trigger, select **+ New step** (or **+**), search for **Add a row into a table**, and select it (Excel Online (Business)).
2. Set the file location fields:
   - **Location:** OneDrive for Business
   - **Document Library:** OneDrive
   - **File:** browse to and select `Procurement Log.xlsx`
   - **Table:** select `ProcurementTable` from the dropdown
3. Map the columns. For the **Date** column, you must enter an expression — do not type the date by hand:
   - Click the **Date** field, then select the **fx** (Expression / function) tab in the dynamic content panel.
   - Type this expression into the fx editor, then select **Add / OK**:
     ```
     formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')
     ```
   - The field should now show a blue/purple **token**, not plain text.
4. Map the remaining columns using the **Dynamic content** tab — pick the values that come from the **trigger** (the inputs you defined in Step 3):
   - **Requester:** `requester`
   - **Item:** `item`
   - **Quantity:** `quantity`
   - **Reason:** `reason`
   - **Status:** type the literal text `Pending`

> **⚠️ Warning:** The `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')` expression must be entered through the **fx editor** so it becomes a token. If you paste it as plain text into the Date field, Excel will store the literal characters `formatDateTime(...)` instead of a real date.

**Action 2 — Send an email (Office 365 Outlook):**
1. Select **+ New step**, search for **Send an email (V2)** (Office 365 Outlook), and select it.
2. Fill in the email:
   - **To:** the procurement team address (use your own email for testing)
   - **Subject:** type `New Procurement Request from `, then insert the **requester** dynamic content right after it
   - **Body:** type the text below, inserting each value from the **Dynamic content** panel where shown (do not type the variable names by hand):
     ```
     A new procurement request has been submitted:
     Requester: {requester}
     Item: {item}
     Quantity: {quantity}
     Reason: {reason}
     Status: Pending
     ```

**Action 3 — Respond to the agent:**
1. Select **+ New step**, search for **Respond to the agent**, and select it.
2. Add a **Text** output named `result` with the value: `Logged and procurement team notified.`
3. Select **Save** at the top to save (and publish) the flow.
4. Return to the Copilot Studio tab (or select **Go back to agent** if prompted).

> **⚠️ Warning:** If the **Send an email** action shows an **"Unauthorized"** error, the Office 365 Outlook **connection** is broken or signed in with an account that has no mailbox. Open the action's **…** menu, select **My connections**, and **reconnect** using a mailbox-enabled work account. Every connection used by the flow must show a green ✓ before the flow will run.

### Step 5: Wire the flow into the topic (~10 minutes)
1. Back in Copilot Studio, the flow should now appear as a tool/action node inside the **New Procurement Request** topic. If it does not appear, **refresh** the page and make sure the flow was **published** in the **same environment (NUS Copilot Sandbox)**.
2. Select the tool node. Under its **inputs**, map each input to the matching topic variable — this step is mandatory; the flow receives nothing if you skip it:
   - input `requester` → variable `requester`
   - input `item` → variable `item`
   - input `quantity` → variable `quantity`
   - input `reason` → variable `reason`
3. After the tool node, add a **Send a message** node that shows the value the flow returned. Insert the `result` output via the **{x}** button:
   ```
   {result} Your request has been recorded. Thank you!
   ```
4. Select **Save** to save the topic.

> **⚠️ Warning:** Mapping is the step everyone forgets. After adding the flow as a tool, you **must** map each flow input to its matching topic variable. Unmapped inputs arrive empty, so your Excel row and email will be blank.

### Step 6: Test end-to-end (~10 minutes)
1. Open the **Test** pane and select the **Refresh / restart** icon so it loads the latest topic.
2. Type a message that starts the request, e.g. `procurement request` — the agent recognises it from the topic **Description** (or phrases). Answer the questions:
   - Name: `Daniel`
   - Item: `Wireless mouse`
   - Quantity: `10`
   - Reason: `New hires`
3. Confirm all three results occurred:
   - The agent shows the confirmation message ("Logged and procurement team notified. Your request has been recorded. Thank you!").
   - A **new row** appears in **Procurement Log.xlsx** (with a real date, the four values, and Status `Pending`).
   - The **notification email** arrives in your inbox.
4. If anything is missing, open the flow in Power Automate and review its **run history** (28-day run history) — select the latest run to inspect the inputs each step received and any error messages.

---

## Checkpoint
You are ready to move on when all of the following are true:
- ✅ A **Procurement Log** workbook with a **ProcurementTable** exists in OneDrive
- ✅ A **Procurement Assistant** agent captures four variables (`requester`, `item`, `quantity`, `reason`)
- ✅ An **agent flow** triggered by **When an agent calls the flow**, with four matching inputs
- ✅ One conversation produces both a **new Excel row** and a **notification email**
- ✅ The agent shows the flow's returned confirmation message

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Flow doesn't appear in the topic | Refresh the Copilot Studio page; confirm the flow was **published** and is in the **same environment (NUS Copilot Sandbox)**. |
| Inputs unmapped or arriving empty | Select the tool node and map **each** flow input to its matching topic variable. |
| "Unauthorized" error on Send an email | Reconnect the **Office 365 Outlook** connection with a mailbox-enabled work account; every connection must show a green ✓. |
| Date column shows `formatDateTime(...)` as text | You typed the expression instead of entering it in the **fx editor**. Re-enter it via **fx** so it becomes a token. |
| Excel row is blank | Map the columns to the **trigger** dynamic content (the inputs), not to outputs of later steps. |
| No email received | Check your Junk folder, verify the **To** address, and review the flow **run history** for errors. |
| Flow can't find the table | Confirm the file is in **OneDrive for Business** and the table is named exactly `ProcurementTable`. |

## Key Takeaways
- An **agent flow** uses the **When an agent calls the flow** trigger and ends with **Respond to the agent**.
- Agent **variables** map to flow **inputs**; this mapping is mandatory and easy to forget.
- The flow can **return** a value (`result`) that the agent shows back to the user.
- Dates come from the `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')` expression entered via the **fx editor** as a token — never typed as text.
- One short conversation now triggers real business actions: **logging** and **notifying** together.

## Duration
~50 minutes

## Next Steps
Proceed to [Lab 11: Automated Response Generation](../Lab%2011%20-%20Automated%20Response%20Generation/index.md).

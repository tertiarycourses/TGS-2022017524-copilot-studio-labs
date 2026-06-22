# Lab 6: Procurement Request Workflow

## Lab Title
Connect a Procurement Agent to a Power Automate Flow

## Lab Objectives
By the end of this lab, you will be able to:
1. Build an agent topic that captures a procurement request as variables
2. Create an **agent flow** (Power Automate) triggered **when the agent calls it**
3. Define flow **inputs** and pass agent variables into them
4. Have the flow **log the request to Excel and email the procurement team**
5. Return a confirmation from the flow back to the agent

## Prerequisites
- Completed [Lab 5](../Lab%205%20-%20Sales%20Enquiry%20Assistant/index.md) (capturing variables)
- Completed Day 1 Labs 1–2 (email + Excel actions)

## Scenario
Staff request items through an agent. When they finish, the agent **automatically logs** the request to a spreadsheet and **emails** the procurement team — no manual copying. This is your first true **agent + flow** integration.

---

## Step-by-Step Guide

### Step 1: Prepare the procurement log (~5 minutes)
1. In Excel (OneDrive), create a workbook named `Procurement Log`.
2. Add headers in row 1: `Date`, `Requester`, `Item`, `Quantity`, `Reason`, `Status`.
3. Select A1:F1 → **Insert → Table** (tick *My table has headers*).
4. Name the table `ProcurementTable` (Table Design tab). Close Excel.

### Step 2: Create the agent and capture the request (~10 minutes)
1. Copilot Studio → **Create → New agent** → **Skip to configure**:
   - **Name:** `Procurement Assistant`
   - **Instructions:**
     ```
     You are a Procurement Assistant. Collect a staff member's purchase request:
     requester name, item, quantity, and reason. Collect one at a time, be concise,
     then confirm the request has been submitted.
     ```
   - **Create**.
2. **Topics → Add a topic → From blank**, name it `New Procurement Request`.
3. Trigger **Phrases:** `I need to buy something`, `procurement request`, `I want to order supplies`, `raise a purchase request`.
4. Add **Ask a question** nodes (Identify = *User's entire response*, except quantity = *Number*):
   - `What is your name?` → save as `requester`
   - `What item do you need?` → save as `item`
   - `How many?` (Number) → save as `quantity`
   - `What is the reason for this request?` → save as `reason`
5. **Save**.

### Step 3: Create the agent flow as a tool (~15 minutes)
1. Still in the **New Procurement Request** topic, after the last question select **+** → **Add a tool** → **New Agent flow**.
   - *(Alternatively: Tools tab → Add a tool → New agent flow.)*
2. Power Automate opens with the trigger **When an agent calls the flow**.
3. On the trigger, select **+ Add an input** and create four inputs (match names to keep it clear):
   - **Text** `requester`
   - **Text** `item`
   - **Number** `quantity`
   - **Text** `reason`

### Step 4: Add the flow actions — log + email (~15 minutes)
**Action 1 — Add a row into a table (Excel Online Business):**
1. **+ New step** → **Add a row into a table**.
2. Location **OneDrive for Business**, Library **OneDrive**, File **Procurement Log.xlsx**, Table **ProcurementTable**.
3. Map columns:
   - **Date:** Expression `utcNow()`
   - **Requester:** dynamic content **requester** (from the trigger)
   - **Item:** **item**
   - **Quantity:** **quantity**
   - **Reason:** **reason**
   - **Status:** `Pending`

**Action 2 — Send an email (Office 365 Outlook → Send an email V2):**
1. **+ New step** → **Send an email (V2)**.
2. **To:** procurement team address (use your own email for testing).
3. **Subject:** `New Procurement Request from ` + **requester**
4. **Body:**
   ```
   A new procurement request has been submitted:
   Requester: {requester}
   Item: {item}
   Quantity: {quantity}
   Reason: {reason}
   Status: Pending
   ```
   (insert each value via dynamic content)

**Return a result to the agent:**
1. **+ New step** → search **Respond to the agent** (Return value(s) to agent).
2. Add a **Text** output named `result` with value: `Logged and procurement team notified.`

3. Select **Save / Publish** the flow. When done, choose **Go back to agent** (or return to the Copilot Studio tab).

### Step 5: Wire the flow into the topic (~10 minutes)
1. Back in Copilot Studio, the flow should appear as a tool/action node in the topic. If not, refresh.
2. Under the tool's **inputs**, map each one to the topic variable:
   - `requester` → `requester`
   - `item` → `item`
   - `quantity` → `quantity`
   - `reason` → `reason`
3. After the tool node, add a **Send a message** node that uses the returned value:
   `{result} Your request has been recorded. Thank you!`
4. **Save** the topic.

### Step 6: Test end-to-end (~10 minutes)
1. Open the **Test** pane (refresh).
2. Type `procurement request` and answer:
   - Name: `Daniel`, Item: `Wireless mouse`, Quantity: `10`, Reason: `New hires`
3. Confirm:
   - The agent shows the confirmation message.
   - A **new row** appears in **Procurement Log.xlsx**.
   - The **email** arrives in your inbox.
4. Open the flow's **run history** to inspect inputs/outputs if anything is missing.

---

## Checkpoint
- ✅ **Procurement Assistant** agent captures 4 variables
- ✅ An **agent flow** triggered by the agent, with matching inputs
- ✅ Each request → new Excel row **and** notification email
- ✅ Agent shows the flow's returned confirmation

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Flow not appearing in topic | Refresh the topic; ensure the flow was **published** and in the **same environment**. |
| Inputs unmapped / empty | Re-map each tool input to the matching topic variable. |
| Excel row blank | Check column mapping to the **trigger** dynamic content (not other steps). |
| No email | Check Junk; verify the **To** address; review run history. |

## Key Takeaways
- An **agent flow** uses the trigger **"When an agent calls the flow."**
- Agent **variables** map to flow **inputs**; the flow can **return** values to the agent.
- One conversation now triggers real actions: logging **and** notifying.

## Duration
~50 minutes

## Next Steps
Proceed to [Lab 7: Automated Response Generation](../Lab%207%20-%20Automated%20Response%20Generation/index.md).

# Lab 15: Order Processing Workflow (Agent + Flow)

## Lab Title
End-to-End Order Processing — Agent Captures the Order, Flow Logs It, Confirms It, and Alerts the Warehouse

## Lab Objectives
By the end of this lab, you will be able to:
1. Build a Copilot Studio **Order Assistant** agent that captures a customer order as structured data (name, email, product, quantity, address)
2. Connect that agent to a Power Automate **agent flow** using **When an agent calls the flow** and **Respond to the agent**
3. **Log** each order into an Excel table (**Order Log** workbook → **OrderTable**) with an automatic timestamp and a `Received` status
4. Use an **AI prompt** to draft a friendly order-confirmation email, then **Send an email** to the customer
5. Use a **Condition** so that large orders (quantity over 100) trigger a **restock alert** email to the warehouse — and small orders do not

## Prerequisites
- Completed Day 2 Labs 6–11 (create an agent, capture variables, connect an agent to a flow, AI prompts)
- Completed Day 1 Labs 1–2 (email + Excel actions)
- Environment **NUS Copilot Sandbox** with a working Outlook connection

> **Tip:** This lab reuses the exact same skills as the Procurement workflow in **Lab 14** — you are simply applying the "capture → log → generate → notify → branch" pattern to a brand-new business domain: **Order Processing**.

## Scenario
You work for **ACME Pte Ltd**. A customer places an order by chatting with an agent. The moment the order is captured, the workflow should do four things automatically:

1. **Record** the order in a shared Excel order register.
2. **Confirm** the order to the customer by email.
3. **Check** the quantity — if it is a large order, **alert the warehouse** to restock.
4. **Tell the agent** it is done, so the agent can thank the customer.

You will build this as a Copilot Studio **agent** (the part the customer talks to) plus a Power Automate **agent flow** (the part that does the back-office work).

---

## Step-by-Step Guide

### Step 1: Prepare the Order Log Excel table (~5 min)
The flow needs somewhere to write each order. We use an Excel **Table** (not just a sheet) because Power Automate can only add rows to a named table.

1. Go to **OneDrive** (office.com → OneDrive) and create a new Excel workbook named exactly **Order Log**.
2. In **row 1**, type these seven column headers, one per cell, starting in cell **A1**:

   `Date` | `Customer` | `Email` | `Product` | `Quantity` | `Address` | `Status`

3. Select the header cells **A1:G1**, then go to the **Insert** ribbon → click **Table**. In the dialog, make sure **My table has headers** is ticked, then click **OK**.
4. With the table selected, open the **Table Design** ribbon (top of the screen). In the **Table Name** box on the left, type **OrderTable** and press **Enter**.
5. Close Excel. Your changes save automatically to OneDrive.

> **Tip:** Later, if a date cell shows `########`, the column is just too narrow — widen it by double-clicking the border between the column letters. The data is fine.

### Step 2: Create the Order Assistant agent (~10 min)
1. Open **Copilot Studio** (copilotstudio.microsoft.com) and confirm the environment picker (top-right) shows **NUS Copilot Sandbox**. The agent and the flow must live in the **same environment**.
2. Click **Create** (left menu) → **New agent** → at the top of the setup screen click **Skip to configure**.
3. Fill in:
   - **Name:** `Order Assistant`
   - **Instructions:**
     ```
     You are an Order Assistant for ACME Pte Ltd.
     Collect a customer's order: customer name, email, product, quantity, and delivery address.
     Collect one item at a time, be friendly and concise, then confirm the order has been placed.
     ```
4. Click **Create**.
5. In the left menu open **Topics** → **Add a topic** → **From blank**. Rename the topic **New Order** (click the topic name at the top to rename).
6. Click the **Trigger** node → set **Phrases** to: `I want to place an order`, `new order`, `I'd like to buy`, `order products` (one phrase per line).
7. Below the trigger, click **+** → **Ask a question** five times to add five questions. For each one, type the message, set what to **Identify**, and save the answer to a **variable**:

   | Question message | Identify | Save answer as variable |
   |---|---|---|
   | `What is your name?` | User's entire response | `customerName` |
   | `What is your email?` | User's entire response | `email` |
   | `Which product would you like to order?` | User's entire response | `product` |
   | `How many units?` | **Number** | `quantity` |
   | `What is the delivery address?` | User's entire response | `address` |

   > **⚠️ Warning:** For the quantity question you **must** change **Identify** to **Number**. If it stays as text, the "greater than 100" comparison in Step 6 will not work correctly.

8. Click **Save** (top-right).

### Step 3: Start the agent flow (~10 min)
1. Still inside the **New Order** topic, click the **+** below your last question → **Add a tool** → **New Agent flow**. This opens the Power Automate flow designer in a new tab.
2. The first (trigger) node is already **When an agent calls the flow**. Click it to open it.
3. Click **+ Add an input** once for each field below. Choose the type, then type the exact name:
   - **Text** → `customerName`
   - **Text** → `email`
   - **Text** → `product`
   - **Number** → `quantity`
   - **Text** → `address`

> **Tip:** These input names are how the agent will hand its variables to the flow. Spell them exactly as shown — you will match them up again in Step 7.

### Step 4: Log the order to Excel (~5 min)
1. Click **+ New step** → search **Excel Online (Business)** → choose the action **Add a row into a table**.
2. Fill in the action's first three boxes from the dropdowns:
   - **Location:** OneDrive for Business
   - **Document Library:** OneDrive
   - **File:** browse to **Order Log.xlsx**
   - **Table:** **OrderTable**
3. The seven table columns now appear as fields. Map them:
   - **Date:** click inside the box → click the **fx** (function) icon to open the formula editor → type exactly:
     ```
     formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')
     ```
     then click **Add** / **OK**. The formula collapses into a single token. **Never type this expression directly into the field** — always enter it through the **fx** editor, or it will be saved as plain text.
   - **Customer:** dynamic content `customerName`
   - **Email:** dynamic content `email`
   - **Product:** dynamic content `product`
   - **Quantity:** dynamic content `quantity`
   - **Address:** dynamic content `address`
   - **Status:** type the literal word `Received`

### Step 5: Draft and send the order confirmation (~10 min)
1. *(Recommended)* Add an AI step: **+ New step** → search **AI prompt** → choose **Create text with GPT using a prompt** (sometimes shown as **Run a prompt**). In the prompt box, type:
   ```
   Write a short, friendly order confirmation email (max 100 words).
   Customer: {customerName}; Product: {product}; Quantity: {quantity}; Delivery to: {address}.
   Confirm the order is received and will be processed. Sign off as "The ACME Order Team".
   Output only the email body.
   ```
   (Insert each `{...}` value by picking it from the **dynamic content** list rather than typing it.)
2. **+ New step** → search **Office 365 Outlook** → choose **Send an email (V2)**. Fill in:
   - **To:** dynamic content `email`
   - **Subject:** type `Order confirmation: ` then add dynamic content `product`
   - **Body:** add the **AI prompt output** (the generated text from step 1). If you skipped the AI step, type your own short message using the dynamic content tokens.

> **⚠️ Warning:** If the Send an email action shows **Unauthorized** (a red error), the Outlook connection is signed in with the wrong account. Click the action's **…** menu → **+ Add new connection**, then sign in with a real **mailbox-enabled** tenant account. Every connection on the action should show a green check mark ✓ before you continue. (Same fix as [Lab 1](../../Day%201/Lab%201%20-%20Automated%20Email%20Workflow/index.md).)

### Step 6: Add the restock-alert Condition (~10 min)
Large orders should warn the warehouse; small orders should not.

1. **+ New step** → search **Condition** → choose **Condition** (under Control).
2. Build the test:
   - Left box: dynamic content `quantity`
   - Operator: **is greater than**
   - Right box: type `100`
3. In the **If yes** branch (this runs only for large orders):
   - Click **Add an action** → **Send an email (V2)**.
   - **To:** the warehouse address — for testing, use your own email so you can see it arrive.
   - **Subject:** type `RESTOCK ALERT: ` then add dynamic content `product`.
   - **Body:** type a message and drop in the tokens, e.g.
     `Large order received: ` `quantity` ` units of ` `product` ` for ` `customerName` `. Please check stock and restock if needed.`
4. Leave the **If no** branch **empty** — small orders need no alert.

> **Tip:** If Power Automate ever wraps an action in an automatic **For each** loop, it means you selected a field that can return multiple values. Here every field (`quantity`, `product`, etc.) is a single value, so no loop should appear. If one does, delete the action and re-add the dynamic content carefully.

### Step 7: Return a result and wire the inputs (~10 min)
1. **+ New step** → search **Respond to the agent** → add it. Add a **Text** output named `result` with the value:
   ```
   Your order has been placed and confirmed by email.
   ```
2. Click **Save** (and **Publish** if prompted), then close the flow tab and return to the agent (**Go back to agent** / the Copilot Studio tab).
3. In the **New Order** topic, click your flow's tool node. You will see the five flow inputs. Map each one to the matching agent **variable** from the dropdown:
   - `customerName` → `customerName`
   - `email` → `email`
   - `product` → `product`
   - `quantity` → `quantity`
   - `address` → `address`
4. Below the tool node, click **+** → **Send a message** and type:
   ```
   {result} Thank you for your order!
   ```
   (Insert `result` from the flow's outputs.)
5. Click **Save**.

### Step 8: Test end-to-end (~10 min)
1. Open the **Test** pane (top-right). Click the **refresh** icon so it picks up your latest changes.
2. Type `new order` and answer the questions for a **large** order:
   - Name: `Mei Ling`
   - Email: **your own email address**
   - Product: `Air Fryer Pro`
   - Quantity: `150`
   - Address: `123 Orchard Rd`
3. Confirm all four results:
   - The agent shows your "Thank you for your order!" message.
   - A **new row** appears in **Order Log.xlsx** with **Status** = `Received` and a timestamp in the **Date** column.
   - The **order confirmation** email arrives in your inbox.
   - Because `150` is greater than `100`, a **RESTOCK ALERT** email **also** arrives.
4. Run it once more with a **small** quantity (e.g. `5`) and confirm:
   - The order is still logged and confirmed.
   - **No** restock alert email is sent.

---

## Checkpoint
You are done when:
- ✅ The **Order Assistant** captures all five order fields (and quantity is a **Number**)
- ✅ The agent flow **logs** the order, **confirms** by email, and **conditionally** alerts the warehouse
- ✅ A **large** order (150) gets a restock alert; a **small** order (5) does not
- ✅ A new row with **Status = Received** and a real timestamp appears in **OrderTable**

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Flow does not appear in the topic | Refresh the page; make sure the flow is **Published** and in the **same** environment (**NUS Copilot Sandbox**). |
| Flow inputs arrive empty | In the tool node, re-map each agent variable to the matching flow input (Step 7). |
| Restock alert never fires (or always fires) | The Condition must compare `quantity` **is greater than** `100`, and `quantity` must be identified as a **Number** in Step 2. |
| Send an email shows **Unauthorized** | Reconnect Outlook with a mailbox-enabled account; confirm every connection shows a green ✓. |
| Date column shows the literal text `formatDateTime(...)` | You typed the expression instead of entering it through the **fx** editor. Re-enter it via **fx**. |
| Date cell shows `########` | The column is too narrow. Widen it — the data is correct. |
| An action got wrapped in **For each** | You selected a multi-value field. Remove the action and re-add single-value dynamic content. |

## Key Takeaways
- Order Processing is a complete **capture (agent) → log → confirm → alert** loop, end to end.
- A **Condition on quantity** turns a business rule (the restock threshold) into automatic behaviour.
- The timestamp comes from an **fx expression** (`formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')`) entered through the formula editor, never typed as text.
- This is the **same pattern as Procurement (Lab 14)** applied to a new domain — proof that one set of skills covers many business workflows.

## Duration
~55 minutes

## Next Steps
Proceed to the [Lab 16: Capstone Workshop](../Lab%2016%20-%20Capstone%20Workshop/index.md) to design and build your own end-to-end workflow.

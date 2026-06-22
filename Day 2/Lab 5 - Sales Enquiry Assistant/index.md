# Lab 5: Sales Enquiry Assistant

## Lab Title
Build a Sales Enquiry Assistant that Captures Structured Data

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a **Topic** with a trigger phrase
2. Add **question nodes** that capture answers into **variables**
3. Confirm the captured details back to the user
4. Produce a clean **structured summary** of the enquiry
5. Understand how these variables will feed a Power Automate flow (Lab 6 & Day 3)

## Prerequisites
- Completed [Lab 4](../Lab%204%20-%20Create%20Your%20First%20Agent/index.md)
- Read [Module 3](../Module%203%20-%20Business%20Agents%20Concepts.md), especially *Prompt design for structured outputs*

## Scenario
Your sales team wants every enquiry captured consistently. You'll build an agent topic that collects **name, company, product, and quantity**, then presents a tidy summary. This structured data is exactly what a flow needs to log and route the enquiry.

---

## Step-by-Step Guide

### Step 1: Create the agent (~5 minutes)
1. In Copilot Studio, **Create → New agent** → **Skip to configure**.
2. Fill in:
   - **Name:** `Sales Enquiry Assistant`
   - **Description:** `Captures sales enquiries (name, company, product, quantity) as structured data.`
   - **Instructions:**
     ```
     You are a Sales Enquiry Assistant.
     Your job is to collect a customer's enquiry details: full name, company, product of interest, and quantity.
     Collect one item at a time and be polite and concise.
     Do not answer unrelated questions; gently steer back to capturing the enquiry.
     ```
3. Select **Create**.

### Step 2: Create a "New Sales Enquiry" topic (~10 minutes)
1. Open the **Topics** tab → **Add a topic** → **From blank**.
2. Rename the topic (top of canvas): `New Sales Enquiry`.
3. Select the **Trigger** node → set it to **Phrases** and add trigger phrases (these are what a user types to start the topic):
   - `I want to make an enquiry`
   - `I'd like a quote`
   - `new sales enquiry`
   - `I'm interested in a product`
4. Select **Save**.

### Step 3: Capture the customer's name (~10 minutes)
1. Under the trigger, select **+** → **Ask a question**.
2. Configure:
   - **Question text:** `Sure, I can help with that! What is your full name?`
   - **Identify:** choose **User's entire response** (we just want the text).
   - **Save response as:** rename the variable to `customerName`.
3. Add another **Ask a question** node for company:
   - **Question text:** `Thanks! Which company are you with?`
   - **Identify:** **User's entire response**
   - **Save as:** `company`

### Step 4: Capture product and quantity (~10 minutes)
1. Add an **Ask a question** node:
   - **Question text:** `Which product are you interested in?`
   - **Identify:** **User's entire response**
   - **Save as:** `product`
2. Add an **Ask a question** node for quantity:
   - **Question text:** `How many units would you like?`
   - **Identify:** choose **Number** (so the answer is captured as a number).
   - **Save as:** `quantity`

> Capturing into named variables (`customerName`, `company`, `product`, `quantity`) is what makes the output **structured** — each piece of data is separate and reusable.

### Step 5: Confirm and summarize (~10 minutes)
1. Add a node → **Send a message**.
2. Enter a summary that inserts every variable (use the **{x}** / **Insert variable** button for each):
   ```
   Thank you! Here is a summary of your enquiry:
   • Name: {customerName}
   • Company: {company}
   • Product: {product}
   • Quantity: {quantity}
   A sales representative will contact you within 1 business day.
   ```
3. Select **Save**.

### Step 6: Test the assistant (~10 minutes)
1. Open the **Test** pane (refresh it if needed).
2. Type a trigger phrase: `I'd like a quote`.
3. Answer each question in turn:
   - Name: `Mei Ling`
   - Company: `BrightTech`
   - Product: `Air Fryer Pro`
   - Quantity: `25`
4. Confirm the agent returns the structured summary with all four values filled in.
5. Try the **unhappy path**: enter text instead of a number for quantity, and observe how the agent re-asks. Adjust the question if needed.

---

## Checkpoint
- ✅ Agent **Sales Enquiry Assistant** with a **New Sales Enquiry** topic
- ✅ Four variables captured: `customerName`, `company`, `product`, `quantity`
- ✅ A structured summary returned in testing

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Topic doesn't trigger | Add more trigger phrases; type something close to them. |
| Variable shows blank in summary | Ensure you inserted the **variable**, not plain text; check the **Save as** name. |
| Quantity rejected | Set the question's **Identify** to **Number**; enter digits like `25`. |
| Agent goes off-topic | Tighten the instructions to steer back to the enquiry. |

## Key Takeaways
- **Topics** start from **trigger phrases**.
- **Question nodes** capture answers into **variables** — the basis of structured data.
- A confirmation summary builds user trust and verifies the captured data.

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 6: Procurement Request Workflow](../Lab%206%20-%20Procurement%20Request%20Workflow/index.md), where you'll connect a capturing agent to a Power Automate flow.

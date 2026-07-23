# Lab 1: Automated Email Workflow

## Lab Title
Build an Automated Email Workflow in Power Automate

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a flow from a blank canvas in Power Automate's new designer
2. Configure a **manual trigger** with a text **input**
3. Add a **Send an email (V2)** action and create an Office 365 Outlook **connection**
4. Use **dynamic content** to insert the input value into the email body
5. **Save**, then **Test → Run** the flow and confirm the email is delivered
6. Read the **run history** to verify each step succeeded

## Prerequisites
- Completed [Lab 0](../Lab%200%20-%20Environment%20Setup/index.md) (accounts ready)
- Signed in at <a href="https://make.powerautomate.com" target="_blank" rel="noopener">https://make.powerautomate.com</a> with **NUS Copilot Sandbox** selected (top-right)
- Outlook working with your account (a mailbox-enabled account)

## Scenario
At **ACME Pte Ltd**, every customer enquiry should get an instant, personalized "thank you" reply so customers know they've been heard. In this lab you build the simplest possible automation — a flow you start by hand that emails a personalized confirmation. It teaches the core pattern you'll reuse all course long: **Trigger → Action → Output**.

---

## Step-by-Step Guide

### Step 1: Start a new flow (~5 minutes)
1. Go to **<a href="https://make.powerautomate.com" target="_blank" rel="noopener">https://make.powerautomate.com</a>** and sign in.
2. Confirm the **Environment selector** (top-right) shows **NUS Copilot Sandbox** — the environment from Lab 0.
3. In the left menu, select **Create**.
4. Under "Start from blank", select **Instant cloud flow**.

   > **Tip:** An **instant** flow is started manually by clicking a button — perfect for learning and testing. Later labs use automatic triggers (a form submission, a new email, etc.).

5. In the dialog box:
   - **Flow name:** `Lab 1 - Send Confirmation Email`
   - **Choose how to trigger this flow:** select **Manually trigger a flow**
6. Select **Create**. The new designer opens with one step already on the canvas: the trigger **Manually trigger a flow**.

### Step 2: Add an input to the trigger (~5 minutes)
We'll let whoever runs the flow type a customer name, so the email can be personalized.

1. Select the trigger card **Manually trigger a flow** to open its panel on the right.
2. Select **+ Add an input**.
3. From the type list, choose **Text**.
4. Replace the default input name with `CustomerName`.

> **Tip:** This input becomes one of the trigger's **outputs** — a piece of data you can drop into later steps using dynamic content.

### Step 3: Add the Send an email action (~10 minutes)
1. Below the trigger, select the **+** (plus) button, then **Add an action**.
2. In the search box, type **Send an email**.
3. Select the **Office 365 Outlook** connector, then choose the action **Send an email (V2)**.

   > **⚠️ Warning:** Pick **Office 365 Outlook**, not Gmail, Outlook.com, or SMTP. Only Office 365 Outlook uses your course work account.

4. If this is your first use of the connector, Power Automate creates a **connection**: select **Sign in**, choose your course account, and approve. A green ✓ next to the connection means it's ready.
5. Configure the email fields in the action panel:
   - **To:** type your own email address (so you receive the test).
   - **Subject:** type `Thank you for your enquiry`
   - **Body:** build the message with the name inserted dynamically:
     1. Click inside the **Body** field and type: `Hi ` (with a trailing space)
     2. Select the **dynamic content** icon (the small lightning bolt) that appears in/next to the field.
     3. From the list, under **Manually trigger a flow**, choose **CustomerName**. It appears as a coloured **token** (chip) in the field.
     4. Click after the token and continue typing: `, thank you for reaching out to ACME Pte Ltd. We have received your enquiry and a team member will respond within 1 business day.`

> **Tip:** **Dynamic content** is how outputs from earlier steps get reused. The coloured `CustomerName` token is a placeholder — it's replaced with the real value when the flow runs.

> **⚠️ Warning — don't paste stray characters.** Type the text yourself; don't copy backticks (`` ` ``) or quotation marks from this guide into the field, or they'll appear literally in the email.

### Step 4: Save and test (~5 minutes)
1. Select **Save** (top-right).

   > **Tip:** There is **no separate "Send" button**. Running the flow *is* what sends the email — the *Send an email* action does the work. So the routine is always: **Save**, then **Test → Run flow**.

2. Select **Test** (top-right) → choose **Manually** → **Test** → **Run flow**.
3. Power Automate prompts for the input you defined:
   - **CustomerName:** type `Jane Tan`
4. Select **Run flow**, then **Done**.
5. Watch the run status — each step should show a **green check**.
6. Open **Outlook** and confirm the email arrived, personalized as "Hi Jane Tan".

### Step 5: Review the run history (~5 minutes)
1. In the left menu, select **My flows**, then open **Lab 1 - Send Confirmation Email**.
2. Look at the **28-day run history** — you'll see your test run with a status.
3. Select the run to inspect each step's **inputs and outputs**. This is how you debug flows: a **green check** = success; a **red ⚠️** = error (click it to read the message).

---

## Checkpoint
You should now have:
- ✅ A flow named **Lab 1 - Send Confirmation Email** with a `CustomerName` text input
- ✅ An Office 365 Outlook connection showing a green ✓
- ✅ A successful test run (all steps green)
- ✅ A personalized email received in Outlook reading "Hi Jane Tan, …"

## Troubleshooting
| Problem | Solution |
|---------|----------|
| No "Send an email (V2)" action listed | Make sure you selected the **Office 365 Outlook** connector (not Gmail / Outlook.com / SMTP). |
| Action fails with **"Unauthorized"** | The Office 365 Outlook connection is broken/expired, **or** the signed-in account has **no mailbox**. Open the action's connection, **reconnect** with a mailbox-enabled account (green ✓). |
| Connection shows a red ⚠️ | The connection needs to be re-authorized — select it and **reconnect** / sign in again. |
| Email not received | Check Junk/Spam; confirm the **To** address; re-run the test. |
| Can't find dynamic content | Click directly **inside** the Body field first, then open the lightning-bolt menu. |
| `CustomerName` shows as plain text, not a token | Delete it and re-insert it from the dynamic content list so it becomes a coloured token. |
| Clicked "Save" but no email arrived | Saving does not send. You must **Test → Run flow** — running the flow performs the action. |

## Key Takeaways
- Every flow follows the pattern **Trigger → Actions**.
- Trigger **inputs** become **outputs** that you reuse in later steps via **dynamic content** tokens.
- A connector needs a **connection**: green ✓ = ready, red ⚠️ = reconnect. **"Unauthorized"** on *Send an email* means the Outlook connection is broken or the account has no mailbox.
- There is **no separate Send button** — **Save**, then **Test → Run** to make the actions happen.
- **Test** + **run history** are your tools for verifying and debugging.

## Duration
~30 minutes

## Next Steps
Proceed to [Lab 2: Excel Data Logging Workflow](../Lab%202%20-%20Excel%20Data%20Logging%20Workflow/index.md).

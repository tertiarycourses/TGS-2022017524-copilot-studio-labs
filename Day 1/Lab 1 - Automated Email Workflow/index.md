# Lab 1: Automated Email Workflow

## Lab Title
Build an Automated Email Workflow in Power Automate

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a flow from a blank canvas in Power Automate
2. Choose and configure a **trigger**
3. Add a **Send an email** action
4. Use **dynamic content** to insert data from the trigger into the email
5. Test the flow and confirm the email is delivered

## Prerequisites
- Completed [Lab 0](../Lab%200%20-%20Environment%20Setup/index.md) (accounts ready)
- Signed in at https://make.powerautomate.com
- Outlook working with your account

## Scenario
You want a confirmation email to be sent automatically whenever you manually start the flow (e.g. for testing) — and later, whenever a real event happens. This is the simplest possible automation and teaches the core pattern: **Trigger → Action → Output**.

---

## Step-by-Step Guide

### Step 1: Start a new flow (~5 minutes)
1. Go to **https://make.powerautomate.com** and sign in.
2. Confirm your **environment** (top-right) is the one from Lab 0.
3. In the left menu, select **Create**.
4. Under "Start from blank", select **Instant cloud flow**.

   > An **instant** flow is started manually by clicking a button — perfect for learning and testing. (Later labs use automatic triggers.)

5. In the dialog:
   - **Flow name:** `Lab 1 - Send Confirmation Email`
   - **Choose how to trigger this flow:** select **Manually trigger a flow**
6. Select **Create**. The flow designer opens with one step already added: the trigger **Manually trigger a flow**.

### Step 2: Add an input to the trigger (~5 minutes)
We'll let the person who runs the flow type a customer name, so the email can be personalized.

1. Select the trigger card **Manually trigger a flow** to expand it.
2. Select **+ Add an input**.
3. Choose **Text**.
4. Name the input `CustomerName`.
5. (Optional) Add a second **Text** input named `CustomerEmail`.

> These inputs are the trigger's **outputs** — data that flows into the next steps.

### Step 3: Add the Send an email action (~10 minutes)
1. Below the trigger, select **+ New step** (or the **+** between cards).
2. In the search box, type **Send an email**.
3. Select the **Office 365 Outlook** connector, then choose the action **Send an email (V2)**.
4. If asked, **sign in** to create the Outlook connection (use your course account). Select **Continue**.
5. Configure the email fields:
   - **To:** your own email address (so you receive the test). If you added `CustomerEmail`, you can use that instead.
   - **Subject:** `Thank you for your enquiry`
   - **Body:** type the message and insert the name dynamically:
     1. Click into the **Body** field and type: `Hi `
     2. Select the **dynamic content** icon (lightning bolt) or the **/** menu.
     3. Choose **CustomerName** from the list (under "Manually trigger a flow").
     4. Continue typing: `, thank you for reaching out. We have received your enquiry and a team member will respond within 1 business day.`

> **Dynamic content** is how outputs from earlier steps get reused. The `CustomerName` chip will be replaced with the real value when the flow runs.

### Step 4: Save and test (~10 minutes)
1. Select **Save** (top-right).
2. Select **Test** (top-right) → choose **Manually** → **Test** → **Run flow**.
3. Power Automate asks for the inputs you defined:
   - **CustomerName:** `Jane Tan`
   - (**CustomerEmail:** your email, if you added it)
4. Select **Run flow**, then **Done**.
5. Watch the run status — each step should show a **green check**.
6. Open **Outlook** and confirm the email arrived, personalized with "Hi Jane Tan".

### Step 5: Review the run history (~5 minutes)
1. Go to **My flows** → open **Lab 1 - Send Confirmation Email**.
2. Look at the **28-day run history** — you'll see your test run.
3. Select the run to inspect each step's **inputs and outputs**. This is how you debug flows: green = success, red = error (click to read the message).

---

## Checkpoint
You should now have:
- ✅ A flow named **Lab 1 - Send Confirmation Email**
- ✅ A successful test run (all green checks)
- ✅ A personalized email received in Outlook

## Troubleshooting
| Problem | Solution |
|---------|----------|
| No "Send an email (V2)" action | Make sure you picked the **Office 365 Outlook** connector (not Gmail/SMTP). |
| Email not received | Check Junk/Spam; confirm the **To** address; re-run the test. |
| Connection error | Re-create the Outlook connection and sign in again. |
| Can't find dynamic content | Click directly inside the Body field first, then open the lightning-bolt menu. |

## Key Takeaways
- Every flow = **Trigger → Actions**.
- **Inputs/outputs** carry data between steps via **dynamic content**.
- **Test** + **run history** are your tools for verifying and debugging.

## Duration
~30 minutes

## Next Steps
Proceed to [Lab 2: Excel Data Logging Workflow](../Lab%202%20-%20Excel%20Data%20Logging%20Workflow/index.md).

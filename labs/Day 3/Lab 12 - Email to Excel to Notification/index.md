# Lab 12: Email Enquiry → Excel Logging → Notification

## Lab Title
End-to-End Workflow: Capture an Email Enquiry, Log It, and Notify the Team

## Lab Objectives
By the end of this lab, you will be able to:
1. Create an **automated cloud flow** that starts on its own when an email arrives
2. Configure the **When a new email arrives (V3)** trigger with an optional subject filter
3. **Log** each enquiry as a new row in an Excel table, with a clean timestamp
4. **Notify** the sales team automatically with the enquiry details
5. Orchestrate the classic **Capture → Log → Notify** pattern into one hands-off workflow

## Prerequisites
- Completed Day 1 Labs 1–2 (email + Excel actions)
- An Excel `Enquiry Log` with table `EnquiryTable` (from Lab 2) — or create one (Date, Name, Email, Message, Status)

## Scenario
ACME Pte Ltd receives customer enquiries by email to a shared inbox. Right now, staff copy each enquiry into a spreadsheet by hand and forget to tell the sales team. In this lab you will build an automated flow in the **NUS Copilot Sandbox** environment that, the moment an enquiry email arrives, **logs it to Excel** and **emails the sales team** — completely hands-off. This is the classic **Capture → Log → Notify** pattern.

---

## Step-by-Step Guide

### Step 1: Create an automated cloud flow (~5 minutes)
1. In your browser, go to **<a href="https://make.powerautomate.com" target="_blank" rel="noopener">https://make.powerautomate.com</a>** and sign in.
2. Top-right, confirm the environment selector shows **NUS Copilot Sandbox**. If it shows a different environment, click it and switch — every tool in this course uses the same environment.
3. In the left menu, select **Create**.
4. Under **Start from blank**, select **Automated cloud flow**.
5. In the **Build an automated cloud flow** dialog:
   - **Flow name:** `Lab 12 - Email Enquiry to Excel and Notify`
   - In **Choose your flow's trigger**, type `when a new email arrives` in the search box.
   - Select **When a new email arrives (V3)** under **Office 365 Outlook**.
6. Select **Create**.

> **Tip:** If this is your first Office 365 / Excel action, Power Automate may ask you to sign in to create a **connection**. Always sign in with your own course account. A working connection shows a green ✓ — you will rely on this later.

### Step 2: Configure the email trigger (~10 minutes)
1. The flow opens in the new designer with the trigger card already placed. Select the **When a new email arrives (V3)** card to open its panel on the right.
2. Set:
   - **Folder:** `Inbox` (use the folder picker — do not type it)
   - **Importance:** `Any`
   - **Only with Attachments:** `No`
   - **Include Attachments:** `No`
3. Select **Show advanced options** (or **Show all**) to reveal more fields, then set:
   - **Subject Filter:** `Enquiry`
   - This means only emails whose subject contains the word **Enquiry** will start the flow — which keeps your log clean while testing.

> **Tip:** Without a subject filter, **every** incoming email starts the flow. During training, set a filter so unrelated mail (newsletters, replies) does not flood your Excel log.

### Step 3: Log the enquiry to Excel (~12 minutes)
1. Under the trigger card, select the **+** (plus) → **Add an action**.
2. Search `add a row into a table` and select **Add a row into a table** under **Excel Online (Business)**.
3. In the action panel set:
   - **Location:** `OneDrive for Business`
   - **Document Library:** `OneDrive`
   - **File:** browse to and select **Enquiry Log.xlsx**
   - **Table:** select **EnquiryTable** from the dropdown
4. The five table columns (Date, Name, Email, Message, Status) now appear. Map them:
   - **Name:** click the field, then from **Dynamic content** insert **From** (or **From** display name if you prefer)
   - **Email:** insert **Dynamic content → From**
   - **Message:** insert **Dynamic content → Body preview**
   - **Status:** type `New`
5. For the **Date** column, enter an expression so the timestamp is clean:
   - Click the **Date** field, then open the **fx** (Expression) editor.
   - Type exactly: `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')`
   - Select **Add** (or **OK**). The field now shows a blue **fx token**, not the raw text.

> **⚠️ Warning:** Enter the date through the **fx** editor so it becomes a token. If you type `formatDateTime(...)` directly into the box as plain text, Excel stores the literal text and you get a meaningless string instead of a date.

### Step 4: Notify the sales team (~10 minutes)
1. Under the Excel action, select **+** → **Add an action**.
2. Search `send an email` and select **Send an email (V2)** under **Office 365 Outlook**.
3. Configure:
   - **To:** the sales team address — for testing, use your own email
   - **Subject:** type `New enquiry received: ` then insert **Dynamic content → Subject**
   - **Body:** type the message below, inserting the matching **Dynamic content** tokens where shown in braces:
     ```
     A new enquiry has arrived and been logged.

     From: [From]
     Subject: [Subject]
     Message: [Body preview]

     Status: New — please follow up.
     ```
4. Select **Save** (top right).

> **⚠️ Warning:** If saving or testing later shows **"Unauthorized"** on the Send an email action, your Office 365 Outlook connection has expired or used the wrong account. Open the action's **…** menu → **My connections** (or the connection link at the bottom of the panel) and **reconnect** with a **mailbox-enabled** account. Every connection must show a green ✓ before the flow will run.

### Step 5: Test the end-to-end workflow (~10 minutes)
1. Top right, select **Test** → **Manually** → **Test**.
2. From another account (or the same one), **send an email** to your inbox with:
   - **Subject:** `Enquiry - bulk order`
   - **Body:** a short sentence, e.g. `Hi, I'd like a quote for 200 units.`
3. Within about a minute the flow should trigger. Confirm:
   - Every step shows a **green ✓** in the run view.
   - A **new row** appears in **Enquiry Log.xlsx** with the sender, message, and a readable date/time.
   - The **notification email** arrives with the enquiry details.
4. Now send a **second** test email **without** the word "Enquiry" in the subject (e.g. subject `Hello`). Confirm the flow does **not** run — proving the subject filter works.

> **Tip:** If the new Excel row shows `########` in the Date column, the column is just too narrow. Double-click the column border in Excel to auto-fit — the value is correct.

### Step 6: Review and harden (~3 minutes)
1. In the left menu, open **My flows** → **Lab 12 - Email Enquiry to Excel and Notify** → the latest run to inspect inputs and outputs of each step.
2. Discuss optional improvements:
   - Add a **Condition** to flag high-priority enquiries (e.g. subject contains "urgent").
   - Capture the sender's display name in a separate column.

---

## Checkpoint
- ✅ Automated flow triggered by an **incoming email**
- ✅ Each matching email → **new Excel row** with a clean timestamp
- ✅ Each matching email → **team notification email**
- ✅ Non-matching emails are correctly **ignored** by the subject filter

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Flow doesn't trigger | Confirm the email reached the **Inbox** and the subject contains `Enquiry`; triggers can take up to a minute. |
| "Unauthorized" on Send an email | Reconnect the **Office 365 Outlook** connection with a mailbox-enabled account; every connection must be green ✓. |
| Date shows raw text like `formatDateTime(...)` | You typed it as text. Re-enter it via the **fx** editor so it becomes a blue token. |
| Date column shows `########` | The column is too narrow — double-click the column border in Excel to auto-fit. |
| Empty Excel fields | Map to the **trigger's** dynamic content (From / Subject / Body preview), not static text. |
| Too many rows logged | Add or tighten the **Subject Filter** on the trigger. |
| No notification email | Check **Junk**; verify the **To** address; check run history for errors. |

## Key Takeaways
- Automated triggers (an **email arrives**) make workflows run with zero clicks.
- One trigger can fan out into multiple actions — **log** and **notify** in a single flow.
- Use the **fx** editor for dates so Excel stores a real, readable timestamp.
- Subject filters keep automation focused and your data clean.

## Duration
~40 minutes

## Next Steps
Proceed to [Lab 13: Invoice Upload → Approval Workflow](../Lab%2013%20-%20Invoice%20Upload%20Approval/index.md).

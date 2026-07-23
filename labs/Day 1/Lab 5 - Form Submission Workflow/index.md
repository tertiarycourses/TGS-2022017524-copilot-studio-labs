# Lab 5: Form Submission Workflow

## Lab Title
Capture Microsoft Forms Submissions to Email and Excel (Automatic Trigger)

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a **Microsoft Form** with three required questions and a shareable **URL**
2. Build a flow using the **When a new response is submitted** trigger (Microsoft Forms)
3. Add **Get response details** to read each answer (mapping the Response Id)
4. **Email** the submitted enquiry to your team
5. **Log** the same enquiry into the Excel **EnquiryTable** — all automatically on submit

## Prerequisites
- Completed [Lab 1](../Lab%201%20-%20Automated%20Email%20Workflow/index.md) (Send an email) and [Lab 2](../Lab%202%20-%20Excel%20Data%20Logging%20Workflow/index.md) (Excel table + logging)
- An Excel **Enquiry Log** workbook with table **EnquiryTable** (Date, Name, Email, Message, Status) from Lab 2
- Signed in at **make.powerautomate.com** in the **NUS Copilot Sandbox** environment

## Scenario
At **ACME Pte Ltd**, customers fill in an online enquiry form. The moment they **submit**, the workflow should **email the team** the new enquiry **and record it in Excel** — with no manual work. This is your first **automatic, event-driven** workflow (Labs 1–3 were manual, Lab 4 was scheduled). You'll also get a **form link** you can send to anyone.

---

## Step-by-Step Guide

### Step 1: Create the form in Microsoft Forms (~10 minutes)
1. Open a new browser tab and go to **<a href="https://forms.office.com" target="_blank" rel="noopener">https://forms.office.com</a>**.
2. Sign in with the **same account** you use for Power Automate in the **NUS Copilot Sandbox** tenant.
3. Click **+ New Form**.
4. Click the title at the top and enter: `Customer Enquiry Form`.
5. Add a short description, e.g. `Tell us about your enquiry and we'll respond within 1 business day.`
6. Add these three questions. For each, click **+ Add new**, choose **Text**, type the question, then toggle **Required** on:
   - `Full Name` → **Required** on
   - `Email` → **Required** on
   - `Your Message` → click the **…** on the question and choose **Long answer** for more space → **Required** on
7. The form saves automatically as you type.

> **Tip:** Keep the question titles exactly as shown — you'll match them to Excel columns later, and clear names make the dynamic tokens easy to find.

### Step 2: Get the shareable form URL (~5 minutes)
1. Top-right of Forms, click **Collect responses** (older UI: **Share**).
2. Set the audience — for testing choose **Anyone can respond** (or your organization).
3. Copy the **link** shown (e.g. `https://forms.office.com/r/XXXXXXXX`).
4. **Save this URL** somewhere — it's the link you'd send to customers, and you'll use it to test at the end.

### Step 3: Create the automated flow (~5 minutes)
1. Go back to **<a href="https://make.powerautomate.com" target="_blank" rel="noopener">https://make.powerautomate.com</a>** (confirm the environment is **NUS Copilot Sandbox**).
2. Left menu → **+ Create** → **Automated cloud flow**.
3. **Flow name:** `Lab 5 - Form Submission to Email and Excel`.
4. In "Choose your flow's trigger", search `Forms` and select **When a new response is submitted** (Microsoft Forms).
5. Click **Create**.
6. On the trigger card, set **Form Id** → pick **Customer Enquiry Form** from the dropdown.

### Step 4: Get the response details (~10 minutes)
The trigger only gives you a response **Id** — you need another action to read the actual answers.

1. Below the trigger, click **+** → **Add an action**.
2. Search `Forms` → select **Get response details** (Microsoft Forms).
3. Configure:
   - **Form Id:** pick **Customer Enquiry Form** (the same form)
   - **Response Id:** click the field, open dynamic content (lightning bolt), and insert **Response Id** (from the trigger)

> **⚠️ Warning:** **Get response details** is **required**. Without it, later steps only see an internal Id, not the real answers — and your email/Excel will be blank. Always map **Response Id** from the trigger, then use **this action's** outputs (Full Name, Email, Your Message) in every step that follows.

### Step 5: Email the submission to your team (~10 minutes)
1. Click **+** → **Add an action**.
2. Select **Send an email (V2)** (Office 365 Outlook). Complete the connection if prompted (it must show a green check).
3. Configure (insert each value from **Get response details** dynamic content):
   - **To:** your team's address (use your own working mailbox for testing)
   - **Subject:** type `New enquiry from ` then insert **Full Name**
   - **Body:**
     ```
     A new enquiry was submitted via the form:
     Name: [insert Full Name]
     Email: [insert Email]
     Message: [insert Your Message]
     ```

> **⚠️ Warning:** If you get an **Unauthorized** error, the Outlook connection is broken or the account has no mailbox. Reconnect **Office 365 Outlook** with a mailbox-enabled account (see [Lab 1](../Lab%201%20-%20Automated%20Email%20Workflow/index.md)); the connection must show a green ✓.

### Step 6: Log the submission to Excel (~10 minutes)
1. Click **+** → **Add an action**.
2. Select **Add a row into a table** (Excel Online (Business)). Complete the connection if prompted.
3. Set the location:
   - **Location:** OneDrive for Business
   - **Document Library:** OneDrive
   - **File:** browse to **Enquiry Log** (the `.xlsx` workbook)
   - **Table:** `EnquiryTable`
4. Map the columns:
   - **Date:** click the **fx** (expression) icon → enter exactly `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')` → click **Add / OK** so it becomes a **token** (a highlighted chip), never typed text
   - **Name:** dynamic content → **Full Name**
   - **Email:** dynamic content → **Email**
   - **Message:** dynamic content → **Your Message**
   - **Status:** type `New`
5. Top-right, click **Save**.

> **⚠️ Warning:** The **Date** value must be entered through the **fx** editor and become a token. If you type the formula as plain text, the cell stores the literal text `formatDateTime(...)` instead of a real date. (This is the same fix from Lab 2.)

### Step 7: Test the whole workflow (~10 minutes)
1. In Power Automate, click **Test** → **Manually** → **Test**. The flow goes into a "waiting for trigger" state.
2. Open the **form URL** you saved in Step 2 (new tab or your phone).
3. Fill in the form — Full Name `Jane Tan`, Email `jane@example.com`, Your Message `Interested in 50 units` — and click **Submit**.
4. Within about a minute the flow triggers. Confirm:
   - Every step shows a green check in the run.
   - The **email** arrives with the submitted details.
   - A **new row** appears in **Enquiry Log** → **EnquiryTable** with a clean date, the answers, and **Status** `New`.
5. Submit the form a **second time** with different details and confirm another row and another email.

> **Tip:** Triggers can take up to a minute. If nothing happens, confirm you clicked **Test** *before* submitting — or just submit again, since a saved flow fires automatically on every real submission.

---

## Checkpoint
- ✅ A **Customer Enquiry Form** with three required questions and a shareable URL
- ✅ Automated flow triggered by **When a new response is submitted**
- ✅ **Get response details** mapping the **Response Id** from the trigger
- ✅ Each submission → **notification email** to the team **and** a **new row** in **EnquiryTable** (Date via fx token)

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Form not listed in the trigger | Sign into Power Automate with the **same account** that owns the form, in the **NUS Copilot Sandbox** environment. |
| Answers show as IDs / blank | You must add **Get response details**, map **Response Id** from the trigger, and use **its** outputs (not the trigger's) in later steps. |
| Flow doesn't trigger after submit | Triggers can take up to a minute; confirm **Test** was started before submitting, or submit again (a saved flow fires automatically). |
| Date shows literal text | Enter the date through the **fx** editor so it becomes a token (see [Lab 2](../Lab%202%20-%20Excel%20Data%20Logging%20Workflow/index.md)). |
| Send email **Unauthorized** | Reconnect **Office 365 Outlook** with a mailbox-enabled account; the connection must show green ✓. |
| Add a row **Unauthorized** | Reconnect **Excel Online (Business)** with an account that can access the Enquiry Log workbook. |

## Key Takeaways
- A **Microsoft Forms** trigger turns a public form into an automatic workflow — no buttons to press.
- **Get response details** is required to read the individual answers behind the Response Id.
- The **Date** column is filled by an **fx** token (`formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')`), never typed text.
- One submission can fan out to **multiple actions** (notify **and** log) — the core pattern for Day 3.

## Duration
~50 minutes

## Next Steps
You've completed Day 1 and all the core Power Automate trigger types (manual, scheduled, form, email). Proceed to [Day 2 — Module 3: Business Agents Concepts](../../Day%202/Module%203%20-%20Business%20Agents%20Concepts.md).

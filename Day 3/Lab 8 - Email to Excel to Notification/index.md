# Lab 8: Email Enquiry → Excel Logging → Notification

## Lab Title
End-to-End Workflow: Capture an Email Enquiry, Log It, and Notify the Team

## Lab Objectives
By the end of this lab, you will be able to:
1. Use an **automated trigger** — *When a new email arrives*
2. Extract details from the incoming email (sender, subject, body)
3. **Log** the enquiry into an Excel table
4. **Notify** the sales team with the details
5. Orchestrate three steps into one automatic, end-to-end workflow

## Prerequisites
- Completed Day 1 Labs 1–2 (email + Excel actions)
- An Excel `Enquiry Log` with table `EnquiryTable` (from Lab 2) — or create one (Date, Name, Email, Message, Status)

## Scenario
Customers email enquiries to a shared inbox. You want every enquiry **automatically logged** and the **team notified** the moment it arrives — the classic *Capture → Log → Notify* pattern, fully hands-off.

---

## Step-by-Step Guide

### Step 1: Create an automated cloud flow (~5 minutes)
1. **https://make.powerautomate.com** → **Create** → **Automated cloud flow**.
2. **Flow name:** `Lab 8 - Email Enquiry to Excel and Notify`.
3. In "Choose your flow's trigger", search **When a new email arrives** and select **When a new email arrives (V3)** (Office 365 Outlook).
4. Select **Create**.

### Step 2: Configure the email trigger (~10 minutes)
1. On the trigger card, set:
   - **Folder:** `Inbox`
   - **Importance:** `Any`
   - (Optional) **Subject Filter:** `Enquiry` — so only emails with "Enquiry" in the subject start the flow. This keeps your log clean during testing.
2. Leave attachments off for now.

> **Why a subject filter?** Without it, *every* incoming email triggers the flow. A filter focuses automation on real enquiries.

### Step 3: Log the enquiry to Excel (~10 minutes)
1. **+ New step** → **Excel Online (Business) → Add a row into a table**.
2. Location **OneDrive for Business**, Library **OneDrive**, File **Enquiry Log.xlsx**, Table **EnquiryTable**.
3. Map columns using the trigger's dynamic content:
   - **Date:** Expression `utcNow()`
   - **Name:** dynamic content **From** (the sender's address) — or **From** display name if available
   - **Email:** **From**
   - **Message:** **Body preview** (or **Body**)
   - **Status:** `New`

### Step 4: Notify the sales team (~10 minutes)
1. **+ New step** → **Office 365 Outlook → Send an email (V2)**.
2. Configure:
   - **To:** the sales team address (use your own email for testing)
   - **Subject:** `New enquiry received: ` + dynamic content **Subject**
   - **Body:**
     ```
     A new enquiry has arrived and been logged.
     From: {From}
     Subject: {Subject}
     Message: {Body preview}
     Status: New — please follow up.
     ```
3. **Save** the flow.

### Step 5: Test the end-to-end workflow (~10 minutes)
1. Select **Test → Manually → Test**.
2. From another account (or the same one), **send an email** to your inbox with subject `Enquiry - bulk order` and a short body.
3. Within a minute, the flow should trigger. Confirm:
   - All steps are **green** in the run.
   - A **new row** appears in **Enquiry Log.xlsx** with the sender, message, and timestamp.
   - The **notification email** arrives with the enquiry details.
4. Send a second test email **without** "Enquiry" in the subject and confirm it is **ignored** (filter working).

### Step 6: Review and harden (~5 minutes)
1. Open **My flows → Lab 8 → run history** to inspect inputs/outputs.
2. Discuss improvements (optional):
   - Add a **Condition** to flag high-priority enquiries (e.g. subject contains "urgent").
   - Add a second row mapping to capture the sender's display name separately.

---

## Checkpoint
- ✅ Automated flow triggered by **incoming email**
- ✅ Each matching email → **new Excel row**
- ✅ Each matching email → **team notification**
- ✅ Non-matching emails correctly ignored

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Flow doesn't trigger | Confirm the email reached the **Inbox** and matches the **subject filter**; triggers can take up to a minute. |
| Empty Excel fields | Map to the **trigger's** dynamic content (From / Subject / Body preview). |
| Too many rows logged | Add or tighten the **subject filter**. |
| No notification | Check Junk; verify the **To** address; check run history. |

## Key Takeaways
- Automated triggers (**email arrives**) make workflows run with zero clicks.
- One trigger can fan out into multiple actions (log **and** notify).
- Filters keep automation focused and your data clean.

## Duration
~40 minutes

## Next Steps
Proceed to [Lab 9: Invoice Upload → Approval Workflow](../Lab%209%20-%20Invoice%20Upload%20Approval/index.md).

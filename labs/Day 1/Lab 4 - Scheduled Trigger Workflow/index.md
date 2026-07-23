# Lab 4: Scheduled Trigger Workflow

## Lab Title
Build a Scheduled (Recurring) Workflow with Power Automate

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a **Scheduled cloud flow** that uses the **Recurrence** trigger
2. Configure the Interval, Frequency, **Time zone**, hours, and specific days
3. Send a **daily reminder email** automatically on a timetable
4. **Test/Run now** without waiting for the scheduled time
5. (Optional stretch) Read the Excel **EnquiryTable** and include a live **count** in the email

## Prerequisites
- Completed [Lab 1](../Lab%201%20-%20Automated%20Email%20Workflow/index.md) (Send an email)
- *(For the optional stretch)* An Excel **Enquiry Log** workbook with table **EnquiryTable** from [Lab 2](../Lab%202%20-%20Excel%20Data%20Logging%20Workflow/index.md)
- Signed in at **make.powerautomate.com** in the **NUS Copilot Sandbox** environment

## Scenario
At **ACME Pte Ltd**, some work isn't triggered by an event — it just needs to happen **on a schedule**. Every **weekday morning** the team should get a reminder to review new enquiries. You will build a flow that runs automatically using the **Recurrence** trigger, so no one has to start it.

> **Tip:** Trigger types so far — **manual** (Labs 1–3, you press Run) and **scheduled** (this lab, runs by the clock). Lab 5 adds an **event** trigger (a form submission).

---

## Step-by-Step Guide

### Step 1: Create a scheduled flow (~6 minutes)
1. Go to **<a href="https://make.powerautomate.com" target="_blank" rel="noopener">https://make.powerautomate.com</a>**.
2. Top-left, confirm the environment selector reads **NUS Copilot Sandbox**. If not, click it and switch.
3. In the left menu, click **+ Create**.
4. Under "Start from blank", click **Scheduled cloud flow**.
5. In the dialog:
   - **Flow name:** `Lab 4 - Daily Enquiry Reminder`
   - **Starting:** today's date and any time
   - **Repeat every:** `1` and **Day**
6. Click **Create**. The designer opens with a **Recurrence** trigger already added.

### Step 2: Fine-tune the schedule (~10 minutes)
1. Click the **Recurrence** trigger card to open it.
2. Set the basics:
   - **Interval:** `1`
   - **Frequency:** `Day`
3. Click **Show advanced options** and set:
   - **Time zone:** `(UTC+08:00) Kuala Lumpur, Singapore`
   - **At these hours:** `9`
   - **At these minutes:** `0`
   - **On these days:** tick **Monday, Tuesday, Wednesday, Thursday, Friday** (leave Saturday and Sunday unticked)
4. The schedule now reads: **every weekday at 9:00 AM Singapore time**.

> **⚠️ Warning:** You MUST set the **Time zone**. Without it, the Recurrence trigger uses **UTC**, so a "9" would fire at 9:00 UTC = 5:00 PM Singapore — the wrong local time. This is the same UTC-vs-local trap from Lab 2.

### Step 3: Send the reminder email (~8 minutes)
1. Below the Recurrence trigger, click **+** → **Add an action**.
2. Search `send an email` and select **Send an email (V2)** (from **Office 365 Outlook**). Complete the connection if prompted (it must show a green check).
3. Configure:
   - **To:** your team's address (use your own mailbox for testing)
   - **Subject:** `Daily reminder: review new enquiries`
   - **Body:**
     ```
     Good morning,
     This is your daily reminder to review and follow up on new enquiries
     in the Enquiry Log. Please action any items marked "New".
     ```
4. Top-right, click **Save**.

> **⚠️ Warning:** If you hit an **Unauthorized** error, the Outlook connection is broken or the account has no mailbox. Reconnect **Office 365 Outlook** with a mailbox-enabled account (see [Lab 1](../Lab%201%20-%20Automated%20Email%20Workflow/index.md)). The connection must show a green ✓ before running.

### Step 4: Test the flow now (~5 minutes)
You don't have to wait until 9 AM — you can run it on demand to check it works.
1. Top-right, click **Test** → **Manually** → **Test** → **Run flow** → **Done**.
2. Confirm every step shows a green check and the reminder email arrives in your inbox.
3. From now on the flow also runs **automatically** on its schedule.

> **Tip:** A scheduled flow only fires on its timetable in real life — **Test → Run flow** lets you verify it immediately instead of waiting for 9 AM tomorrow.

### Step 5 (Optional stretch): Include a live count from Excel (~15 minutes)
Make the reminder smarter by counting how many enquiries are logged in **EnquiryTable**.

1. **Above** the Send an email action, click **+** → **Add an action**.
2. Search `list rows` and select **List rows present in a table** (from **Excel Online (Business)**).
3. Configure the location:
   - **Location:** OneDrive for Business
   - **Document Library:** OneDrive
   - **File:** browse to **Enquiry Log** (the `.xlsx` workbook)
   - **Table:** `EnquiryTable`
4. Open the **Send an email (V2)** action again. Click into the **Body** where you want the count, then open the **fx** (expression) editor and enter exactly:
   ```
   length(outputs('List_rows_present_in_a_table')?['body/value'])
   ```
   - Click **Add / OK** so it becomes a **token** (highlighted chip), not plain text.
   - Example line: `There are currently ` *(token)* ` enquiries logged.`
5. Click **Save**, then **Test → Run flow** again. The email now shows the live record count.

> **⚠️ Warning:** The name inside `outputs('...')` must match your action's **internal name** exactly, with spaces replaced by underscores. If the expression errors, open the **List rows present in a table** action → **…** menu → check the action name, and adjust `List_rows_present_in_a_table` to match.

---

## Checkpoint
- ✅ A **scheduled** flow **Lab 4 - Daily Enquiry Reminder** using the **Recurrence** trigger
- ✅ Configured for **weekdays at 9:00 AM** with **Time zone (UTC+08:00) Kuala Lumpur, Singapore**
- ✅ A reminder email sent on a successful **Test → Run flow**
- ✅ *(Optional)* A live record count pulled from **EnquiryTable**

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Email arrives at the wrong time | Set **Time zone** in the Recurrence **advanced options** (e.g. (UTC+08:00) Kuala Lumpur, Singapore). Without it the schedule uses UTC. |
| Flow runs every day including weekends | In **On these days**, tick only **Monday–Friday**. |
| Send email **Unauthorized** | Reconnect **Office 365 Outlook** with a mailbox-enabled account; the connection must show green ✓. |
| `length(...)` expression error | Match the name inside `outputs('...')` to the **List rows** action's actual internal name (spaces become underscores). |
| Don't want to wait for the schedule | Use **Test → Manually → Run flow** to run it immediately. |
| Count shows as literal text, not a number | The expression wasn't added via the **fx** editor as a token. Re-enter it through **fx** and confirm it becomes a highlighted chip. |

## Key Takeaways
- The **Recurrence** trigger runs flows automatically on a timetable — no human starts them.
- Always set the **Time zone** so schedules fire at the right local time, not UTC.
- Use **Test → Run flow** to verify a scheduled flow without waiting for its scheduled time.
- Scheduled flows are ideal for digests, reminders, and clean-up jobs.

## Duration
~30 minutes (45 with the optional stretch)

## Next Steps
Proceed to [Lab 5: Form Submission Workflow](../Lab%205%20-%20Form%20Submission%20Workflow/index.md).

# Lab 2: Excel Data Logging Workflow

## Lab Title
Capture Form Data and Log It into Excel with Power Automate

## Lab Objectives
By the end of this lab, you will be able to:
1. Prepare an Excel file with a formatted **Table** in OneDrive
2. Use a **form submission** style trigger to collect data
3. Add an **Add a row into a table** (Excel) action
4. Map trigger outputs into Excel columns using dynamic content
5. Verify each submission appears as a new row

## Prerequisites
- Completed [Lab 1](../Lab%201%20-%20Automated%20Email%20Workflow/index.md)
- Access to Excel via OneDrive (verified in Lab 0)

## Scenario
Every enquiry should be recorded so nothing is lost. You'll build a flow that takes submitted details (name, email, message) and **logs each one as a new row** in an Excel spreadsheet — a running enquiry register.

---

## Step-by-Step Guide

### Step 1: Create the Excel log file with a Table (~10 minutes)
Power Automate can only write to Excel data that is formatted as a **Table**.

1. Go to **https://www.office.com**, open **Excel**, and create a **New blank workbook**.
2. Rename it (top of screen): `Enquiry Log`. It saves automatically to **OneDrive**.
3. In row 1, type these column headers, one per cell:
   - A1: `Date`
   - B1: `Name`
   - C1: `Email`
   - D1: `Message`
   - E1: `Status`
4. Select the range **A1:E1** (or A1:E2 to include one empty row).
5. On the ribbon, select **Insert → Table**.
6. In the dialog, tick **My table has headers**, then select **OK**.
7. (Recommended) With the table selected, open the **Table Design** tab and set **Table Name** to `EnquiryTable`. This makes it easy to find in Power Automate.
8. Close Excel (changes are saved automatically).

### Step 2: Create the flow and trigger (~5 minutes)
We'll use a manual trigger with inputs to *simulate* a submitted form. (Microsoft Forms uses the same pattern — see the note at the end.)

1. Go to **https://make.powerautomate.com** → **Create** → **Instant cloud flow**.
2. **Flow name:** `Lab 2 - Log Enquiry to Excel`
3. Trigger: **Manually trigger a flow** → **Create**.
4. On the trigger card, select **+ Add an input** three times and add:
   - **Text** input named `Name`
   - **Text** input named `Email`
   - **Text** input named `Message`

### Step 3: Add the "Add a row into a table" action (~10 minutes)
1. Select **+ New step**.
2. Search for **Add a row into a table**.
3. Choose the **Excel Online (Business)** connector → action **Add a row into a table**.
4. Sign in / **Continue** if prompted to create the connection.
5. Configure the location of your file:
   - **Location:** `OneDrive for Business`
   - **Document Library:** `OneDrive`
   - **File:** browse to and select **Enquiry Log.xlsx**
   - **Table:** select `EnquiryTable`
6. The action now shows one field per column. Fill them in:
   - **Date:** insert an **expression** for the current date/time (do **not** type it as plain text, or it will log the literal words). With the **Date** box empty, click the **fx** icon (or the **Function / Expression** tab), type the expression below, then click **Add / OK**. It should appear as a colored **token/chip**, not text:
     ```
     formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')
     ```
     This stamps each row with a clean, readable timestamp like `2026-06-23 03:30`.
     > **Tip:** plain `utcNow()` also works but produces a long UTC value such as `2026-06-23T03:30:00.504Z`. The `formatDateTime` version above is shorter and easier to read.
   - **Name:** dynamic content (⚡) → **Name**
   - **Email:** dynamic content (⚡) → **Email**
   - **Message:** dynamic content (⚡) → **Message**
   - **Status:** type the static text `New`

### Step 4: Save and test (~10 minutes)
1. Select **Save**.
2. Select **Test → Manually → Test → Run flow**.
3. Enter sample values:
   - **Name:** `Ahmad Rahman`
   - **Email:** `ahmad@example.com`
   - **Message:** `Interested in a bulk order of 50 units.`
4. **Run flow** → **Done**. Confirm all steps are green.
5. Open **Enquiry Log.xlsx** in Excel — a **new row** should appear with your values and a timestamp.
6. Run the test **2–3 more times** with different values to confirm each submission adds another row.

### Step 5: (Optional) Connect it to a real form (~5 minutes)
To make this a true *form submission* workflow:
1. Create a form at **https://forms.office.com** with questions Name, Email, Message.
2. Build a new flow with the trigger **When a new response is submitted** (Microsoft Forms).
3. Add **Get response details**, then the same **Add a row into a table** action, mapping the Forms answers into the columns.

> This shows the power of triggers: swap the manual trigger for a Forms trigger and the same logging logic runs automatically on every real submission.

---

## Checkpoint
- ✅ `Enquiry Log.xlsx` with a Table named `EnquiryTable`
- ✅ Flow **Lab 2 - Log Enquiry to Excel** runs successfully
- ✅ Multiple test rows logged with timestamps

## Troubleshooting
| Problem | Solution |
|---------|----------|
| File/Table not listed | Ensure the data is formatted as a **Table** (Insert → Table) and saved in OneDrive. |
| Date column shows the literal text `utcNow()` or `formatDateTime(...)` | You typed it into the box as plain text. Clear the box, click the **fx** icon, type the expression in the **Function/Expression** editor, and click **Add** so it becomes a **token/chip**. |
| Row added but columns blank | Re-map each column to the correct dynamic content chip. |
| Date is hard to read (e.g. `2026-06-23T03:30:00.504Z`) | You used plain `utcNow()`. Use `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')` for a short, readable timestamp. |

## Key Takeaways
- Power Automate writes to Excel **Tables**, not loose cells.
- **Expressions** like `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')` must be entered via the **fx editor** (so they become a token), not typed as text.
- The same logging action works behind any trigger (manual, Forms, email, agent).

## Duration
~35 minutes

## Next Steps
Proceed to [Lab 3: Simple Approval Workflow](../Lab%203%20-%20Simple%20Approval%20Workflow/index.md).

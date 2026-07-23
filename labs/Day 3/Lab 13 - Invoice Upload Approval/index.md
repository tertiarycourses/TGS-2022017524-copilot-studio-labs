# Lab 13: Invoice Upload → Approval Workflow

## Lab Title
End-to-End Workflow: Trigger an Approval When an Invoice File Is Uploaded

## Lab Objectives
By the end of this lab, you will be able to:
1. Use a **file upload** trigger — *When a file is created* in OneDrive
2. Pass file details into a **Start and wait for an approval** action
3. Assign the approval to a **real tenant user** so the run succeeds
4. **Branch** on the approval outcome with a Condition
5. **Move the file** and **notify** by outcome, completing the **Upload → Approve → Act** pattern

## Prerequisites
- Completed Day 1 Lab 3 (approvals + conditions)
- Access to OneDrive (to create folders)

## Scenario
At ACME Pte Ltd, staff drop supplier invoices into a shared OneDrive folder, but they sit unseen until someone remembers to check. In this lab you will build an automated flow in the **NUS Copilot Sandbox** environment so that when an invoice lands in **Invoices/Incoming**, finance is asked to **approve or reject** it. Approved invoices move to an **Approved** folder and rejected ones to **Rejected**, with an email sent either way. This is the **Upload → Approve → Act** pattern.

---

## Step-by-Step Guide

### Step 1: Prepare the OneDrive folders (~5 minutes)
1. Go to **<a href="https://www.office.com" target="_blank" rel="noopener">https://www.office.com</a>**, sign in, and open **OneDrive**.
2. Select **+ Add new** → **Folder** and create a folder named `Invoices`.
3. Open the `Invoices` folder and create **three** subfolders inside it:
   - `Incoming`
   - `Approved`
   - `Rejected`
4. Leave `Incoming` empty for now — you will upload a test file later.

> **Tip:** Create all four folders **before** building the flow. The flow's triggers and Move file actions let you browse to these folders, which is far safer than typing paths by hand.

### Step 2: Create the automated flow with a file trigger (~8 minutes)
1. Go to **<a href="https://make.powerautomate.com" target="_blank" rel="noopener">https://make.powerautomate.com</a>** and confirm the environment selector reads **NUS Copilot Sandbox**.
2. In the left menu, select **Create** → **Automated cloud flow**.
3. In the dialog:
   - **Flow name:** `Lab 13 - Invoice Upload Approval`
   - Search `when a file is created` and select **When a file is created** under **OneDrive for Business**.
4. Select **Create**.
5. Select the trigger card to open its panel, then set:
   - **Folder:** use the folder picker (the small folder icon) and browse to `Invoices/Incoming`. Do not type the path.

> **Tip:** The trigger fires whenever a **new** file appears in that exact folder — that is your "upload" event. It does not fire for files already there before the flow was turned on.

### Step 3: Start the approval (~10 minutes)
1. Under the trigger, select **+** → **Add an action**.
2. Search `start and wait for an approval` and select **Start and wait for an approval** under **Approvals**.
3. Configure:
   - **Approval type:** `Approve/Reject - First to respond`
   - **Title:** type `Invoice approval needed: ` then insert **Dynamic content → File name**
   - **Assigned to:** start typing your **own name or course email**, then **pick the matching person from the people-picker dropdown** so it resolves to a **person chip** (a rounded tag with the name).
   - **Details:** type `Please review the uploaded invoice: ` then insert **Dynamic content → File name**.

> **⚠️ Warning:** The **Assigned to** approver MUST be a user that already exists in **this** tenant. Pick the person from the dropdown so it becomes a **person chip** — do **not** type a free-text external email. If you paste an outside address, the run fails with *"The approvers/assigned to must contain valid users in the organization."*

### Step 4: Branch on the outcome (~12 minutes)
1. Under the approval action, select **+** → **Add an action**, search `condition`, and select **Condition** (Control).
2. Configure the Condition:
   - Left value: insert **Dynamic content → Outcome**
   - Operator: `is equal to`
   - Right value: type `Approve` exactly (capital A, no quotes)

**In the `True` branch (Approved):**
1. Select **+** → **Add an action** → **Move file** (OneDrive for Business):
   - **File to Move:** insert **Dynamic content → Id** (from the trigger)
   - **Destination Folder:** use the picker to select `Invoices/Approved`
   - **If another file is already there:** `Replace`
2. Select **+** → **Add an action** → **Send an email (V2)** (Office 365 Outlook):
   - **To:** your own email (for testing)
   - **Subject:** type `Invoice APPROVED: ` then insert **Dynamic content → File name**
   - **Body:** `The invoice has been approved and moved to the Approved folder for payment processing.`

**In the `False` branch (Rejected):**
1. Select **+** → **Add an action** → **Move file**:
   - **File to Move:** **Dynamic content → Id**
   - **Destination Folder:** `Invoices/Rejected`
   - **If another file is already there:** `Replace`
2. Select **+** → **Add an action** → **Send an email (V2)**:
   - **To:** your own email
   - **Subject:** type `Invoice REJECTED: ` then insert **Dynamic content → File name**
   - **Body:** `The invoice was rejected. Please review and resubmit if necessary.`
3. Select **Save**.

> **⚠️ Warning:** Insert **File name** and **Id** as **single-value** dynamic content. If the designer ever wraps an action in an automatic **"Apply to each"** loop, you accidentally selected an array/list output. Delete the For each, then re-add the plain **Move file** / **Send an email** action and pick the single-value tokens (File name, Id). The Outcome and trigger file fields are all single-value.

> **⚠️ Warning:** If **Send an email** shows **"Unauthorized"**, reconnect the **Office 365 Outlook** connection with a **mailbox-enabled** account. All connections must be green ✓ before the flow can run.

### Step 5: Test both paths (~10 minutes)
1. Top right, select **Test** → **Manually** → **Test**.
2. In OneDrive, **upload a sample PDF** (any file) into `Invoices/Incoming`.
3. The flow triggers and pauses at the approval. Respond in **one** of these ways:
   - Open the **Approvals** hub from the left menu of make.powerautomate.com (or Power Automate), open the request, and choose **Approve**.
   - Or respond from the approval email / Teams card.
4. Confirm the **True** path:
   - The file **moved** from `Incoming` to `Invoices/Approved`.
   - You received the **APPROVED** email.
5. Repeat: upload **another** file, let the flow pause, and this time choose **Reject**. Confirm it moves to `Invoices/Rejected` and you get the **REJECTED** email.

> **Tip:** Approval emails can be slow or land in **Junk**. The most reliable place to respond is the **Approvals hub** in the left menu — it always shows pending requests assigned to you.

### Step 6: Review (~5 minutes)
1. Open **My flows** → **Lab 13 - Invoice Upload Approval** → the latest runs and confirm the correct branch executed each time.
2. Optional enhancement: at the start of the flow, add a row to an `Invoice Register` Excel table with Status `Pending`, then update it after the decision for a full audit trail.

---

## Checkpoint
- ✅ Flow triggered by a **file upload** to `Invoices/Incoming`
- ✅ Approval requested, **assigned to a real tenant user**, and awaited
- ✅ Approved → file in **Approved** folder + approval email
- ✅ Rejected → file in **Rejected** folder + rejection email

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Run fails: "valid users in the organization" | **Assigned to** must be a real tenant user picked from the people-picker dropdown (a person chip) — not a typed external email. |
| Trigger doesn't fire | Confirm the file went into the exact `Invoices/Incoming` folder; allow up to a minute; the file must be **new**. |
| An "Apply to each" wrapped my action | You selected an array output. Delete the For each and re-add the plain action using single-value tokens (**Id**, **File name**, **Outcome**). |
| Move file fails | Use the trigger's **Id** as **File to Move**; make sure the destination folders already exist. |
| Wrong branch runs | The Condition right value must equal exactly `Approve`. |
| "Unauthorized" on Send an email | Reconnect the **Office 365 Outlook** connection with a mailbox-enabled account; connections must be green ✓. |
| No approval email | Respond in the **Approvals hub**; check **Junk**; emails can be slow. |

## Key Takeaways
- A **file-created** trigger turns a simple upload into a full workflow.
- Approvals only run when **Assigned to** is a real tenant user chosen from the dropdown.
- Conditions route the file and notifications by the **Outcome**.
- Moving files between status folders gives a visible, auditable process.

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 14: Purchase Request → Manager Approval → Notification](../Lab%2014%20-%20Purchase%20Request%20Approval/index.md).

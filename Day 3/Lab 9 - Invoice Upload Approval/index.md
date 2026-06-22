# Lab 9: Invoice Upload → Approval Workflow

## Lab Title
End-to-End Workflow: Trigger an Approval When an Invoice File Is Uploaded

## Lab Objectives
By the end of this lab, you will be able to:
1. Use a **file upload** trigger — *When a file is created* in OneDrive/SharePoint
2. Pass file details into an **approval**
3. Branch on the approval outcome
4. Notify finance and **move/update** the file's status accordingly
5. Orchestrate the *Upload → Approve → Act* pattern

## Prerequisites
- Completed Day 1 Lab 3 (approvals + conditions)
- Access to OneDrive (to create folders)

## Scenario
When someone drops an invoice into an **Invoices/Incoming** folder, finance should be asked to **approve or reject** it, and the requester should be notified of the decision. No more invoices sitting unseen in a folder.

---

## Step-by-Step Guide

### Step 1: Prepare the folders (~5 minutes)
1. Go to **OneDrive** (https://www.office.com → OneDrive).
2. Create a folder structure:
   - `Invoices`
     - `Incoming`
     - `Approved`
     - `Rejected`
3. (Optional) Place one sample PDF in `Incoming` later for testing.

### Step 2: Create the automated flow with a file trigger (~10 minutes)
1. **make.powerautomate.com** → **Create** → **Automated cloud flow**.
2. **Name:** `Lab 9 - Invoice Upload Approval`.
3. Trigger: search **When a file is created** → choose **OneDrive for Business → When a file is created**.
4. **Create**, then configure the trigger:
   - **Folder:** browse to `Invoices/Incoming`.

> The trigger fires whenever a new file lands in that folder — that's your *upload* event.

### Step 3: Start the approval (~10 minutes)
1. **+ New step** → **Approvals → Start and wait for an approval**.
2. Configure:
   - **Approval type:** `Approve/Reject - First to respond`
   - **Title:** `Invoice approval needed: ` + dynamic content **File name**
   - **Assigned to:** the finance approver's email (your own for testing)
   - **Details:** `Please review the uploaded invoice: ` + **File name**. (You can also add the **File path**.)

### Step 4: Branch on the outcome (~10 minutes)
1. **+ New step** → **Condition**.
2. Set: dynamic content **Outcome** `is equal to` `Approve`.

**If yes (Approved):**
1. **Add an action → Move file** (OneDrive for Business):
   - **File to move:** dynamic content **Id** (from the trigger)
   - **Destination folder:** `Invoices/Approved`
   - **If another file is already there:** `Replace` or `Copy with a new name`
2. **Add an action → Send an email (V2):**
   - **To:** your email
   - **Subject:** `Invoice APPROVED: ` + **File name**
   - **Body:** `The invoice "{File name}" has been approved and moved to the Approved folder for payment processing.`

**If no (Rejected):**
1. **Add an action → Move file:** destination `Invoices/Rejected`.
2. **Add an action → Send an email (V2):**
   - **Subject:** `Invoice REJECTED: ` + **File name**
   - **Body:** `The invoice "{File name}" was rejected. Please review and resubmit if necessary.`

3. **Save** the flow.

### Step 5: Test both paths (~10 minutes)
1. Select **Test → Manually → Test**.
2. **Upload a sample PDF** into `Invoices/Incoming`.
3. The flow triggers and pauses at the approval. Respond via email or the **Approvals** hub — choose **Approve**.
4. Confirm:
   - The file **moved** to `Invoices/Approved`.
   - You received the **APPROVED** email.
5. Repeat: upload another file and **Reject** it; confirm it moves to `Invoices/Rejected` and you get the **REJECTED** email.

### Step 6: Review (~5 minutes)
1. Check **run history** for both runs and confirm the correct branch executed.
2. Optional enhancement: add a row to an `Invoice Register` Excel table at the start (Status `Pending`) and update the status after the decision for a full audit trail.

---

## Checkpoint
- ✅ Flow triggered by a **file upload** to `Invoices/Incoming`
- ✅ Approval requested and awaited
- ✅ Approved → file in **Approved** + approval email
- ✅ Rejected → file in **Rejected** + rejection email

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Trigger doesn't fire | Confirm the file went into the exact **Incoming** folder; allow up to a minute. |
| Move file fails | Use the trigger's **Id** as the file to move; ensure destination folders exist. |
| Wrong branch runs | The Condition right value must equal exactly `Approve`. |
| No approval email | Respond via the **Approvals** hub; check Junk. |

## Key Takeaways
- A **file-created** trigger turns a simple upload into a workflow.
- Approvals + conditions route the file and notifications by outcome.
- Moving files between status folders gives a visible, auditable process.

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 10: Purchase Request → Manager Approval → Notification](../Lab%2010%20-%20Purchase%20Request%20Approval/index.md).

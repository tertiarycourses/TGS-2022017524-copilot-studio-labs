# Lab 3: Simple Approval Workflow

## Lab Title
Build a Simple Approval Workflow with Power Automate

## Lab Objectives
By the end of this lab, you will be able to:
1. Add a **Start and wait for an approval** action
2. Send an approval request to an approver and wait for the decision
3. Use a **Condition** to branch on Approved vs Rejected
4. Send a different notification email for each outcome
5. Test the full approve / reject paths

## Prerequisites
- Completed [Lab 1](../Lab%201%20-%20Automated%20Email%20Workflow/index.md) and [Lab 2](../Lab%202%20-%20Excel%20Data%20Logging%20Workflow/index.md)
- An email address to act as the **approver** (you can approve your own requests for testing)

## Scenario
A staff member submits a request (e.g. a small purchase). A manager must **approve or reject** it. Based on the decision, the requester is automatically notified. This introduces two essential building blocks: **approvals** and **conditions (branching)**.

---

## Step-by-Step Guide

### Step 1: Create the flow and inputs (~5 minutes)
1. **https://make.powerautomate.com** → **Create** → **Instant cloud flow**.
2. **Flow name:** `Lab 3 - Simple Approval`
3. Trigger: **Manually trigger a flow** → **Create**.
4. Add inputs on the trigger card:
   - **Text:** `RequesterName`
   - **Text:** `RequesterEmail`
   - **Text:** `RequestDetails`

### Step 2: Add the approval action (~10 minutes)
1. Select **+ New step**.
2. Search for **Approvals** and choose **Start and wait for an approval**.
3. If prompted, **Continue** to create the Approvals connection.
4. Configure:
   - **Approval type:** `Approve/Reject - First to respond`
   - **Title:** type `Approval needed: ` then insert dynamic content **RequestDetails**
   - **Assigned to:** your email address (you'll act as the approver for testing)
   - **Details:** type `Requested by ` then insert **RequesterName**. Add more context as you like.

> **Start and wait for an approval** pauses the flow until the approver responds. The approver gets an email and can also respond in the Power Automate / Teams **Approvals** hub.

### Step 3: Add a Condition to branch on the outcome (~10 minutes)
1. Select **+ New step** → search for **Condition** → select **Condition** (Control).
2. Build the condition:
   - **Left box:** dynamic content → **Outcome** (from the approval step).
   - **Operator:** `is equal to`
   - **Right box:** type `Approve`

   > The approval step's **Outcome** output is the text `Approve` or `Reject`.

3. You now have two branches: **If yes** (approved) and **If no** (rejected).

### Step 4: Add a notification email to each branch (~10 minutes)
**In the "If yes" branch:**
1. Select **Add an action** → **Office 365 Outlook → Send an email (V2)**.
2. Configure:
   - **To:** dynamic content **RequesterEmail**
   - **Subject:** `Your request has been APPROVED`
   - **Body:** `Hi ` + **RequesterName** + `, your request "` + **RequestDetails** + `" has been approved. You may proceed.`

**In the "If no" branch:**
1. Select **Add an action** → **Send an email (V2)** again.
2. Configure:
   - **To:** **RequesterEmail**
   - **Subject:** `Your request has been REJECTED`
   - **Body:** `Hi ` + **RequesterName** + `, unfortunately your request "` + **RequestDetails** + `" was not approved. Please contact your manager for details.`

### Step 5: Save and test BOTH paths (~10 minutes)
1. Select **Save**.
2. **Test → Manually → Run flow** with:
   - **RequesterName:** `Siti`
   - **RequesterEmail:** your email
   - **RequestDetails:** `New office chair – $120`
3. The flow will **pause** at the approval step. Check your email (or the **Approvals** hub at make.powerautomate.com → **Approvals**).
4. Select **Approve** and submit. The flow resumes down the **If yes** branch and sends the approval email.
5. Confirm you received the **APPROVED** email.
6. **Run the test again**, this time **Reject** the approval. Confirm you receive the **REJECTED** email and the flow took the **If no** branch.
7. Open the **run history** and confirm the correct branch ran each time.

---

## Checkpoint
- ✅ Flow **Lab 3 - Simple Approval** with approval + condition + two emails
- ✅ Approve path → APPROVED email received
- ✅ Reject path → REJECTED email received

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Flow stuck "running" | That's expected — it's waiting for your approval response. Go to the Approvals hub and respond. |
| Condition always goes to "If no" | The right-hand value must be exactly `Approve` (capital A, matching the **Outcome** text). |
| No approval email | Check Junk; respond via the **Approvals** hub instead. |
| Both branches empty | Make sure you added the email action *inside* each branch, not after the Condition. |

## Key Takeaways
- **Start and wait for an approval** pauses a flow until a human decides.
- **Outcome** (`Approve`/`Reject`) drives a **Condition**.
- **Conditions** create branching logic — different actions for different outcomes.

## Duration
~40 minutes

## Next Steps
You've completed Day 1 and the core Power Automate building blocks. Proceed to [Day 2 — Module 3: Business Agents Concepts](../../Day%202/Module%203%20-%20Business%20Agents%20Concepts.md).

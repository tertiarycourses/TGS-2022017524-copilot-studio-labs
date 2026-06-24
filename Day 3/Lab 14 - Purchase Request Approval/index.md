# Lab 14: Purchase Request → Manager Approval → Notification

## Lab Title
End-to-End Workflow: Agent-Captured Purchase Request with Manager Approval and Notification

## Lab Objectives
By the end of this lab, you will be able to:
1. Combine an **agent** (capture) with an **agent flow** (log + approve + notify) in one process
2. Log a request to Excel as **Pending** with a clean timestamp
3. Use a **Condition** (cost threshold) to decide auto-approve vs manager approval
4. Assign approvals to a **real tenant user** and notify the requester of every outcome
5. Build a complete **Capture → Log → Approve → Notify** business workflow

## Prerequisites
- Completed Day 2 Lab 8 (agent calling a flow) and Day 1 Lab 3 (approvals)
- An Excel `Procurement Log` with table `ProcurementTable` (from Lab 10) — add a `Status` column if missing

## Scenario
At ACME Pte Ltd, staff raise purchase requests through the **Procurement Assistant** agent built in Day 2 Lab 10. In this lab you will extend it so each request is **logged to Excel**, routed by **cost threshold** (small requests auto-approve; larger ones go to a manager), and the requester is **automatically notified** of the result. Everything runs in the **NUS Copilot Sandbox** environment — the full procurement loop, end to end.

---

## Step-by-Step Guide

### Step 1: Reuse the Procurement Assistant agent (~5 minutes)
1. Go to **https://copilotstudio.microsoft.com**, confirm the environment is **NUS Copilot Sandbox**, and open your **Procurement Assistant** agent (from Day 2 Lab 10).
2. Open its **New Procurement Request** topic and confirm it captures these variables: `requester`, `requesterEmail`, `item`, `quantity`, `reason`.
   - If `requesterEmail` is missing, add an **Ask a question** node: `What is your email?` → save the answer to a variable named `requesterEmail`.
   - Add an `estCost` variable: add an **Ask a question** node `What is the estimated total cost (SGD)?`, set the **Identify** type to **Number**, and save to `estCost`.
   - Confirm `quantity` is also a **Number** variable.

> **Tip:** `quantity` and `estCost` must be **Number** variables, not Text. The Condition in Step 4 compares `estCost` to 500 numerically — a Text value can throw a comparison error.

### Step 2: Build the agent flow (~8 minutes)
1. In the topic, after the questions, select **+** → **Add a tool** → **New Agent flow**.
2. The flow opens with a **When an agent calls the flow** trigger. Select it and add these inputs (matching name and type exactly):
   - **Text** `requester`
   - **Text** `requesterEmail`
   - **Text** `item`
   - **Number** `quantity`
   - **Text** `reason`
   - **Number** `estCost`

### Step 3: Log the request as Pending (~7 minutes)
1. Under the trigger, select **+** → **Add an action** → **Add a row into a table** (Excel Online (Business)).
2. Set **Location** `OneDrive for Business`, **Document Library** `OneDrive`, **File** `Procurement Log.xlsx`, **Table** `ProcurementTable`.
3. Map the columns from the flow's inputs (under **Dynamic content**):
   - **Requester:** `requester`
   - **Item:** `item`
   - **Quantity:** `quantity`
   - **Reason:** `reason`
   - **Status:** type `Pending`
   - (If your table has a Cost column, map `estCost`.)
4. For the **Date** column, click the field, open the **fx** (Expression) editor, type exactly `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')`, and select **Add**. The field shows a blue **fx token**.

> **⚠️ Warning:** Enter the date via the **fx** editor so it becomes a token. Typing the expression as plain text stores literal characters in Excel instead of a real timestamp. If Excel later shows `########` in the Date column, the column is simply too narrow — auto-fit it.

### Step 4: Decide the approval path with a Condition (~12 minutes)
A common rule: small requests auto-approve; larger ones need a manager.

1. Under the Excel action, select **+** → **Add an action** → **Condition** (Control):
   - Left value: **Dynamic content → estCost**
   - Operator: `is greater than`
   - Right value: type `500`

**In the `True` branch (needs manager approval):**
1. Select **+** → **Add an action** → **Start and wait for an approval** (Approvals):
   - **Approval type:** `Approve/Reject - First to respond`
   - **Title:** type `Purchase approval: ` then insert **item**, type ` x`, then insert **quantity**
   - **Assigned to:** type your **own name or course email** and **pick the matching person from the people-picker dropdown** so it resolves to a **person chip**.
   - **Details:** `Requested by ` + **requester** + `. Reason: ` + **reason** + `. Est cost: SGD ` + **estCost** + `.`
2. Under the approval, add a **nested Condition**:
   - Left value: **Dynamic content → Outcome**
   - Operator: `is equal to`
   - Right value: type `Approve`
   - **Nested `True`:** add **Send an email (V2)** → **To:** **requesterEmail**, **Subject:** `Purchase APPROVED: ` + **item**, **Body:** confirm the request is approved.
   - **Nested `False`:** add **Send an email (V2)** → **To:** **requesterEmail**, **Subject:** `Purchase REJECTED: ` + **item**, **Body:** explain the request was rejected.

**In the `False` branch (auto-approved, ≤ 500):**
1. Select **+** → **Add an action** → **Send an email (V2)** → **To:** **requesterEmail**, **Subject:** `Purchase AUTO-APPROVED: ` + **item**, **Body:** confirm the request is approved automatically.

> **⚠️ Warning:** The **Assigned to** approver MUST be a real user in **this** tenant — pick from the people-picker dropdown so it becomes a **person chip**. A typed external email makes the run fail with *"valid users in the organization."*

> **⚠️ Warning:** Insert **requesterEmail**, **item**, **Outcome** etc. as **single-value** dynamic content. If the designer wraps a Send an email in an **"Apply to each"** loop, you picked a list/array output — delete the For each and re-add the plain action using the single-value tokens (Outcome and the trigger inputs are all single-value).

> **Tip on status updates:** to flip the row to Approved/Rejected later, use Excel **Update a row** with a **key column** (e.g. add an `ID` column set to a unique value when the row is created, then update by that key). Status updates are optional for this lab — focus on the approve + notify flow.

### Step 5: Return a result and wire inputs (~10 minutes)
1. Under the branches, select **+** → **Add an action** → **Respond to the agent**. Add a **Text** output named `result` with value `Your request has been submitted for processing.`
2. Select **Save**, then **Publish** the flow, then **Go back to agent**.
3. In the topic's tool node, map every flow input to the matching agent variable: `requester`, `requesterEmail`, `item`, `quantity`, `reason`, `estCost`.
4. After the tool node, add a **Send a message** node showing `{result}` so the user sees the confirmation.
5. Select **Save** on the topic, then **Publish** the agent.

> **⚠️ Warning:** If **Send an email** returns **"Unauthorized"**, reconnect the **Office 365 Outlook** connection with a **mailbox-enabled** account. All connections must show a green ✓ before the flow can run.

### Step 6: Test all paths (~8 minutes)
1. Open the **Test** pane in Copilot Studio. Run a request **under** the threshold:
   - item `Notebook`, quantity `5`, reason `Stationery`, estCost `120`
   - Expect: a `Pending` row logged, an **AUTO-APPROVED** email, and the confirmation message in chat.
2. Run a request **over** the threshold and **approve** it:
   - item `Laptop`, quantity `2`, reason `New hires`, estCost `3000`
   - Respond in the **Approvals hub** (left menu) → **Approve**. Expect an **APPROVED** email.
3. Run another over-threshold request and **Reject** it → expect a **REJECTED** email.
4. Open **My flows → run history** and the **Procurement Log** to confirm each path behaved correctly.

> **Tip:** Approval emails can be slow or land in **Junk**. The **Approvals hub** in the left menu is the reliable place to approve or reject pending requests.

---

## Checkpoint
- ✅ Agent captures the request and calls the flow with all inputs mapped
- ✅ Request logged to Excel as **Pending** with a clean timestamp
- ✅ Threshold Condition routes **auto-approve** vs **manager approval**
- ✅ Approvals assigned to a **real tenant user**; requester notified of every outcome

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Run fails: "valid users in the organization" | **Assigned to** must be a real tenant user picked from the people-picker dropdown (a person chip) — not a typed external email. |
| Condition errors on estCost | Ensure `estCost` (and `quantity`) are **Number** variables/inputs and you enter digits only. |
| An "Apply to each" wrapped my email action | You picked a list/array output. Delete the For each and re-add the plain action using single-value tokens (**Outcome**, **requesterEmail**, etc.). |
| "Unauthorized" on Send an email | Reconnect the **Office 365 Outlook** connection with a mailbox-enabled account; connections must be green ✓. |
| Date shows raw text / `########` | Re-enter the date via the **fx** editor so it is a token; widen the Excel column to fix `########`. |
| Approval never resumes | Respond in the **Approvals hub**; check **Junk**; emails can be slow. |
| Inputs empty in the flow | Re-map each agent variable to the matching flow input in the tool node. |

## Key Takeaways
- This is the full loop: **capture (agent) → log → approve → notify**.
- Approvals only run when **Assigned to** is a real tenant user picked from the dropdown.
- **Conditions** implement real business rules such as value thresholds.
- Keep single-value tokens out of accidental For each loops, and use the **fx** editor for dates.

## Duration
~50 minutes

## Next Steps
Proceed to [Lab 15: Order Processing Workflow](../Lab%2015%20-%20Order%20Processing%20Workflow/index.md).

# Lab 10: Purchase Request → Manager Approval → Notification

## Lab Title
End-to-End Workflow: Agent-Captured Purchase Request with Manager Approval and Notification

## Lab Objectives
By the end of this lab, you will be able to:
1. Combine an **agent** (capture) with a **flow** (approve + notify) in one process
2. Log the request, then route it for **manager approval**
3. Use a **condition** (e.g. value threshold) to decide the approval path
4. **Update the record status** and **notify** the requester of the decision
5. Build a complete *Request → Approve → Notify* business workflow

## Prerequisites
- Completed Day 2 Lab 6 (agent calling a flow) and Day 1 Lab 3 (approvals)
- An Excel `Procurement Log` with table `ProcurementTable` (from Lab 6) — add a `Status` column if missing

## Scenario
Staff raise purchase requests through the **Procurement Assistant** agent. Each request is **logged**, sent to a **manager for approval**, and the requester is **automatically notified** of the result — the full procurement loop end to end.

---

## Step-by-Step Guide

### Step 1: Reuse the Procurement Assistant agent (~5 minutes)
1. Open your **Procurement Assistant** (Lab 6) and its **New Procurement Request** topic.
2. Confirm it captures: `requester`, `requesterEmail`, `item`, `quantity`, `reason`.
   - If `requesterEmail` is missing, add an **Ask a question** node: `What is your email?` → save as `requesterEmail`.
   - (Optional) Add `estCost` (Number): `What is the estimated total cost (SGD)?` → save as `estCost`. We'll use it for the approval threshold.

### Step 2: Build the approval flow (~10 minutes)
1. In the topic, after the questions, **+** → **Add a tool** → **New Agent flow**.
2. Trigger **When an agent calls the flow**. Add inputs:
   - **Text** `requester`, **Text** `requesterEmail`, **Text** `item`, **Number** `quantity`, **Text** `reason`, **Number** `estCost`.

### Step 3: Log the request as Pending (~5 minutes)
1. **+ New step** → **Excel → Add a row into a table** (`Procurement Log` / `ProcurementTable`).
2. Map: Date `utcNow()`, Requester **requester**, Item **item**, Quantity **quantity**, Reason **reason**, Status `Pending`.
   - (If your table has a Cost column, map **estCost**.)

### Step 4: Decide the approval path with a condition (~10 minutes)
A common rule: small requests auto-approve; larger ones need a manager.

1. **+ New step** → **Condition**: dynamic content **estCost** `is greater than` `500`.

**If yes (needs manager approval):**
1. **Add an action → Approvals → Start and wait for an approval**:
   - Type `Approve/Reject - First to respond`
   - **Title:** `Purchase approval: ` + **item** + ` x` + **quantity**
   - **Assigned to:** the manager's email (your own for testing)
   - **Details:** `Requested by {requester}. Reason: {reason}. Est cost: SGD {estCost}.`
2. **Add → Condition** (nested): **Outcome** `is equal to` `Approve`.
   - **If yes:** Send an email to **requesterEmail**, Subject `Purchase APPROVED: {item}`, Body confirming approval.
   - **If no:** Send an email to **requesterEmail**, Subject `Purchase REJECTED: {item}`, Body explaining rejection.

**If no (auto-approved, ≤ 500):**
1. **Add an action → Send an email (V2)** to **requesterEmail**: Subject `Purchase AUTO-APPROVED: {item}`, Body confirming the request is approved automatically.

> **Tip on updating status:** to mark the row Approved/Rejected, use **Update a row** (Excel) with a **key column** (e.g. add an `ID` column populated with a unique value such as `utcNow()` when you create the row, then update by that key). For this lab, status updates are optional — focus on the approval + notification flow.

### Step 5: Return a result and wire inputs (~10 minutes)
1. **+ New step** → **Respond to the agent** with **Text** output `result` = `Your request has been submitted for processing.`
2. **Save / Publish** the flow → **Go back to agent**.
3. In the topic, map all flow inputs to the matching variables (`requester`, `requesterEmail`, `item`, `quantity`, `reason`, `estCost`).
4. After the tool node, **Send a message:** `{result}` so the user sees confirmation.
5. **Save** the topic.

### Step 6: Test all paths (~10 minutes)
1. Open the **Test** pane. Run a request **under the threshold**:
   - item `Notebook`, quantity `5`, reason `Stationery`, estCost `120`
   - Expect: row logged, **AUTO-APPROVED** email, confirmation in chat.
2. Run a request **over the threshold** and **approve** it:
   - item `Laptop`, quantity `2`, reason `New hires`, estCost `3000`
   - Expect: row logged, approval requested, after you approve → **APPROVED** email.
3. Run another over-threshold request and **reject** it → **REJECTED** email.
4. Check the **run history** and the **Procurement Log** to confirm each path behaved correctly.

---

## Checkpoint
- ✅ Agent captures the request and calls the flow
- ✅ Request logged to Excel as **Pending**
- ✅ Threshold condition routes auto-approve vs manager approval
- ✅ Requester notified of every outcome (auto-approved / approved / rejected)

## Troubleshooting
| Problem | Solution |
|---------|----------|
| Condition errors on estCost | Ensure `estCost` is a **Number** input and you enter digits. |
| Approval never resumes | Respond via the **Approvals** hub; check Junk. |
| Wrong notification | Verify the nested Condition compares **Outcome** to exactly `Approve`. |
| Inputs empty in flow | Re-map each agent variable to the matching flow input. |

## Key Takeaways
- This is the full loop: **capture (agent) → log → approve → notify**.
- **Conditions** implement real business rules (value thresholds).
- Every outcome ends with a clear notification and (optionally) a status update.

## Duration
~50 minutes

## Next Steps
Proceed to the [Lab 11: Capstone Workshop](../Lab%2011%20-%20Capstone%20Workshop/index.md) to build your own end-to-end workflow.

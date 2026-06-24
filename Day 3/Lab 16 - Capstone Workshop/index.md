# Lab 16: Capstone Workshop — Build Your Own End-to-End Workflow

## Lab Title
Business Workflow Workshop: Design and Build a Complete Automation

## Lab Objectives
By the end of this workshop, you will be able to:
1. **Design** an end-to-end workflow for a real business scenario on paper before you build
2. **Build** it by combining a Copilot Studio agent with one or more Power Automate flows
3. **Orchestrate** triggers, actions, conditions, approvals, and notifications into one working process
4. **Test** the happy path and every branch using a structured test log
5. **Present** your workflow and explain its business value

## Prerequisites
- Completed all Day 1–3 labs (you will reuse skills from across the whole course)
- Your environment **NUS Copilot Sandbox** set up, with working Outlook and Excel connections (all green ✓)

> **Tip:** This is the last-afternoon capstone. You are not learning a new technique here — you are combining the pieces you already practised into one workflow that is **yours**. Pick a scenario you genuinely care about and the rest gets easier.

## Scenario
You work for **ACME Pte Ltd**. Choose **one** real business process from your day-to-day work (or one of the four tracks below), then design and build a complete automation for it: something **triggers** it, data is **captured** and **logged**, a **business rule** decides what happens, the right people are **notified**, and the process ends in a clear **final state**.

You will work **individually or in a small group** and finish with a **working, tested workflow** plus a short **demo**.

---

## Step-by-Step Guide

### Step 1: Choose a track (~10 min)

Pick **one** scenario below (or adapt one to your own job). Each maps directly to skills you have already practised.

#### Track A — Sales
**Lead-to-CRM workflow.** A customer submits an enquiry (via the **Sales Enquiry Assistant** or an email). The workflow logs the lead, generates a personalised acknowledgement with an **AI prompt**, and notifies the assigned salesperson. High-value leads (quantity or deal size over a threshold) also raise a manager alert.

#### Track B — Finance
**Expense / invoice approval workflow.** An expense or invoice is submitted (agent form or file upload). It is logged, routed for **approval** based on amount, and the requester is notified. Approved items move to a "to-pay" status; rejected items are returned with a reason.

#### Track C — Procurement
**Purchase-request workflow.** Staff raise a purchase request via an agent. It is logged, routed for **manager approval** when it exceeds a cost threshold, and the requester is notified. The procurement team gets a consolidated notification for approved items.

#### Track D — Order Processing
**Order intake workflow.** A customer places an order (an agent captures product, quantity, address). The order is logged, an order-confirmation email is generated with an **AI prompt**, large orders trigger a **restock alert** to the warehouse, and the customer is notified of the order status.

### Step 2: Design on paper first (~20 min)

Use the orchestration method from [Module 4](../Module%204%20-%20End-to-End%20Orchestration%20Concepts.md). Complete this **design sheet** *before* you build anything — a clear plan makes the build fast and the testing obvious.

| Design item | Your answer |
|-------------|-------------|
| **One-sentence summary** ("When ___, do ___, then ___, finally ___") | |
| **Trigger** (email / form / file upload / agent call / schedule) | |
| **Data to capture** (the fields / variables, and their types) | |
| **Actions in order** (log, generate, approve, notify…) | |
| **Decision point(s)** (the condition and the two paths) | |
| **End states** (final status + who is notified for each outcome) | |
| **Tools used** (agent? which flows? Excel? Outlook? Approvals?) | |

> **⚠️ Warning:** Get this design sheet checked by a facilitator or peer **before** building. Fixing a plan on paper takes a minute; fixing a half-built flow takes much longer.

### Step 3: Build it incrementally (~60–90 min)

Build **one piece at a time and test after each piece** — never build everything and test once at the end.

**Suggested build order:**
1. **Data store** — create the Excel log as a named **Table** (include any status / key columns your end states need).
2. **Capture** — build the agent topic (**Ask a question** nodes → variables) *or* configure the automated trigger (email / file). Remember to set numeric fields to **Number**.
3. **Log** — add **Add a row into a table**; test that one record is written correctly. Use the **fx** editor for any timestamp: `formatDateTime(utcNow(),'yyyy-MM-dd HH:mm')` (enter it via **fx**, never type the expression into the field).
4. **Generate** (if used) — add an **AI prompt** action; test that the generated text reads well.
5. **Decide** — add **Condition(s)** for your business rule; test **both** branches (just above and just below the threshold).
6. **Approve** (if used) — add **Start and wait for an approval**; test **approve** and **reject**.
7. **Notify** — add **Send an email** actions for each outcome; test that each one is delivered.
8. **Connect** — if using an agent, add **When an agent calls the flow** as the trigger and **Respond to the agent** at the end, then wire the agent variables → flow inputs and show the returned confirmation message.

> **⚠️ Warning — green connections:** Before testing any **Send an email** or Excel action, confirm every connection shows a green check mark ✓. An **Unauthorized** error on Send an email means the Outlook connection is the wrong account — reconnect with a real **mailbox-enabled** tenant account.

> **⚠️ Warning — approvals:** In **Start and wait for an approval**, set **Assigned to** by **picking a real tenant user from the dropdown**. Do not type an external email address — external approvers will never receive the request and the flow will appear to hang.

> **Tip:** If an action gets wrapped in an automatic **For each** loop, you picked a multi-value field. Most of your fields are single values — remove the action and re-add the dynamic content carefully.

**Reuse your earlier labs as templates:**
- Email sending → Lab 1
- Excel logging → Lab 2
- Approval + condition → Lab 3
- Scheduled / recurring trigger → Lab 4
- Form submission trigger → Lab 5
- Agent fundamentals & instructions → Lab 6
- Knowledge / RAG grounding → Lab 7
- Tools & actions → Lab 8
- Agent capture (structured data) → Lab 9
- Agent → flow integration → Lab 10
- AI-generated response → Lab 11
- Email/file trigger end-to-end → Labs 12–13
- Full approval loop → Lab 14
- Agent-driven order processing → Lab 15

### Step 4: Test thoroughly (~20 min)

Complete this **test log**. Your workflow is not done until every relevant row passes. (Skip the approval rows only if your track has no approval step.)

| Test case | Expected result | Pass? |
|-----------|-----------------|-------|
| Happy path (typical input) | Logged + notified + correct end state | |
| Approval → Approved | Approved branch runs + correct email sent | |
| Approval → Rejected | Rejected branch runs + correct email sent | |
| Threshold / edge case (just above & just below) | Correct branch chosen each time | |
| Bad / missing input | Agent re-asks; flow does not crash | |
| Run history | Every step green; logged data correct | |

> **Tip:** Open the flow's **Run history** (Power Automate → your flow → 28-day run history) to see exactly which step failed and read the error. Green = success, red = failure.

### Step 5: Present your workflow (~5 min each)

Demo to the group. Cover:
1. **The business problem** and who it helps.
2. **The trigger and the steps** — walk through your one-sentence design summary.
3. **A live run** of the happy path *and* at least one branch.
4. **The business value** — time saved, errors avoided, consistency gained.
5. **What you would add next** with more time.

---

## Assessment checklist

Your capstone is complete when:
- ✅ It has a clear **trigger** and runs end to end
- ✅ It **captures or receives** data and **logs** it to an Excel **Table**
- ✅ It includes at least one **Condition** (branching on a business rule)
- ✅ It includes an **approval** *or* an **AI-generated** response
- ✅ It **notifies** the right people for **every** outcome
- ✅ Every relevant test case in Step 4 **passes**
- ✅ All connections are green ✓ and any approver is a **real tenant user**
- ✅ You can **explain** its business value in plain language

---

## Stretch goals (optional)
- Add a **scheduled** flow that emails a daily summary of new records.
- Use **Update a row** to keep the Excel **Status** column current at each stage (e.g. `Received` → `Approved` → `Completed`).
- Deploy the agent to **Microsoft Teams** so colleagues can use it where they already work.
- Add a **second approver** or an **escalation** if no response within a time limit.
- Post outcomes to a **Teams channel** instead of (or as well as) email.

---

## Duration
~2–3 hours

## Congratulations 🎉
You have completed the **Microsoft Copilot Studio & Power Automate for Business Workflow Automation** course. You can now design and build end-to-end automations that capture requests, apply business rules, route approvals, and notify stakeholders — across **Sales, Finance, Procurement, and Order Processing**.

**Where to go next:**
- Explore the [Power Automate Templates Gallery](https://make.powerautomate.com/templates/) for ready-made patterns.
- Review [Copilot Studio documentation](https://learn.microsoft.com/microsoft-copilot-studio/) for advanced agent features.
- Identify one manual process at your workplace and automate it this week.

# Lab 11: Capstone Workshop — Build Your Own End-to-End Workflow

## Lab Title
Business Workflow Workshop: Design and Build a Complete Automation

## Lab Objectives
By the end of this workshop, you will be able to:
1. **Design** an end-to-end workflow for a real business scenario
2. **Build** it by combining a Copilot Studio agent with Power Automate flows
3. **Orchestrate** triggers, actions, conditions, approvals, and notifications
4. **Test** the happy path and every branch
5. **Present** your workflow and explain its business value

## Prerequisites
- Completed all Day 1–3 labs (you'll reuse every skill)
- Your environment set up (Lab 0)

## Format
- **Duration:** ~2–3 hours
- **Work:** individually or in small groups
- **Deliverable:** a working, tested workflow + a 5-minute demo

---

## Step 1: Choose a track (~10 minutes)

Pick **one** scenario (or adapt one to your own job). Each maps directly to skills you've practiced.

### Track A — Sales
**Lead-to-CRM workflow.** A customer submits an enquiry (via the **Sales Enquiry Assistant** or an email). The workflow logs the lead, generates a personalized acknowledgement (AI prompt), and notifies the assigned salesperson. High-value leads (quantity over a threshold) also raise a manager alert.

### Track B — Finance
**Expense/invoice approval workflow.** An expense or invoice is submitted (agent form or file upload). It is logged, routed for approval based on amount, and the requester is notified. Approved items move to a "to-pay" folder/status; rejected items are returned with a reason.

### Track C — Procurement
**Purchase-request workflow.** Staff raise a request via an agent. It is logged, routed for manager approval over a cost threshold, and the requester is notified. The procurement team gets a consolidated notification for approved items.

### Track D — Order Processing
**Order intake workflow.** A customer places an order (agent captures product, quantity, address). The order is logged, an order-confirmation email is generated (AI prompt), stock-low orders trigger a restock alert to the warehouse, and the customer is notified of the order status.

---

## Step 2: Design on paper first (~20 minutes)

Use the method from [Module 4](../Module%204%20-%20End-to-End%20Orchestration%20Concepts.md). Complete this design sheet **before** building:

| Design item | Your answer |
|-------------|-------------|
| **One-sentence summary** ("When ___, do ___, then ___, finally ___") | |
| **Trigger** (email / form / file upload / agent call / schedule) | |
| **Data to capture** (the fields / variables) | |
| **Actions in order** (log, generate, approve, notify…) | |
| **Decision point(s)** (the condition and the two paths) | |
| **End states** (final status + who is notified for each outcome) | |
| **Tools used** (agent? which flows? Excel? Outlook? Approvals?) | |

> Get this design checked by a facilitator or peer before building — fixing a plan is cheaper than fixing a flow.

---

## Step 3: Build it (~60–90 minutes)

Build incrementally and test after each piece — don't build everything then test once.

**Suggested build order:**
1. **Data store** — create the Excel log with a **Table** (and any status/key columns).
2. **Capture** — build the agent topic (question nodes → variables) *or* configure the automated trigger (email/file).
3. **Log** — add the *Add a row into a table* action; test that a record is written.
4. **Generate** (if used) — add an **AI prompt** action; test the generated text.
5. **Decide** — add **Condition(s)** for your business rule; test both branches.
6. **Approve** (if used) — add **Start and wait for an approval**; test approve and reject.
7. **Notify** — add **Send an email** actions for each outcome; test delivery.
8. **Connect** — if using an agent, wire variables → flow inputs and show the returned confirmation.

**Reuse your earlier labs as templates:**
- Email sending → Lab 1
- Excel logging → Lab 2
- Approval + condition → Lab 3
- Agent capture → Lab 5
- Agent → flow integration → Lab 6
- AI-generated response → Lab 7
- Email/file trigger end-to-end → Labs 8–9
- Full approval loop → Lab 10

---

## Step 4: Test thoroughly (~20 minutes)

Complete this test log. Your workflow isn't done until every row passes.

| Test case | Expected result | Pass? |
|-----------|-----------------|-------|
| Happy path (typical input) | Logged + notified + correct end state | |
| Approval → Approved | Approved branch + correct email | |
| Approval → Rejected | Rejected branch + correct email | |
| Threshold/edge case (just above & below) | Correct branch chosen | |
| Bad/missing input | Agent re-asks; flow doesn't crash | |
| Run history | All steps green; data correct | |

---

## Step 5: Present your workflow (~5 minutes each)

Demo to the group. Cover:
1. **The business problem** and who it helps.
2. **The trigger and the steps** (walk the design sentence).
3. **A live run** of the happy path and one branch.
4. **The business value** — time saved, errors avoided, consistency gained.
5. **What you'd add next** with more time.

---

## Assessment checklist

Your capstone is complete when:
- ✅ It has a clear **trigger** and runs end to end
- ✅ It **captures or receives** data and **logs** it to Excel
- ✅ It includes at least one **condition** (branching)
- ✅ It includes an **approval** *or* an **AI-generated** response
- ✅ It **notifies** the right people for every outcome
- ✅ Every test case in Step 4 **passes**
- ✅ You can **explain** its business value

---

## Stretch goals (optional)
- Add a **scheduled** flow that emails a daily summary of new records.
- Use **Update a row** to keep the Excel **Status** current at each stage.
- Deploy the agent to **Microsoft Teams** so colleagues can use it.
- Add a **second approver** or an **escalation** if no response within a time limit.
- Post outcomes to a **Teams channel** instead of (or as well as) email.

---

## Duration
~2–3 hours

## Congratulations 🎉
You've completed the **Microsoft Copilot Studio & Power Automate for Business Workflow Automation** course. You can now design and build end-to-end automations that capture requests, apply business rules, route approvals, and notify stakeholders — across Sales, Finance, Procurement, and Order Processing.

**Where to go next:**
- Explore the [Power Automate Templates Gallery](https://make.powerautomate.com/templates/) for ready-made patterns.
- Review [Copilot Studio documentation](https://learn.microsoft.com/microsoft-copilot-studio/) for advanced agent features.
- Identify one manual process at your workplace and automate it this week.

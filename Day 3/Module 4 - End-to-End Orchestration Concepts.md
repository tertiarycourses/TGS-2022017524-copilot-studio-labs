# Module 4: End-to-End Workflow Automation

> **Read this before the Day 3 labs.** ~15 minutes.

You now have both halves of an automated business process. Today you join them into complete, end-to-end workflows — and learn the design discipline that keeps them reliable.

---

## 1. Agents + Power Automate = end-to-end automation

By now you've built both halves:

- **Power Automate flows** (Day 1) — the *doing*: send email, log to Excel, run approvals.
- **Copilot Studio agents** (Day 2) — the *understanding*: capture requests as structured data and call flows.

**End-to-end automation** chains these into a complete business process where a **single trigger flows all the way through to a finished outcome** — with little or no manual work in between:

```
 CAPTURE  →  RECORD  →  DECIDE  →  NOTIFY  →  CLOSE
 (agent/    (Excel    (approval  (email/    (final
  email/     log)      or rule)   Teams)     status)
  form)
```

One event goes in the top; a finished, recorded, communicated result comes out the bottom.

---

## 2. Workflow orchestration

**Orchestration** is arranging multiple steps — and sometimes multiple flows and agents — so they run in the right order, pass data correctly, and handle every outcome.

A well-orchestrated workflow has five qualities:

1. **A clear trigger** — one starting event (email arrives, file uploaded, agent finishes capturing).
2. **Sequenced actions** — each step's **output** feeds the next step's **input**.
3. **Branching** — conditions route the process (approved vs rejected, high value vs low value).
4. **Notifications** — the right people are told at the right moments.
5. **A definite end state** — the record is updated to its final status (Logged / Approved / Rejected / Completed).

> **No dead ends.** Orchestration is mostly about making sure *every* path — including the unhappy ones — leads somewhere defined. A rejected request still needs an owner, a notification, and a final status.

### Common orchestration patterns

You'll build one of each this morning. Notice how they grow in complexity:

| Pattern | Shape | What's new | Day 3 lab |
|---------|-------|------------|-----------|
| **Capture → Log → Notify** | Linear: record it, tell someone | Pure sequence, no branch | Lab 12 |
| **Upload → Approve → Act** | File trigger, then human decision | Adds an approval + branch | Lab 13 |
| **Request → Approve → Notify** | Multi-party approval chain | Adds routing by who/what | Lab 14 |

> **Approver reminder (from Day 1):** the approver in any approval step must be a real **user in your tenant**, not an outside email address. Pick a colleague — or yourself — for testing.

---

## 3. Managing workflow outputs and next steps

Every step produces **outputs**. Managing them well is what separates a demo from a dependable workflow:

- **Pass data forward** with dynamic content — sender's email → notification; captured quantity → approval title. (Use the **fx** expression editor for any small formatting, like a date or a trimmed string.)
- **Use a Status column** as the source of truth: `New → Pending → Approved/Rejected → Done`. Update it at each stage so anyone can see where a request stands at a glance.
- **Decide the next step for every outcome.** Never leave a branch empty — an approved request and a rejected request *both* need a defined follow-up.
- **Notify deliberately.** Tell the requester the result; tell the team when action is needed. Avoid noisy, redundant emails.
- **Make it traceable.** The Excel log **plus** the Power Automate **run history** together give you a complete audit trail.

### Designing a workflow — a simple method

Use this every time *before* you start clicking in the designer:

1. **Write the sentence:** *"When ___ happens, do ___, then ___, and finally ___."*
2. **Identify the trigger** (the "when").
3. **List the actions** in order (the "do / then / finally").
4. **Mark the decision points** (where it branches).
5. **Define each end state** (final status + who is notified).
6. **Build, test the happy path, then test every branch.**

> **Sentence first, build second.** If you can't say the workflow in one plain sentence, you're not ready to build it yet. The sentence reveals your trigger, your steps, and your end states before you touch the tool.

You'll apply exactly this method in **Lab 16 (Capstone Workshop)**.

---

## 4. What you'll build on Day 3

- **Lab 12:** Email enquiry → log to Excel → notify the team (Capture → Log → Notify).
- **Lab 13:** Invoice file uploaded → approval workflow (Upload → Approve → Act).
- **Lab 14:** Purchase request → manager approval → notification (Request → Approve → Notify).
- **Lab 15:** Order Processing — an agent captures an order, then the flow confirms, logs, and raises a restock alert.
- **Lab 16:** Capstone — design and build your **own** end-to-end workflow for Sales, Finance, Procurement, or Order Processing.

Labs 12–14 drill the three core patterns; Lab 15 brings the agent back into the loop; Lab 16 is where you put it all together yourself.

---

**Next:** [Lab 12: Email Enquiry → Excel Logging → Notification](Lab%2012%20-%20Email%20to%20Excel%20to%20Notification/index.md)

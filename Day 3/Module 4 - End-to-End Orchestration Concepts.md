# Module 4: End-to-End Workflow Automation

> **Read this before the Day 3 labs.** ~15 minutes.

## 1. Agents + Power Automate = end-to-end automation

By now you've built both halves:

- **Power Automate flows** (Day 1) — the *doing*: send email, log to Excel, run approvals.
- **Copilot Studio agents** (Day 2) — the *understanding*: capture requests as structured data and call flows.

**End-to-end automation** chains these into a complete business process where a single trigger flows all the way through to a finished outcome — capture → record → decide → notify → close — with little or no manual work.

## 2. Workflow orchestration

**Orchestration** is arranging multiple steps (and sometimes multiple flows/agents) so they run in the right order, pass data correctly, and handle each outcome.

A well-orchestrated workflow has:

1. **A clear trigger** — one starting event (email arrives, file uploaded, agent finishes capturing).
2. **Sequenced actions** — each step's **output** feeds the next step's **input**.
3. **Branching** — conditions route the process (approved vs rejected, high value vs low value).
4. **Notifications** — the right people are told at the right moments.
5. **A definite end state** — the record is updated to its final status (Logged / Approved / Rejected / Completed).

### Common orchestration patterns

| Pattern | Shape | Day 3 lab |
|---------|-------|-----------|
| **Capture → Log → Notify** | Linear: record it, tell someone | Lab 8 |
| **Upload → Approve → Act** | File trigger then human decision | Lab 9 |
| **Request → Approve → Notify** | Multi-party approval chain | Lab 10 |

## 3. Managing workflow outputs and next steps

Every step produces **outputs**. Managing them well is what makes a workflow reliable:

- **Pass data forward** with dynamic content (sender's email → notification; captured quantity → approval title).
- **Use a Status column** as the source of truth (`New → Pending → Approved/Rejected → Done`). Update it at each stage so anyone can see where a request stands.
- **Decide the next step for every outcome.** Never leave a branch empty — an approved request and a rejected request both need a defined follow-up.
- **Notify deliberately.** Tell the requester the result; tell the team when action is needed. Avoid noisy, redundant emails.
- **Make it traceable.** The Excel log + Power Automate **run history** together give you an audit trail.

### Designing a workflow — a simple method

1. **Write the sentence:** *"When ___ happens, do ___, then ___, and finally ___."*
2. **Identify the trigger** (the "when").
3. **List the actions** in order (the "do / then / finally").
4. **Mark the decision points** (where it branches).
5. **Define each end state** (final status + who is notified).
6. **Build, test the happy path, then test every branch.**

You'll apply exactly this method in **Lab 11 (Capstone Workshop)**.

## 4. What you'll build on Day 3

- **Lab 8:** Email enquiry → log to Excel → notify the team (Capture → Log → Notify).
- **Lab 9:** Invoice file uploaded → approval workflow (Upload → Approve → Act).
- **Lab 10:** Purchase request → manager approval → notification (Request → Approve → Notify).
- **Lab 11:** Design and build your **own** end-to-end workflow for Sales, Finance, Procurement, or Order Processing.

---

**Next:** [Lab 8: Email Enquiry → Excel Logging → Notification](Lab%208%20-%20Email%20to%20Excel%20to%20Notification/index.md)

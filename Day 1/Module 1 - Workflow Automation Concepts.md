# Module 1: Introduction to Workflow Automation

> **Read this before the Day 1 labs.** It explains the "why" behind everything you'll build. ~20 minutes.

## 1. What is business workflow automation?

A **business workflow** is a repeatable series of steps that gets work done — for example:

> *A customer emails an enquiry → someone records it in a spreadsheet → a salesperson is notified → they reply.*

**Automation** means letting software perform those steps for you, consistently and instantly, instead of doing them by hand. Good candidates for automation are tasks that are:

- **Repetitive** — done the same way many times (logging enquiries, sending confirmations)
- **Rule-based** — clear "if this, then that" logic (if amount > $1,000, get approval)
- **Time-consuming** — manual copying, chasing approvals, re-typing data

**Benefits:** fewer mistakes, faster turnaround, nothing falls through the cracks, and staff focus on higher-value work.

In this course you automate workflows with two Microsoft tools:

- **Power Automate** — builds the automated steps (the "flows").
- **Copilot Studio** — builds AI **agents** that understand natural-language requests and feed clean, structured data into those flows.

## 2. Standalone agents vs integrated workflows

| | **Standalone agent** | **Integrated workflow** |
|---|---|---|
| What it does | Chats and answers questions | Performs real actions across systems |
| Example | "What's your return policy?" | Logs the enquiry, emails the team, files a ticket |
| Powered by | Copilot Studio alone | Copilot Studio **+** Power Automate |
| Outcome | Information | Action + record + notification |

A **standalone agent** is helpful but only *talks*. An **integrated workflow** connects the agent to Power Automate so the conversation actually *triggers work* — saving a record, sending an email, starting an approval. That integration is the heart of this course.

## 3. Workflow logic: the four building blocks

Every workflow you build is made of these four parts. Learn these terms now — you'll use them in every lab.

### Trigger — *what starts the workflow*
The event that kicks everything off. Examples:
- An **email is received**
- A **file is uploaded** to a folder
- A **form is submitted**
- A **schedule** is reached (e.g. every morning at 9 am)
- An **agent** calls the flow

> A flow does nothing until its trigger fires. Every flow has exactly one trigger.

### Actions — *what the workflow does*
The steps that run after the trigger, in order. Examples:
- **Send an email**
- **Add a row** to an Excel table
- **Start an approval** and wait for a decision
- **Post a message** to Teams
- **Create or update** a record

### Outputs — *the data the workflow produces or passes along*
The pieces of information that move between steps. Examples:
- The **sender's email address** from a received email
- The **customer name and product** captured by an agent
- The **approval result** ("Approved" / "Rejected")

Outputs from one step become inputs to the next — this is called **dynamic content**.

### Steps — *the ordered sequence as a whole*
Trigger + actions arranged top-to-bottom make up the **steps** of the workflow. Steps can also include **conditions** (branching: if/else) and **loops** (repeat for each item).

### Putting it together

```
TRIGGER            ACTIONS (steps)                       OUTPUTS
─────────          ──────────────────────────           ──────────
Email received  →  1. Read sender + subject          →  sender, subject
                   2. Add a row to Excel             →  logged record
                   3. Send notification to sales     →  confirmation
```

## 4. How the days fit together

- **Day 1 (this day):** Build flows in **Power Automate** — email, Excel logging, approvals. You'll master triggers, actions, and outputs.
- **Day 2:** Build **agents** in Copilot Studio that capture requests as structured data and connect to flows.
- **Day 3:** Combine agents + flows into complete **end-to-end** business workflows, then build your own in the workshop.

---

**Next:** [Lab 1: Automated Email Workflow](Lab%201%20-%20Automated%20Email%20Workflow/index.md)

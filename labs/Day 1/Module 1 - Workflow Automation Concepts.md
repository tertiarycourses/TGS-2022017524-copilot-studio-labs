# Module 1: Introduction to Workflow Automation

> **Read this before the Day 1 labs.** It explains the "why" behind everything you'll build over the next three days. ~20 minutes.

By the end of this reading you will be able to:

- Explain what a business workflow is and which tasks are worth automating
- Tell the difference between an agent that only *talks* and a workflow that actually *does work*
- Use the four building-block terms — **trigger, actions, outputs, steps** — that recur in every single lab

---

## 1. What is business workflow automation?

A **business workflow** is a repeatable series of steps that gets work done. You already run dozens of them by hand every week. For example:

> *A customer emails an enquiry → someone records it in a spreadsheet → a salesperson is notified → they reply.*

Four small steps, but each one takes attention, and any of them can be forgotten, delayed, or done inconsistently.

**Automation** means letting software perform those steps for you — consistently, instantly, and the same way every time — instead of doing them by hand. The best candidates for automation share three traits:

| Trait | What it looks like | Everyday example |
|-------|--------------------|------------------|
| **Repetitive** | Done the same way many times | Logging enquiries, sending confirmations |
| **Rule-based** | Clear "if this, then that" logic | If amount > $1,000, get approval |
| **Time-consuming** | Manual copying, chasing, re-typing | Re-keying form data into a spreadsheet |

**What you gain:** fewer mistakes, faster turnaround, a complete record of what happened, nothing falling through the cracks — and people freed up for higher-value work that actually needs human judgement.

> **Rule of thumb:** if you find yourself doing the same clicking, copying, and emailing over and over, it is probably a workflow waiting to be automated.

In this course you automate workflows with **two** Microsoft tools that work as a pair:

- **Power Automate** — builds the automated steps (the **flows**) that do the work.
- **Copilot Studio** — builds AI **agents** that understand natural-language requests and feed clean, structured data into those flows.

You'll learn Power Automate first (Day 1), then agents (Day 2), then how to combine them (Day 3).

---

## 2. Standalone agents vs integrated workflows

It helps to be clear, from the very start, about the difference between an agent that just *answers* and a workflow that *acts*.

| | **Standalone agent** | **Integrated workflow** |
|---|---|---|
| What it does | Chats and answers questions | Performs real actions across systems |
| Example | "What's your return policy?" | Logs the enquiry, emails the team, files a ticket |
| Powered by | Copilot Studio alone | Copilot Studio **+** Power Automate |
| Outcome | Information | Action **+** record **+** notification |

A **standalone agent** is genuinely useful, but it only *talks*. Ask it a question, get an answer — the conversation ends and nothing changes in your business systems.

An **integrated workflow** connects that same agent to Power Automate, so the conversation actually *triggers work*: a record gets saved, an email gets sent, an approval gets started. The customer feels heard *and* the back-office task is already done.

```
Standalone agent:   User asks  →  Agent answers           (talk only)

Integrated:         User asks  →  Agent answers
                                   └─► triggers a flow ─►  log + email + approval
                                                          (talk AND action)
```

That bridge between conversation and action is the heart of this course.

---

## 3. Workflow logic: the four building blocks

Every workflow you build — whether a simple flow or a full agent-driven process — is made of these four parts. Learn these terms now; you will use them in *every* lab.

### Trigger — *what starts the workflow*

The single event that kicks everything off. Examples:

- An **email is received**
- A **file is uploaded** to a folder
- A **form is submitted**
- A **schedule** is reached (e.g. every morning at 9 AM)
- An **agent** calls the flow

> Every flow has **exactly one** trigger, and it does nothing until that trigger fires.

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

Outputs from one step become inputs to the next — in Power Automate this is called **dynamic content**, and it's how data flows down the chain.

### Steps — *the ordered sequence as a whole*

Trigger + actions, arranged top-to-bottom, make up the **steps** of the workflow. Steps can also include:

- **Conditions** — branching with if/else logic (e.g. *if amount > $1,000, route to a manager*)
- **Loops** — repeat an action for each item in a list

### Putting it together

```
TRIGGER            ACTIONS (steps)                       OUTPUTS
─────────          ──────────────────────────           ──────────
Email received  →  1. Read sender + subject          →  sender, subject
                   2. Add a row to Excel             →  logged record
                   3. Send notification to sales     →  confirmation
```

Read that left to right: an event happens, the flow performs a series of steps, and data (outputs) is produced and passed along the way. Keep this **Trigger → Actions → Output** mental model in your head — it is the spine of everything that follows.

---

## 4. How the three days fit together

| Day | You build | New skill | What it gives you |
|-----|-----------|-----------|-------------------|
| **Day 1** | Flows in **Power Automate** | Triggers, actions, outputs | The "hands" that do work — email, Excel logging, approvals |
| **Day 2** | Agents in **Copilot Studio** | Structured capture, tools | The "brain & mouth" that talk to people and produce clean data |
| **Day 3** | Agents **+** flows together | Orchestration | Complete **end-to-end** business workflows, then your own |

Day 1 is all about Power Automate. You'll master the trigger → action → output rhythm by building real flows you can run today.

---

**Next:** [Module 2: Introduction to Power Automate](Module%202%20-%20Introduction%20to%20Power%20Automate.md)

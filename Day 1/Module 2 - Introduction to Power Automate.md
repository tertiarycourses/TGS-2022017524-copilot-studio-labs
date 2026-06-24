# Module 2: Introduction to Power Automate

> **Read this after [Module 1](Module%201%20-%20Workflow%20Automation%20Concepts.md) and before the Day 1 labs.** ~15 minutes.

This module turns the **Trigger → Actions → Output** idea from Module 1 into the actual tool you'll use all day: **Power Automate**. By the end you'll recognise the flow types, the common triggers and actions, and the one thing that trips up every beginner — connections.

---

## 1. What is Power Automate?

**Power Automate** is Microsoft's automation platform. It lets you build **flows** — automated sequences of steps that run across Microsoft 365 and hundreds of other apps, with little or no code. You design a flow visually in a browser by stacking one **trigger** and one or more **actions** (exactly the building blocks from Module 1).

With Power Automate you can:

- React to events — an email arrives, a file is uploaded, a form is submitted
- Move and transform data between systems — Outlook, Excel, SharePoint, Teams, Dataverse, and more
- Run approvals, send notifications, and schedule recurring jobs
- Be called by a Copilot Studio **agent** as a tool (you'll do this on Day 2)

You build flows at **https://make.powerautomate.com**, inside the environment you set up in **Lab 0**.

> **Low-code, not no-thought.** You don't write code, but you do think like a designer: what starts the flow, what it does, and what data moves between steps.

### Types of flow you'll build in this course

There are four flavours of flow. They differ only in *how they start* — once running, they all do the same kind of work.

| Flow type | Started by | Example | Lab |
|-----------|-----------|---------|-----|
| **Instant** | A person clicking Run / a button | Send a confirmation email on demand | Lab 1–3 |
| **Scheduled** | A clock/timetable (Recurrence) | Daily reminder at 9 AM | Lab 4 |
| **Automated** | An event | New form response, new email, new file | Lab 5, Day 3 |
| **Agent flow** | A Copilot Studio agent | Agent logs a request and notifies the team | Day 2–3 |

---

## 2. Common triggers

Every flow starts with **exactly one trigger** — the event that kicks it off. These are the ones you'll use most:

| Trigger | Connector / name | Fires when… | Used in |
|---------|------------------|-------------|---------|
| **Email received** | Office 365 Outlook — *"When a new email arrives (V3)"* | Mail lands in a folder | Day 3, Lab 10 |
| **File upload** | OneDrive / SharePoint — *"When a file is created"* | A document is dropped into a folder | Day 3, Lab 11 |
| **Form submission** | Microsoft Forms — *"When a new response is submitted"* | Someone submits your form | Lab 5 |
| **Schedule** | *"Recurrence"* | A timetable you define is reached | Lab 4 |
| **Manual** | *"Manually trigger a flow"* | You press **Run** | Labs 1–3 |
| **Agent call** | *"When an agent calls the flow"* | A Copilot Studio agent runs the flow as a tool | Day 2–3 |

> **Tip — build with a manual trigger first.** When learning a new flow, start with a **manual** trigger so you can press Run and perfect the actions. Once they work, swap in the real trigger (form, email, schedule). The actions stay exactly the same — only the start event changes.

---

## 3. Creating workflow actions

After the trigger, you add **actions** — the work the flow performs. These are the core actions you'll lean on throughout the course:

### Send emails
*Office 365 Outlook → Send an email (V2).* Send confirmations, notifications, and digests. Use **dynamic content** (outputs from earlier steps) to personalise the subject and body. *(Lab 1)*

### Create Excel entries
*Excel Online (Business) → Add a row into a table* (and *List rows present in a table*). Log every record into a spreadsheet **table** — this becomes your audit trail and single source of truth. *(Lab 2)*

> Excel actions only see data that lives inside a proper **Table** (Insert → Table), not loose cells. This is a classic first-time gotcha.

### Notifications & approvals
- *Approvals → Start and wait for an approval.* Pause the flow until a person approves or rejects, then branch on the **Outcome**. *(Lab 3)*
- Notifications to **Teams** or email keep the right people informed at each step.

Actions are wired together with:

- **Dynamic content** — one step's output becomes the next step's input (Module 1's "outputs")
- **Conditions** — if/else branching to route the process

> **Heads-up on approvals:** the approver you pick must be a real **user in your Microsoft 365 tenant**. Approvals can't be sent to an outside personal email address — pick someone in your organisation (yourself is fine for testing).

### A note on expressions (fx)
Sometimes a field needs a small calculation or formatting — today's date, trimmed text, a number comparison. Power Automate provides an **expression editor** (the **fx** button) for this. You'll only need a few simple ones; we'll point them out in the labs when they appear.

---

## 4. Connections — how Power Automate reaches your apps

Each connector (Outlook, Excel, Approvals, Forms…) needs a **connection** — a saved sign-in that authorises the flow to act on your behalf. The first time you use a connector, you'll **sign in and consent**.

This is the **number one source of "why won't my flow run?"** for beginners, so commit it to memory:

| Connection state | What you'll see | What to do |
|------------------|-----------------|------------|
| **Healthy** | Green / connected | Good to go |
| **Broken / expired** | Red ⚠️ "Reconnect" | Reconnect before running |
| **Wrong rights** | **"Unauthorized"** error | The account lacks rights (e.g. no mailbox) — fix or use a different account |

> **The golden rule for every lab:** green connection = ready; red connection = reconnect first. An **Unauthorized** error almost always means: reconnect the connector or check that the signed-in account actually has permission for that action.

---

## 5. Anatomy of a flow (what you'll see in the designer)

```
[ TRIGGER ]        ← one event that starts the flow
    │
[ Action 1 ]       ← e.g. Get details / read data
    │
[ Condition ]      ← optional if/else branch
   ├── If yes → [ Action ]
   └── If no  → [ Action ]
    │
[ Action 2 ]       ← e.g. Send an email / Add a row
```

The build-and-verify loop is the same in every lab:

1. **Save** the flow.
2. **Test** it — manually, or by triggering the real event.
3. Review the **run history** — **green = success, red = error** — to confirm it worked or to debug.

Get comfortable with this loop today; you'll repeat it dozens of times across the three days.

---

**Next:** [Lab 1: Automated Email Workflow](Lab%201%20-%20Automated%20Email%20Workflow/index.md)

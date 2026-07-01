# Module 3: Building Business Agents with Copilot Studio

> **Read this before the Day 2 labs.** ~15 minutes.

On Day 1 you built the **hands** — Power Automate flows that send email, log to Excel, and run approvals. Today you build the **brain and mouth**: a Copilot Studio **agent** that talks to people in plain language and hands clean, structured data to those flows.

By the end of this reading you'll know what an agent is made of, how to make it produce *predictable* data (the make-or-break skill), and how an agent calls a flow as a tool.

---

## 1. What is a business agent?

A **business agent** is an AI assistant you build in **Copilot Studio**. People chat with it in natural language ("I'd like a quote for 100 units"), and the agent:

- **Understands** the request
- **Asks** for any missing details
- **Captures** the information as clean, structured data
- **Hands off** that data to a Power Automate flow to take action

```
   Day 1                          Day 2
 ┌────────┐                    ┌──────────┐
 │ FLOWS  │  the "hands"       │  AGENT   │  the "brain & mouth"
 │ do work│  ◄───── calls ──── │ talks &  │
 └────────┘                    │ captures │
                               └──────────┘
```

The agent is the friendly front door; the flow is the engine room behind it.

---

## 2. The building blocks of a Copilot Studio agent

An agent is assembled from five kinds of building block. You'll meet each one across today's labs.

| Block | What it is | Example | First seen |
|-------|------------|---------|-----------|
| **Instructions** | Plain-language directions that shape the agent's behaviour and personality | "You are a sales assistant. Always collect name, company, product, and quantity." | Lab 6 |
| **Knowledge** | Documents / sites the agent can answer from (RAG) | Product catalogue, FAQ | Lab 7 |
| **Topics** | Conversation flows the agent runs when the user's message matches the topic's **description** (generative orchestration, the default) or its **trigger phrases** (classic) | A "New Sales Enquiry" topic the agent chooses when someone asks for a quote | Lab 9 |
| **Tools / Actions** | Things the agent can *do*, including **Power Automate flows** | "Log enquiry to Excel" flow | Lab 8 |
| **Variables** | Where captured answers are stored to pass onward | `customerName`, `product`, `quantity` | Lab 9 |

> **Knowledge = RAG.** When you upload documents, the agent uses **Retrieval-Augmented Generation**: it *retrieves* the relevant passages from your files and *generates* an answer grounded in them — so it speaks from your content, not the open internet. You'll set this up in Lab 7.

---

## 3. Prompt design for structured outputs

This is the single most important skill for connecting agents to workflows: getting the agent to produce **structured, predictable data** — not just free-flowing chat.

**Why it matters.** A flow needs clean, named fields. Compare what the agent might hand over:

| The agent hands the flow… | Can the flow use it? |
|---------------------------|----------------------|
| `"the guy from ABC wants some units maybe 100"` | ❌ No — nothing to log reliably |
| `name=John, company=ABC, product=Widget, quantity=100` | ✅ Yes — every field drops straight into a row |

When the data is clean and structured, **every downstream step just works**. When it's messy, the whole workflow is unreliable.

### Three techniques to get structured output

1. **Capture into named variables.** Use question nodes that store each answer in its own variable (`customerName`, `email`, `quantity`). This is the most reliable method, and you'll use it in **Labs 9 and 10**.

2. **Write precise instructions.** Tell the agent exactly what to collect and in what form:
   > *"Collect these four items one at a time: customer name, company, product of interest, and quantity. Do not proceed until all four are provided. Confirm the details back to the user before finishing."*

3. **Ask AI to format the result.** When you want a generated summary, specify the format explicitly:
   > *"Summarize the enquiry as: Customer: &lt;name&gt;; Company: &lt;company&gt;; Product: &lt;product&gt;; Qty: &lt;quantity&gt;; Notes: &lt;notes&gt;."*

### Good-prompt checklist

- ✅ State the agent's **role and goal**
- ✅ List the **exact fields** to collect
- ✅ Specify the **output format**
- ✅ Say **what to do when information is missing**
- ✅ Keep **tone** instructions short and clear

> **Structured agent output = clean flow inputs.** This is the through-line of Day 2. If the agent captures tidy variables, the flow receives tidy inputs — and the handoff in section 4 works first time.

---

## 4. Connecting agents to Power Automate flows

Once the agent has captured the data, it calls a flow as a **tool**:

```
USER chats with AGENT  →  AGENT captures variables  →  AGENT calls FLOW (tool)
                                                          passing variables as inputs
                                                              │
                                                              ▼
                                            FLOW runs actions (log, email, approve)
                                                              │
                                                              ▼
                                            FLOW returns a result  →  AGENT confirms to user
```

The key points:

- The agent **passes its variables** (outputs) into the flow's **inputs**.
- The flow does the work and can **return a value** — say, a reference number — for the agent to show the user.
- This is exactly the same flow-building you learned on Day 1. **Only the trigger changes** — to *"When an agent calls the flow."*

> **It's still Day-1 Power Automate underneath.** Same designer, same actions, same Save → Test → run-history loop. The agent simply replaces the manual "Run" button as the thing that starts the flow.

---

## 5. What you'll build on Day 2

- **Lab 6:** Your first agent — learn the interface, instructions, and testing.
- **Lab 7:** Add **Knowledge (RAG)** so the agent answers from your own documents.
- **Lab 8:** Add **Tools & Actions** so the agent can *do* things, not just answer.
- **Lab 9:** A **Sales Enquiry Assistant** that captures enquiries as structured data.
- **Lab 10:** A **Procurement Request** agent that triggers a Power Automate flow.
- **Lab 11:** **Automated Response Generation** — use AI prompts to draft professional replies.

Each lab adds one capability on top of the last, so by Lab 11 you'll have an agent that understands, retrieves, captures, acts, and writes.

---

**Next:** [Lab 6: Create Your First Copilot Studio Agent](Lab%206%20-%20Create%20Your%20First%20Agent/index.md)

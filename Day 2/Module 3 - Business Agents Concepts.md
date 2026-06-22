# Module 3: Building Business Agents with Copilot Studio

> **Read this before the Day 2 labs.** ~15 minutes.

## 1. What is a business agent?

A **business agent** is an AI assistant you build in **Copilot Studio**. People chat with it in natural language ("I'd like a quote for 100 units"), and the agent:

- **Understands** the request
- **Asks** for any missing details
- **Captures** the information as clean, structured data
- **Hands off** that data to a Power Automate flow to take action

On Day 1 you built the "hands" (flows that do work). On Day 2 you build the "brain and mouth" (an agent that talks to people and produces tidy data for those hands).

## 2. The building blocks of a Copilot Studio agent

| Block | What it is | Example |
|-------|------------|---------|
| **Instructions** | Plain-language directions that shape the agent's behavior and personality | "You are a sales assistant. Always collect name, company, product, and quantity." |
| **Topics** | Conversation flows triggered by what the user says | A "New Sales Enquiry" topic triggered by "I want a quote" |
| **Knowledge** | Documents/sites the agent can answer from | Product catalogue, FAQ |
| **Tools / Actions** | Things the agent can *do*, including **Power Automate flows** | "Log enquiry to Excel" flow |
| **Variables** | Where captured answers are stored to pass onward | `customerName`, `product`, `quantity` |

## 3. Prompt design for structured outputs

The single most important skill for connecting agents to workflows is getting the agent to produce **structured, predictable data** — not just free-flowing chat.

**Why it matters:** A flow needs clean fields. If the agent hands over `"the guy from ABC wants some units maybe 100"`, the flow can't log it reliably. If it hands over `name=John, company=ABC, product=Widget, quantity=100`, every downstream step just works.

**How to get structured output — three techniques:**

1. **Capture into named variables.** Use question nodes that store each answer in its own variable (`customerName`, `email`, `quantity`). This is the most reliable method and you'll use it in Labs 5 and 6.

2. **Write precise instructions.** Tell the agent exactly what to collect and in what form:
   > *"Collect these four items one at a time: customer name, company, product of interest, and quantity. Do not proceed until all four are provided. Confirm the details back to the user before finishing."*

3. **Ask AI to format the result.** When you want a generated summary, instruct the format explicitly:
   > *"Summarize the enquiry as: Customer: <name>; Company: <company>; Product: <product>; Qty: <quantity>; Notes: <notes>."*

**Good prompt checklist:**
- ✅ State the agent's role and goal
- ✅ List the exact fields to collect
- ✅ Specify the output format
- ✅ Say what to do when information is missing
- ✅ Keep tone instructions short and clear

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

- The agent **passes outputs** (its variables) into the flow's **inputs**.
- The flow does the work and can **return** a value (e.g. a reference number) for the agent to show the user.
- This is exactly the same flow-building you learned on Day 1 — only the **trigger** changes to **"When an agent calls the flow."**

## 5. What you'll build on Day 2

- **Lab 4:** Your first agent — learn the interface, instructions, and testing.
- **Lab 5:** A **Sales Enquiry Assistant** that captures enquiries as structured data.
- **Lab 6:** A **Procurement Request** agent that triggers a Power Automate flow.
- **Lab 7:** **Automated Response Generation** — use AI prompts to draft professional replies.

---

**Next:** [Lab 4: Create Your First Copilot Studio Agent](Lab%204%20-%20Create%20Your%20First%20Agent/index.md)

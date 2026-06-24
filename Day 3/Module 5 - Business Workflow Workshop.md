# Module 5: Business Workflow Workshop

> **Read this before the Capstone (Lab 16).** ~10 minutes.

This is your briefing for the capstone. Everything you've learned across three days now comes together in one workflow that you design, build, and explain.

---

## 1. Purpose of the workshop

You've now learned every building block:

- **Power Automate** flows — email, Excel logging, approvals, scheduled and event triggers (Day 1)
- **Copilot Studio** agents — instructions, knowledge/RAG, tools, structured capture (Day 2)
- **End-to-end orchestration** — combining agents + flows across business domains (Day 3 morning)

The workshop is where you **put it together yourself**: design and build a complete, working workflow for a real business process — and explain its value to the business.

> Think of this as moving from *following* recipes to *cooking your own dish* with the techniques you've practised.

---

## 2. The four business domains

Your capstone targets one (or more) of these domains. Each maps directly to labs you've already built — so you're never starting from a blank page; you're adapting and combining work you understand.

| Domain | Typical workflow | Built on |
|--------|------------------|----------|
| **Sales** | Enquiry/lead capture → log → acknowledge → notify rep | Labs 9, 12 |
| **Finance** | Invoice/expense submitted → approve by amount → notify | Labs 3, 13 |
| **Procurement** | Purchase request → manager approval → notify + log | Labs 10, 14 |
| **Order Processing** | Order captured → confirm → log → restock alert | Lab 15 |

> **Pick the domain you understand best.** A workflow you can explain confidently is worth more than an ambitious one you can't finish.

---

## 3. Design method (recap from Module 4)

Run through this **before** you build — it's the same discipline from Module 4:

1. **One sentence:** *"When ___ happens, do ___, then ___, and finally ___."*
2. **Trigger:** manual / scheduled / form / email / file / agent call
3. **Capture:** the fields/variables you need
4. **Actions in order:** log, generate, approve, notify…
5. **Decision points:** the condition(s) and each branch
6. **End states:** final status + who is notified for each outcome

If you can write step 1 cleanly, the rest of the design tends to fall into place.

---

## 4. Quality bar

A strong capstone workflow:

- ✅ Has a clear **trigger** and runs **end to end**
- ✅ **Captures or receives** data and **logs** it (Excel)
- ✅ Includes at least one **condition** (branching)
- ✅ Includes an **approval** *or* an **AI-generated** response
- ✅ **Notifies** the right people for **every** outcome
- ✅ Is **tested** on the happy path **and** every branch

> Treat this as your self-check list. Before you call the capstone "done," walk down it and tick each item.

---

## 5. Tips for success

- **Start small, then add.** Get a basic happy-path flow working end to end first, then layer on conditions, approvals, and notifications.
- **Test after each step** — don't build everything and then test once. Small tests catch problems while they're still easy to find.
- **Reuse your earlier labs as templates** — see the Capstone's reuse list. Adapting working flows is faster and safer than rebuilding from scratch.
- **Check connections are green before running** — a red connector or an **Unauthorized** error means: reconnect first.
- **Remember the approver rule** — approvals must go to a real **user in your tenant** (yourself is fine for testing), never an outside personal email.
- **Use a Status column** in Excel as the single source of truth, updated at each stage.
- **Keep agent output structured** — clean variables in means clean flow inputs out.

> **One sentence, built carefully, tested fully.** That's a winning capstone. Good luck.

---

**Next:** [Lab 16: Capstone Workshop](Lab%2016%20-%20Capstone%20Workshop/index.md)

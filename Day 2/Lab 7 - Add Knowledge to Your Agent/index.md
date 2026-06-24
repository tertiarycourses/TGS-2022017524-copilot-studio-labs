# Lab 7: Add Knowledge to Your Agent (Grounding / RAG)

## Lab Title
Ground Your Agent in Your Own Documents with Knowledge (RAG)

## Lab Objectives
By the end of this lab, you will be able to:
1. Explain **grounding** and **RAG** (Retrieval-Augmented Generation) in plain, everyday terms
2. Add one or more **Knowledge** sources to a Copilot Studio agent (files, public website, or SharePoint)
3. Turn **general knowledge** off so the agent answers only from your content
4. Test that the agent answers **from your documents** and shows **citations**
5. Confirm the agent declines to answer when the information is not in your sources (no made-up answers)
6. Tell the difference between **Instructions** (behaviour) and **Knowledge** (facts)

## Prerequisites
- Completed [Lab 6](../Lab%206%20-%20Create%20Your%20First%20Agent/index.md) (you have an agent)
- A short document to use as knowledge (a PDF/Word FAQ, or a public website URL)

## Scenario
Your **Company Helpdesk** agent from Lab 6 can chat, but it does not actually know **ACME Pte Ltd's** real facts — its return policy, its opening hours, its product list. An agent that only knows general internet information is not very useful for *your* business.

In this lab you will give the agent a **Knowledge** source containing ACME's own information, then prove that the agent answers from that source and nothing else. This is the technique that makes business agents trustworthy.

> **Tip:** **Grounding** means tying the agent's answers to specific source material you provide, so it cannot just invent things. **RAG** (Retrieval-Augmented Generation) is the technology that does this.

### How RAG works (in plain terms)
1. You add documents to **Knowledge**. Copilot Studio breaks them into small passages and indexes them.
2. A user asks a question.
3. The agent **retrieves** the few passages most relevant to that question.
4. The agent **generates** an answer using *only* those passages, and shows **citations** pointing back to the source.

> **RAG in one line:** *Find the relevant text in your documents → hand it to the AI → it answers from that text, with citations.* This keeps answers accurate and up to date without retraining any model.

---

## Step-by-Step Guide

### Step 1: Prepare a knowledge source (~5 minutes)

Pick **one** source to start (you can add more later). Choose whichever is easiest for you:

1. **A file (recommended for this lab):** Create a one-page document called `ACME Company FAQ`. Save it as a **PDF** or **Word** file. Include a few clear facts the agent will answer from, for example:
   ```
   ACME Pte Ltd - Company FAQ

   Opening hours: Monday to Friday, 9am to 6pm. Closed on public holidays.
   Return policy: Items may be returned within 30 days with a receipt.
   Contact: Email help@acme.example or call +65 6123 4567.
   Top products: ACME Widget Pro, ACME Gadget Lite, ACME Toolkit.
   ```
2. **A public website:** any URL whose content you want the agent to use (e.g. a real product page).
3. **A SharePoint** site or document library, if your tenant has one with relevant files.

> **Tip:** Keep the document focused and tidy — use clear headings and short paragraphs. Clean, well-structured content leads to much better retrieval and more accurate answers.

### Step 2: Open your agent's Knowledge tab (~3 minutes)

1. Go to **https://copilotstudio.microsoft.com** and confirm the **environment selector** (top-right) shows **NUS Copilot Sandbox**.
2. Open your **Company Helpdesk** agent from Lab 6.
3. Select the **Knowledge** tab.
4. Select **+ Add knowledge**.

> **⚠️ Warning:** Make sure you are in the **same environment** as your Lab 6 agent and your Power Automate flows. If the environment is wrong, you may be editing a different (or empty) agent.

### Step 3: Add the knowledge source (~10 minutes)

1. On the **Add knowledge** screen, choose the type that matches your source:
   - **Files** / **Upload** — then select and upload your `ACME Company FAQ` PDF or Word file.
   - **Public website** — then paste the URL.
   - **SharePoint** — then paste the site or library URL.
2. Give the source a clear **name**, for example `ACME Company FAQ`.
3. If you are prompted for a **description**, write a short sentence describing what it contains, e.g. `ACME opening hours, return policy, contact details, and top products.` The agent uses this description to decide when this source is relevant.
4. Select **Add**.
5. Watch the source's **status**. It will show **Processing** and then change to **Ready**. Larger files and websites take a little longer.

> **⚠️ Warning:** Do **not** test until the status reads **Ready**. While a source is still **Processing**, the agent cannot use it and may reply that it has no information.

### Step 4: Turn off general knowledge (optional but recommended) (~4 minutes)

By default the agent may blend in general AI/web knowledge. For a business helpdesk you usually want answers **only** from ACME's documents.

1. Open the agent's **Settings** (gear icon, usually top-right) and look for the **Generative AI** section. (Depending on your version, this setting may also appear on the **Overview** page near the Knowledge area.)
2. Find the option **Use general knowledge** (it may read *"Allow the AI to use its own general knowledge"* or similar).
3. Turn it **Off** so the agent relies only on your sources.
4. Select **Save**.

> **Tip:** Turn general knowledge **on** when you want the agent to also answer broad, everyday questions. Turn it **off** when you need tight control and want to prevent answers that did not come from your documents.

### Step 5: Test that answers come from your document (~10 minutes)

1. Open the **Test** pane and select **Refresh** at the top so it picks up your new Knowledge.
2. Ask questions that can **only** be answered from your `ACME Company FAQ`, for example:
   - `What is your return policy?`
   - `What are your opening hours?`
   - `Which products do you offer?`
3. Confirm each answer matches the facts in your document.
4. Look **underneath each answer** for **citations** or **references** (often numbered, like `[1]`, or a "1 reference" link). Click a citation to confirm it points back to your source.

> **Tip:** Citations are your proof that grounding worked. If an answer has no citation, it may have come from general knowledge rather than your document.

### Step 6: Confirm the agent declines when it doesn't know (~5 minutes)

This is the most important test — it proves the agent will not make things up.

1. In the **Test** pane, ask something that is **not** in your document, for example:
   - `What is your CEO's home address?`
   - `Do you sell aeroplanes?`
2. The agent should say it does not have that information (and, following your Lab 6 Instructions, suggest emailing `help@acme.example`).
3. If instead it confidently invents an answer, that is a **hallucination**. Re-check that **general knowledge is Off** (Step 4) and that your Instructions tell it to answer only from provided sources.

> **Tip:** A trustworthy business agent saying *"I don't have that information"* is a success, not a failure. Declining gracefully is exactly the behaviour you want.

### Step 7: Tune your sources (~5 minutes)

1. If an answer is weak or missing, improve the **source document** — add clearer headings and more detail — then re-upload or refresh the source.
2. Add a **second** Knowledge source for broader coverage (for example, a product page website). Give each source a **distinct name and description** so the agent can tell them apart.
3. Reinforce grounding in the **Instructions** (Overview tab). Add a line such as:
   ```
   Only answer using the provided knowledge sources, and cite them.
   If the answer is not in the sources, say you don't have that information.
   ```
4. Select **Save**, refresh the Test pane, and re-test.

---

## Checkpoint
You have successfully completed this lab when:
- ✅ At least one **Knowledge** source shows the status **Ready**
- ✅ The agent answers business questions **from your document**, with visible **citations**
- ✅ **General knowledge** is turned **Off** (if you chose the recommended setup)
- ✅ The agent **declines** to answer (no hallucination) when the information is not in your sources
- ✅ You can explain the difference between **Instructions** and **Knowledge**

## Troubleshooting
| Problem | Cause | Solution |
|---------|-------|----------|
| Source stuck on "Processing" | Large or busy source | Wait a minute or two; if it persists, try a smaller file or a single web page. |
| Agent ignores the document | Source not ready, or no description | Confirm the source is **Ready**; add a clear description; in Instructions, tell it to answer from knowledge. |
| Answers come from the web, not my doc | General knowledge is on | Turn **off** **Use general knowledge** in Settings → Generative AI, then **Save** and refresh the Test pane. |
| No citations appear | Answer was not grounded | Ensure the answer actually came from a Ready source; check that general knowledge is off. |
| Agent makes things up | Hallucination | Turn off general knowledge and add an Instruction to decline when info is missing. |
| Edits not reflected in chat | Test pane caching | Click **Refresh** at the top of the **Test** pane to restart the conversation. |

## Key Takeaways
- **Knowledge = grounding (RAG):** the agent retrieves passages from your documents and answers from them, with citations.
- Use **Instructions** for *behaviour and tone*; use **Knowledge** for *facts*.
- Turning **general knowledge off** keeps answers strictly inside your own content.
- **Citations** let you and your users verify exactly where an answer came from.
- A grounded agent that **declines** when it doesn't know is working correctly — that is how you avoid hallucinations.

## Duration
~40 minutes

## Next Steps
Proceed to [Lab 8: Add Tools and Actions to Your Agent](../Lab%208%20-%20Add%20Tools%20and%20Actions/index.md).

# Lab 7: Automated Response Generation

## Lab Title
Use AI Prompts to Generate Professional Responses Automatically

## Lab Objectives
By the end of this lab, you will be able to:
1. Add an **AI prompt (Prompt action)** inside a flow or agent
2. Feed captured data into the prompt to generate tailored text
3. Control the **format and tone** of the generated output
4. Send the AI-generated response by email
5. Compare static templates vs AI-generated responses

## Prerequisites
- Completed [Lab 6](../Lab%206%20-%20Procurement%20Request%20Workflow/index.md)
- A Sales Enquiry Assistant or similar agent (from Lab 5) you can reuse

## Scenario
Instead of sending the same canned reply to every enquiry, you'll use an **AI prompt** to draft a personalized, professional response based on the customer's details — then email it automatically. This shows how generative AI turns structured data into polished communication.

---

## Step-by-Step Guide

### Step 1: Decide where the AI prompt runs (~5 minutes)
There are two equivalent places to add an AI prompt; this lab uses the **flow** approach because it builds directly on Day 1/Lab 6 skills:
- **In a Power Automate flow:** use the **AI prompt** action (Prompt builder / "Create text with GPT").
- **In Copilot Studio:** add a **Prompt** tool to a topic.

> Both call the same underlying AI. The flow approach keeps all your actions (generate + email) in one place.

### Step 2: Reuse the Sales Enquiry Assistant and add a flow (~10 minutes)
1. Open your **Sales Enquiry Assistant** (Lab 5) → **New Sales Enquiry** topic.
2. After the summary message, select **+** → **Add a tool** → **New Agent flow**.
3. In Power Automate, the trigger is **When an agent calls the flow**. Add inputs:
   - **Text** `customerName`
   - **Text** `company`
   - **Text** `product`
   - **Number** `quantity`

### Step 3: Add the AI prompt action (~15 minutes)
1. **+ New step** → search **AI prompt** (also called **Run a prompt** / **Create text with GPT using a prompt**) under **AI Builder**.
2. Choose to **create a new prompt**.
3. Write the prompt instruction, inserting the inputs as dynamic values:
   ```
   Write a warm, professional email reply (max 120 words) to a sales enquiry.
   Customer name: {customerName}
   Company: {company}
   Product of interest: {product}
   Quantity: {quantity}

   The email should:
   - Thank the customer by name
   - Acknowledge the product and quantity
   - Say a sales representative will follow up within 1 business day with pricing
   - End with a professional sign-off from "The ACME Sales Team"
   Output only the email body text.
   ```
4. **Save** the prompt. The action now outputs generated text (e.g. **Text** / **Response**).

> Notice the prompt **specifies length, tone, content, and format** — this is structured prompt design from Module 3 applied to *output generation*.

### Step 4: Email the generated response (~10 minutes)
1. **+ New step** → **Office 365 Outlook → Send an email (V2)**.
2. **To:** your email (for testing; in production use a captured customer email variable).
3. **Subject:** `Re: Your enquiry about ` + dynamic content **product**
4. **Body:** insert the AI prompt's **output text** (the generated email).
5. (Optional) Add a **Respond to the agent** step returning `Reply drafted and sent.`
6. **Save / Publish** the flow, then **Go back to agent**.

### Step 5: Wire inputs and test (~10 minutes)
1. In the topic, map the flow inputs to the variables: `customerName`, `company`, `product`, `quantity`.
2. **Save** the topic.
3. In the **Test** pane, run the enquiry: name `Mei Ling`, company `BrightTech`, product `Air Fryer Pro`, quantity `25`.
4. Confirm:
   - The flow runs successfully.
   - You receive a **uniquely worded, personalized** email (not a fixed template).
5. Run it again with different details and compare — the AI adapts the wording each time.

### Step 6: Compare template vs AI (~5 minutes)
- The **static template** (Lab 1) is fast and predictable but identical every time.
- The **AI-generated** response is personalized and natural, but you must guide it with a precise prompt and review for accuracy.
- **Best practice:** use AI for drafting, and keep critical facts (prices, policies) as controlled static text or knowledge.

---

## Checkpoint
- ✅ A flow that calls an **AI prompt** with the enquiry details
- ✅ A personalized email generated and sent automatically
- ✅ Understanding of how to control AI output format/tone

## Troubleshooting
| Problem | Solution |
|---------|----------|
| No AI prompt action | Search **AI Builder** / **Create text with GPT**; ensure AI Builder is available in your region/environment (the developer/trial environment includes it). |
| Output too long / wrong tone | Tighten the prompt: state word limit, tone, and "output only the email body." |
| Variables not in output | Confirm you inserted them as dynamic content inside the prompt text. |
| Email body shows prompt instructions | Add "Output only the email body text." and map only the prompt **output**. |

## Key Takeaways
- **AI prompts** turn structured data into polished, personalized text.
- Control quality by specifying **length, tone, content, and format**.
- Combine AI drafting with controlled facts for reliable, professional responses.

## Duration
~45 minutes

## Next Steps
You've completed Day 2. Proceed to [Day 3 — Module 4: End-to-End Orchestration Concepts](../../Day%203/Module%204%20-%20End-to-End%20Orchestration%20Concepts.md).

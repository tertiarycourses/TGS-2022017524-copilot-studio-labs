# Lab 6: Create Your First Copilot Studio Agent

## Lab Title
Create, Configure, and Test Your First Business Agent

## Lab Objectives
By the end of this lab, you will be able to:
1. Create a new agent in Microsoft Copilot Studio using **Skip to configure**
2. Write clear **Instructions** that shape how your agent behaves
3. Identify the main building blocks of an agent (Instructions, Knowledge, Topics, Tools)
4. Add one **Knowledge** source so your agent can answer real questions
5. Test and iterate on your agent in the built-in **Test** pane
6. Publish your agent (optional) and understand what Channels are

## Prerequisites
- Completed [Lab 0](../../Day%201/Lab%200%20-%20Environment%20Setup/index.md) (Copilot Studio trial active)
- Read [Module 3](../Module%203%20-%20Business%20Agents%20Concepts.md)
- Signed in at https://copilotstudio.microsoft.com (same environment as Power Automate)

## Scenario
You work in IT at **ACME Pte Ltd**, a small company. Staff keep emailing IT the same basic questions: opening hours, who to contact, how to reset things. You will build a friendly **Company Helpdesk** agent that answers these questions automatically.

This lab is your guided tour of Copilot Studio. You will learn the interface and the core idea that **Instructions are the heart of the agent** before you build data-capturing, action-taking agents in the labs that follow.

> **Tip:** An "agent" (sometimes still called a "copilot") is just an AI assistant you configure. You do not write code — you describe what you want in plain English, add some reference material, and test it in a chat window.

---

## Step-by-Step Guide

### Step 1: Confirm your environment (~3 minutes)

Before you build anything, make sure you are in the correct environment. This is the single most common cause of problems later in the course.

1. Go to **https://copilotstudio.microsoft.com** and sign in with your course account.
2. Look at the **top-right corner** of the screen. You will see an **environment selector** (a small label showing the current environment name, often with a globe or building icon).
3. Click it and select **NUS Copilot Sandbox** (your course environment from Lab 0).

> **⚠️ Warning:** Copilot Studio **must use the same environment as Power Automate**. If your agent is built in one environment and your flows live in another, they will not be able to connect to each other in Day 3. Always confirm the environment name in the top-right before you start. The environment also needs **Dataverse** enabled, because agents are stored there.

### Step 2: Create the agent with Skip to configure (~10 minutes)

1. In the left menu, select **Create**, then select **New agent**.
2. Copilot Studio opens a **conversational setup** screen that says something like *"Describe your agent to create it."* You could chat with it to build the agent — but for this lab you will fill in the form yourself so you understand every field.
3. Select **Skip to configure** (a link near the top-right of that screen). This opens a simple form.
4. Fill in the form:
   - **Name:** `Company Helpdesk`
   - **Description:** `Answers general questions about ACME Pte Ltd for staff and customers.`
   - **Instructions:** copy and paste the text below into the **Instructions** box:
     ```
     You are the Company Helpdesk agent for ACME Pte Ltd.
     Be friendly, concise, and professional.
     Answer questions about our products, opening hours, and contact details.
     If you do not know an answer, politely say so and suggest emailing help@acme.example.
     Keep replies to 2-3 sentences.
     ```
5. Select **Create** (top-right). Wait a few seconds while the agent is built. The agent's main page then opens.

> **Tip:** Think of the three fields like this — **Name** is what people see, **Description** is a short note for *you* (and helps other agents/tools recognise it later), and **Instructions** are the actual rules the AI follows in every conversation. Instructions are where almost all of your effort goes.

### Step 3: Tour the agent workspace (~5 minutes)

Now that the agent exists, get familiar with the layout. Near the top of the page you will see several tabs. The exact labels can shift slightly between versions, but you will find these building blocks:

1. **Overview** — a summary of your agent and quick links to its parts.
2. **Knowledge** — the documents, websites, and data the agent can read to find facts (you will use this in Step 4 and much more in Lab 7).
3. **Topics** — scripted, step-by-step conversation flows you design by hand for predictable questions.
4. **Tools** (sometimes shown as **Actions**) — things the agent can *do*, such as send an email or run a Power Automate flow (covered in Lab 8).
5. The **Test** pane — a chat panel, usually on the right. If you do not see it, select **Test** at the top-right.

Click through each tab once so you know where things are. You do not need to change anything yet.

> **Tip:** Remember the four building blocks: **Instructions** = behaviour and tone, **Knowledge** = facts the agent can look up, **Topics** = scripted conversations, **Tools/Actions** = things the agent can do. Almost everything in Copilot Studio is one of these four.

### Step 4: Add one Knowledge source (~10 minutes)

Right now your agent only knows what is in its Instructions. Give it something real to answer from.

1. Open the **Knowledge** tab.
2. Select **+ Add knowledge**.
3. Choose **Public website** (the simplest option — no files needed).
4. In the URL box, paste a relevant website. For practice, use the Microsoft Copilot Studio docs:
   `https://learn.microsoft.com/microsoft-copilot-studio/`
   *(Alternatively, if you have a short company FAQ as a PDF or Word file, choose the **Files** option and upload it instead.)*
5. Give the source a short, clear **name** such as `Copilot Studio docs` and, if asked, a one-line **description** of what it contains.
6. Select **Add**.
7. Watch the source's status. It will show **Processing** (or a spinner) and then change to **Ready**. Wait until it says **Ready** before testing — this can take a minute or two.

> **Tip:** A website source lets the agent ground its answers in real content instead of guessing. You will go much deeper on Knowledge in Lab 7.

### Step 5: Test your agent (~7 minutes)

1. Open the **Test** pane on the right. If it is hidden, select **Test** at the top-right.
2. Type these questions one at a time and read the replies:
   - `What can you help me with?`
   - `What is Copilot Studio?`
   - `How do I contact support?`
3. Notice two things working together:
   - Your **Instructions** control the *style* — friendly, short (2-3 sentences), professional.
   - Your **Knowledge** controls the *facts* — answers drawn from the website you added.

> **Tip:** The Test pane updates as you build. After most changes you make, come back here and re-test. This build-then-test loop is exactly how real agents are developed.

### Step 6: Iterate on your Instructions (~5 minutes)

The first version of an agent is rarely perfect. Tuning the Instructions is normal and expected.

1. Suppose replies are too long or too formal. Open the **Overview** tab and find the **Instructions** box.
2. Add a line to make the change you want, for example:
   ```
   Always greet the user by name if they give it.
   Never give legal or financial advice; suggest contacting a manager instead.
   ```
3. Select **Save**.
4. Go back to the **Test** pane. If your earlier conversation is still showing, select **Refresh** (or the circular-arrow icon) at the top of the Test pane so it picks up the new Instructions, then ask again.

> **⚠️ Warning:** The Test pane does **not** always pick up changes automatically. If your edit does not seem to take effect, click **Refresh** at the top of the Test pane to restart the conversation.

### Step 7: Publish the agent (optional) (~5 minutes)

Publishing makes your latest version live so it can be shared. You do not have to deploy it anywhere yet.

1. Select **Publish** (top-right), then confirm by selecting **Publish** again in the dialog.
2. Once publishing finishes, open the **Channels** tab. **Channels** are the places people can use your agent — for example Microsoft Teams, a demo website, or a custom app.
3. Browse the list to see your options. You do not need to connect any channel now; publishing alone is enough to keep your latest version testable.

---

## Checkpoint
You have successfully completed this lab when:
- ✅ You confirmed you are in the **NUS Copilot Sandbox** environment (matching Power Automate)
- ✅ An agent named **Company Helpdesk** exists with your custom **Instructions**
- ✅ At least one **Knowledge** source shows the status **Ready**
- ✅ The agent gives sensible, on-style answers in the **Test** pane
- ✅ You edited the Instructions and saw the change after refreshing the Test pane

## Troubleshooting
| Problem | Cause | Solution |
|---------|-------|----------|
| Agent ignores your new instructions | Test pane is showing the old conversation | Select **Save**, then click **Refresh** at the top of the **Test** pane to restart the chat. |
| Knowledge source stuck on "Processing" | Large website or busy service | Wait a minute or two. If it persists, remove it and add a smaller single page or a short PDF instead. |
| Replies are generic or unhelpful | No grounding, or vague instructions | Make sure a Knowledge source is **Ready** and tighten your Instructions (be specific about tone and scope). |
| Can't see the Test pane | Pane is collapsed | Select **Test** at the top-right of the agent page. |
| Tools/flows won't connect later | Wrong environment | Use the **environment selector** (top-right) to switch to the same environment as Power Automate (**NUS Copilot Sandbox**). |
| "Skip to configure" link not visible | UI variation | Look near the top-right of the "Describe your agent" screen; if missing, briefly chat a one-line description, then edit the fields afterwards on the Overview tab. |

## Key Takeaways
- An agent's behaviour is shaped mainly by its **Instructions** — clear instructions give predictable answers.
- The four building blocks are **Instructions** (behaviour/tone), **Knowledge** (facts), **Topics** (scripted chats), and **Tools/Actions** (doing things).
- **Knowledge** grounds answers in real content so the agent stops guessing.
- The **Test** pane is your build-and-iterate loop — refresh it after each change.
- Always work in the **same environment** as your Power Automate flows, and that environment needs **Dataverse**.

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 7: Add Knowledge to Your Agent](../Lab%207%20-%20Add%20Knowledge%20to%20Your%20Agent/index.md).

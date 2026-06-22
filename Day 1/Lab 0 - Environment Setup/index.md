# Lab 0: Environment Setup — Create Your Copilot Studio & Power Automate Accounts

## Lab Title
Environment Setup — Create Your Microsoft 365, Power Automate, and Copilot Studio Accounts

## Lab Objectives
By the end of this lab, you will be able to:
1. Obtain a Microsoft 365 account that can use Power Platform
2. Sign in to Power Automate and confirm you have a working environment
3. Sign in to Copilot Studio and start a free trial
4. Verify Outlook and Excel (OneDrive) are available for the later labs
5. Understand the difference between a work/school account and a personal account

## Prerequisites
- A web browser (Microsoft Edge or Google Chrome recommended)
- A mobile phone (used once for security verification)
- A credit card *(only if you create a new Business trial in Option B — it is not charged during the free month)*
- About 20–30 minutes

> **Which account should I use?**
> - **Option A — You already have a Microsoft 365 work/school account** (e.g. `name@company.com` provided by your organization). Try this first — you may already have everything. Go to **Step 1**.
> - **Option B — You do NOT have a work/school account** (you only have a personal `@outlook.com` / `@gmail.com`). Power Automate and Copilot Studio require a *work or school* account, so you'll create one via a free **Microsoft 365 Business trial**. Go to **Option B** below first, then continue from Step 2.

> ⚠️ **Why not the Microsoft 365 Developer Program?** As of 2024, Microsoft restricted the free Developer Program E5 sandbox to people with an active **Visual Studio Enterprise or Professional subscription**. If you sign up without one, you'll see *"You don't currently qualify for a Microsoft 365 Developer Program sandbox subscription."* — so we no longer use that path. Use Option B instead.

---

## Step-by-Step Guide

### Option B (only if you have no work/school account): Create a free Microsoft 365 Business trial (~15 minutes)

This creates a new *work* account `you@yourname.onmicrosoft.com` with Microsoft 365 (Outlook, Excel, OneDrive, SharePoint), which is what Power Automate and Copilot Studio need.

1. Open a browser and go to **https://www.microsoft.com/microsoft-365/business** (or search "Microsoft 365 Business Standard free trial").
2. Choose **Microsoft 365 Business Standard** and select **Try free for 1 month**.
3. Enter an email address to start. When prompted, choose **Set up account** / **Create a new account**.
4. Fill in your details (name, business name — you can use your own name, country, phone for verification).
5. Create your **sign-in details**: a username and a domain, giving you `admin@yourname.onmicrosoft.com`. **Write these down** — this is the account you'll use for the whole course.
6. Verify with the code sent to your phone.
7. Add a **payment method** (credit card). You are **not charged during the 1-month free trial**. Set a reminder to **cancel before the trial ends** if you don't want to keep it.
8. Wait 1–2 minutes for provisioning. You now have a Microsoft 365 work tenant.

> **Tips:**
> - If your company email (e.g. `name@company.com`) is already on Microsoft 365, you do **not** need this — use **Option A**.
> - In a classroom, your trainer may provide a ready-made account; ask before creating a trial.
> - To avoid charges, cancel the trial in the **Microsoft 365 admin center → Billing → Your products** before the renewal date.

---

### Step 1: Sign in to the Microsoft 365 portal (~5 minutes)

1. Go to **https://www.office.com** (or **https://m365.cloud.microsoft**).
2. Select **Sign in** and enter your **work/school account** (Option A) or your new **Business trial account** (Option B), then your password.
3. If this is your first sign-in, you may be asked to set up multi-factor authentication (MFA). Follow the prompts using your mobile phone.
4. Once signed in, you should see the Microsoft 365 home page with app tiles (Outlook, Word, Excel, etc.).
5. Confirm you can open **Outlook** (click the Outlook tile). Send yourself a quick test email to confirm it works — you'll use Outlook in Lab 1.
6. Confirm you can open **Excel** and that it saves to **OneDrive** — you'll use this in Lab 2.

> **If you don't see Outlook or Excel:** your account may not have a Microsoft 365 license. Ask your IT administrator to assign one, or use the Business trial account from Option B.

---

### Step 2: Sign in to Power Automate (~5 minutes)

Power Automate is where you build the automated workflows (called **flows**).

1. Open a new tab and go to **https://make.powerautomate.com**.
2. Sign in with the **same account** you used in Step 1.
3. The first time, you may be asked to **select your country/region** — choose the correct one and select **Get started**. (This sets your default Power Platform environment.)
4. You should now see the Power Automate home page with a left-hand menu: **Home, Create, My flows, Templates, Connectors, More**.
5. Look at the **top-right corner** — there is an **Environment** selector (e.g. *"<Your Name>'s Environment"* or *"Default"*). Note which environment is selected; you will build all your flows here.

   > **What is an environment?** An environment is a container that holds your flows, agents, and data. For this course, the **default** environment is fine.

6. Select **My flows** in the left menu — it will be empty for now. That's expected.

> **Free Power Automate:** A Power Automate use-rights plan is included with most Microsoft 365 licenses, which is enough for this course. If prompted, you can also start a **free 90-day trial** of Power Automate Premium.

---

### Step 3: Sign in to Copilot Studio and start a free trial (~5 minutes)

Copilot Studio is where you build the AI **agents** (used on Day 2 and Day 3).

1. Open a new tab and go to **https://copilotstudio.microsoft.com**.
2. Sign in with the **same account** again.
3. If prompted, select your **country/region** and select **Start free trial** (or **Try free**). This activates a **30-day Copilot Studio trial** at no cost.
4. Wait for the workspace to load. You'll see the Copilot Studio home page with options to **Create** an agent.
5. Confirm the **Environment** selector (top-right) shows the **same environment** you used in Power Automate. This is important — your agents and flows must live in the same environment to connect to each other.

   > If the environments differ, click the environment selector and choose the one you used in Step 2.

6. Do **not** create an agent yet — you'll do that in Lab 4. For now, just confirm the page loads.

---

### Step 4: Verify your full setup (~5 minutes)

Run this quick checklist. Each item should already be true if the steps above succeeded:

| # | Check | Where |
|---|-------|-------|
| 1 | I can sign in and see app tiles | https://www.office.com |
| 2 | I can open Outlook and send myself an email | Outlook |
| 3 | I can open Excel and it saves to OneDrive | Excel / OneDrive |
| 4 | Power Automate home page loads, I can see **My flows** | https://make.powerautomate.com |
| 5 | Copilot Studio loads and my trial is active | https://copilotstudio.microsoft.com |
| 6 | Power Automate and Copilot Studio show the **same environment** | Top-right selector in both |

If all six are checked, your environment is ready.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "You can't sign in here with a personal account" | Power Platform needs a *work/school* account. Use Option B to create one via the Business trial. |
| Power Automate says "no environment" | Refresh, re-select your region, or pick an environment in the top-right selector. |
| Copilot Studio trial button missing | You may already have a license; just proceed. Otherwise sign out and back in. |
| Different environment in each tool | Click the environment selector (top-right) in each tool and choose the same one. |
| No Outlook/Excel tiles | Your account lacks a Microsoft 365 license — ask IT or use the Business trial account (Option B). |

---

## Duration
~20–30 minutes

## Next Steps
Read [Module 1: Workflow Automation Concepts](../Module%201%20-%20Workflow%20Automation%20Concepts.md), then proceed to [Lab 1: Automated Email Workflow](../Lab%201%20-%20Automated%20Email%20Workflow/index.md).

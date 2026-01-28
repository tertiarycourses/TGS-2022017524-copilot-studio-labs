# Lab 11: Publish Your Agent

## Lab Title
Publish Your Agent - Deploy to Teams and M365 Copilot

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand why publishing is important for agent updates
2. Publish your agent to make changes live
3. Add the Microsoft Teams and M365 Copilot channel
4. Deploy the agent to Teams for personal use
5. Submit the agent for organization-wide availability

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Fully configured Contoso Helpdesk Agent (from Labs 6-10)
- Microsoft Teams access
- Permissions to publish agents in your environment

## Step-by-Step Guide

### Step 1: Understanding Publishing (~5 minutes)
1. Learn why publishing matters:
   - Makes latest updates available to users
   - New tools and knowledge become accessible
   - All configured channels receive updates
2. Understand that unpublished changes are only visible in development
3. Review: Always publish after making agent changes

### Step 2: Explore Available Channels (~5 minutes)
1. Review channel options:
   - **Teams & M365 Copilot**: Teams chats, meetings, Copilot
   - **Demo website**: Copilot Studio test site
   - **Custom website**: Embed in your site
   - **Mobile app**: Custom mobile integration
   - **SharePoint**: Site-based assistance
   - **Facebook Messenger**: Social platform
   - **Power Pages**: Power Pages websites
   - **Azure Bot Service**: Slack, Telegram, Twilio, etc.

### Step 3: Publish Your Agent (~5 minutes)
1. Open your Contoso Helpdesk Agent
2. Select the **Publish** button (top toolbar)
3. Review the confirmation dialog
4. Select **Publish** to confirm
5. Wait for the "Agent published" notification
6. Note: This only publishes the agent, not to channels yet

### Step 4: Add Teams and M365 Copilot Channel (~5 minutes)
1. Select **Channels** in the top navigation
2. Review available channels
3. Select **Teams and Microsoft 365**
4. Select **Add channel**
5. Wait for the green notification confirming channel added

### Step 5: Add Agent to Teams (~5 minutes)
1. Select **See agent in Teams**
2. A new browser tab opens with the agent details
3. Select **Add** to add the agent to your Teams
4. Wait for the success confirmation
5. Select **Open** to launch the agent in Teams
6. Test the agent with a sample question

### Step 6: Make Available Organization-Wide (~5 minutes)
1. Return to Copilot Studio (Teams/M365 panel still open)
2. Select **Edit details** to customize:
   - Icon and background color
   - Short and long descriptions
   - Teams settings (teams, group chats)
   - Developer information
3. Select **Availability options**
4. Review options:
   - **Share Link**: Direct link for shared users
   - **Show to teammates**: Built with Power Platform section
   - **Show to everyone**: Organization catalog (requires admin)
5. Select **Show to everyone in my org**
6. Select **Submit for admin approval**

### Step 7: Admin Approval Process (~5 minutes)
1. Understand admin workflow:
   - Admin goes to Teams Admin Center
   - Finds the agent in Apps section
   - Reviews and approves the submission
   - Publishes to organization
2. After approval:
   - Agent appears in "Built by your org" section
   - Can be auto-installed via setup policies
   - Can be pinned to left rail for easy access

## Duration
~30 minutes

## Next Steps
Proceed to [Lab 12: Understanding Licensing](../Lab%2012/index.md)

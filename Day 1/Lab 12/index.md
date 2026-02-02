# Lab 12: Publish Your Agent to Teams and M365 Copilot

## Lab Title
Publish Your Agent - Deploy to Teams and Microsoft 365 Copilot

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand why publishing is important for agent updates
2. Publish your agent to make all changes live
3. Add the Microsoft Teams and M365 Copilot channel
4. Deploy the agent to your Teams for testing
5. Make the agent available organization-wide

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Fully tested Sales Agent (from Labs 6-11)
- Microsoft Teams access
- Permissions to publish agents in your environment

## Step-by-Step Guide

### Step 1: Understanding Publishing (~10 minutes)
1. Learn why publishing matters:
   - Makes latest updates available to users
   - New tools, topics, and knowledge become accessible
   - All configured channels receive updates
2. Understand the publish process:
   - Only unpublished changes need to be published
   - Publishes all topics, tools, knowledge, and instructions
   - Takes a few moments to process
3. Review: Always publish after making significant changes

### Step 2: Publish Your Sales Agent (~5 minutes)
1. Open your Sales Agent
2. Select the **Publish** button in the top toolbar
3. Review the confirmation dialog showing what will be published
4. Select **Publish** to confirm
5. Wait for the "Agent published successfully" notification
6. Note: This publishes the agent itself, not necessarily to channels

### Step 3: Explore Available Channels (~10 minutes)
1. Review deployment options:
   - **Teams & M365 Copilot**: Teams chats, meetings, Microsoft 365 Copilot
   - **Demo website**: Built-in Copilot Studio test website
   - **Custom website**: Embed in your own site
   - **Web chat**: Public web-based chat interface
   - **SharePoint**: Site-based assistance
   - **Azure Bot Service**: Integration with Slack, Telegram, etc.
2. Understand channel licensing:
   - Different channels may require different licenses
   - Internal Teams use may have different requirements than external web channels

### Step 4: Add Teams and M365 Copilot Channel (~10 minutes)
1. From the agent Overview, select **Channels** tab (or look for Channels option)
2. Browse available channels
3. Select **Teams and Microsoft 365**
4. Select **+ Add channel**
5. Configure channel settings (team restrictions if needed)
6. Wait for confirmation that the channel was added
7. The agent is now available in Teams and Microsoft 365 Copilot

### Step 5: Deploy Agent to Microsoft Teams (~10 minutes)
1. In the Teams & M365 Copilot channel settings, select **See agent in Teams** or similar option
2. A new browser tab opens showing the agent
3. Select **Add** to install the agent to your personal Teams instance
4. Confirm the installation in the popup
5. Open Teams and locate your agent (should appear in Apps or chat)
6. Test the agent with a sample conversation:
   - `I want to create a meeting recap`
   - Verify all topics work in Teams environment
   - Confirm documents are created in your OneDrive
   - Check that emails draft correctly in Outlook

### Step 6: Organization-Wide Distribution (~10 minutes)
1. Return to Copilot Studio, select your agent
2. Go to the Teams & M365 Copilot channel settings
3. Look for **Edit details** or **Availability options**
4. Customize your agent:
   - Icon and background color
   - Short description (one-liner)
   - Long description (detailed)
   - Developer name
   - Support contact information
5. Review availability/sharing options:
   - **Share Link**: Direct URL for specific users
   - **Show in Teams**: Visible in Teams app catalog
   - **Show to everyone**: Organization-wide availability
6. For organization-wide, you may need to submit for admin approval

### Step 7: Understanding Distribution Models (~5 minutes)
1. Review deployment scenarios:
   - **Personal/Team**: Share the agent link with specific people
   - **Department**: Submit for admin approval for department-wide access
   - **Organization**: Full organization-wide availability (requires admin approval)
2. Each model serves different use cases:
   - Pilot testing (team-level)
   - Department rollout (admin approval)
   - Company-wide adoption (organization-wide)

### Step 8: Post-Deployment Monitoring (~5 minutes)
1. After publishing:
   - Monitor agent usage
   - Collect user feedback
   - Track error rates in analytics
   - Identify improvement opportunities
2. Plan for ongoing updates:
   - Add new topics based on user requests
   - Enhance prompts based on feedback
   - Expand knowledge sources as needed
   - Update agent description with new capabilities
   - Remaining capacity
4. Set up alerts for approaching limits

## Duration
~15 minutes (intel only, no fieldwork required)

## Next Steps
Congratulations on completing Day 1!
Proceed to [Lab 13: Get Started with the Hiring Agent](../../Day%202/Lab%2013/index.md)

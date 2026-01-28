# Lab 10: Add Event Triggers for Autonomous Agents

## Lab Title
Add Event Triggers - Enable Autonomous Agent Capabilities

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand what event triggers are and how they work
2. Differentiate between event triggers and topic triggers
3. Create event triggers for SharePoint item creation
4. Build autonomous workflows with email acknowledgments
5. Test and validate trigger-based automation

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Contoso Helpdesk Agent (from Labs 6-9)
- SharePoint site with IT support tickets list
- Generative orchestration enabled on agent
- Email access for testing

## Step-by-Step Guide

### Step 1: Understanding Event Triggers (~10 minutes)
1. Learn what event triggers are:
   - Enable autonomous agent behavior
   - Fire from external system events
   - No user message required
2. Review trigger types available:
   - SharePoint/OneDrive file or item created
   - Planner task completed/assigned
   - Microsoft Forms response submitted
   - Email received
   - Recurrence/schedule
3. Understand key characteristics:
   - Payload-driven execution
   - Requires generative orchestration
   - Uses maker's authentication

### Step 2: Event vs Topic Triggers (~5 minutes)
1. Compare the two trigger types:
   - Event Triggers: External system events, autonomous behavior, maker authentication
   - Topic Triggers: User input/phrases, conversational responses, user authentication option

### Step 3: Enable Generative Orchestration (~2 minutes)
1. Open your IT Help Desk agent
2. Navigate to **Overview** tab
3. Under Orchestration, toggle **Generative orchestration** to **On**
4. Save changes

### Step 4: Create SharePoint Trigger (~10 minutes)
1. Navigate to **Triggers** section in Overview
2. Select **+ Add trigger**
3. Search for and select **When an item is created** (SharePoint)
4. Configure trigger:
   - Name: `New Support Ticket Created in SharePoint`
   - Wait for connections to configure
5. Configure parameters:
   - Site Address: Your Contoso IT site
   - List Name: Tickets
6. Add instructions for the trigger
7. Select **Create trigger**

### Step 5: Edit Trigger in Power Automate (~10 minutes)
1. Select **...** on the trigger → **Edit in Power Automate**
2. Select the **Sends a prompt to the specified copilot** node
3. Update the Body/message with an expression containing ticket details
4. Select **Publish**

### Step 6: Create Email Acknowledgment Tool (~5 minutes)
1. Navigate to **Tools** tab
2. Select **+ Add a tool** → **Connector**
3. Search for **Send an email (V2)**
4. Configure:
   - Name: `Acknowledge SharePoint ticket`
   - Description: Sends email acknowledgement that ticket was received
5. Configure input parameters
6. Save the tool

### Step 7: Test the Trigger (~8 minutes)
1. In Overview, select **Test Trigger** icon
2. Open SharePoint in a new tab
3. Navigate to your Tickets list
4. Create a new item:
   - Title: `Unable to connect to VPN`
   - Description: `Cannot connect after recent update`
   - Priority: `Normal`
5. Save the item
6. Return to Copilot Studio
7. Monitor the Test trigger panel (use Refresh)
8. Select **Start testing** when trigger appears
9. Verify:
   - Agent received the trigger payload
   - Called the Acknowledge tool
   - Email was sent to submitter
10. Review Activity Map for execution details

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 11: Publish Your Agent](../Lab%2011/index.md)

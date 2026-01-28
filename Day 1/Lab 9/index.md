# Lab 9: Add an Agent Flow for Automation

## Lab Title
Add an Agent Flow for Automation - Multi-Step Workflows

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand what agent flows are and when to use them
2. Create agent flows for deterministic multi-step processes
3. Use expressions for dynamic data handling
4. Integrate SharePoint and email actions
5. Connect agent flows to topics for end-to-end automation

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Contoso Helpdesk Agent with Request device topic (from Lab 8)
- SharePoint Devices list (from Course Setup)
- Email access for testing notifications

## Step-by-Step Guide

### Step 1: Understanding Agent Flows (~10 minutes)
1. Learn what agent flows are:
   - Structured, step-by-step workflows
   - Deterministic execution (same path every time)
   - Built directly in Copilot Studio
2. Compare with Power Automate cloud flows:
   - Agent Flows: Built for agents, in Copilot Studio, no separate license
   - Cloud Flows: General-purpose, Power Automate portal, requires license

### Step 2: Key Features of Agent Flows (~5 minutes)
1. **Natural language authoring**: Describe in plain English
2. **AI actions**: Read documents, summarize, recommend
3. **Generative actions**: Adapt in real-time
4. **Integration actions**: 1400+ connectors
5. **Human in the loop**: Approval steps

### Step 3: Understanding Expressions (~5 minutes)
1. Review expression categories:
   - **Text**: `concat()`, `toLower()`, `substring()`, `trim()`
   - **Math**: `add()`, `sub()`, `mul()`, `div()`
   - **Date**: `utcNow()`, `addDays()`, `formatDateTime()`
   - **Logical**: `if()`, `equals()`, `and()`, `or()`

### Step 4: Create the Device Request Agent Flow (~15 minutes)
1. Open the Request device topic
2. Add a node → **Add a tool** → **New Agent flow**
3. Configure the trigger with inputs:
   - `DeviceSharePointId` (Text): The SharePoint item ID
   - `User` (Text): The user's name
   - `AdditionalComments` (Text): Optional user comments

4. Add **Get item** SharePoint action:
   - Site Address: Your Contoso IT site
   - List Name: Devices
   - Id: Use `DeviceSharePointId` input

5. Add **Send an email (V2)** action:
   - To: Manager's email address
   - Subject: Device Request from [User]
   - Body: Include device details and comments

6. Configure **Respond to agent** action:
   - Return the device model name

7. **Save** and **Publish** the agent flow

### Step 5: Connect Flow to Topic (~5 minutes)
1. Return to the Request device topic
2. Add the agent flow as a tool
3. Map input variables:
   - `DeviceSharePointId` ← Adaptive card selection
   - `User` ← System user context
   - `AdditionalComments` ← Optional comments field
4. Add a confirmation message using the returned model
5. Redirect to End of Conversation topic

### Step 6: Test the Complete Automation (~5 minutes)
1. Open the Test pane
2. Enter: `I need a laptop`
3. Answer `Yes` to request a device
4. Select a device from the adaptive card
5. Optionally add comments
6. Submit the request
7. Verify:
   - Email is received with device details
   - Confirmation message displays the model
8. Review the Activity Map for flow execution

## Duration
~30 minutes

## Next Steps
Proceed to [Lab 10: Add Event Triggers for Autonomous Agents](../Lab%2010/index.md)

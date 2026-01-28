# Lab 7: Add New Topic with Trigger and Nodes

## Lab Title
Add New Topic with Trigger and Nodes - Structured Conversations

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand what topics are and their purpose in agents
2. Create custom topics with trigger descriptions
3. Use conversation nodes (messages, questions, conditions)
4. Connect to SharePoint using connectors
5. Apply Power Fx for dynamic filtering and logic

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Contoso Helpdesk Agent from Lab 6
- SharePoint site with Devices list (from Course Setup)
- Basic understanding of conversation design

## Step-by-Step Guide

### Step 1: Understanding Topics (~10 minutes)
1. Review what a topic is:
   - Structured conversation for specific user questions/tasks
   - Mini-conversation with defined flow
2. Understand topic purposes:
   - **Informational**: Answer "What is...?", "When will...?"
   - **Task completion**: Help with "I want to...", "How do I...?"
   - **Troubleshooting**: Solve "Something isn't working..."
3. Learn topic types:
   - **System topics**: Built-in handlers for common events
   - **Custom topics**: Your specific business logic

### Step 2: Understanding Conversation Nodes (~10 minutes)
1. Review node types:
   - **Send a message**: Display text to user
   - **Ask a question**: Collect user input
   - **Ask with adaptive card**: Rich interactive cards
   - **Add a condition**: Branch logic
   - **Variable management**: Store/clear data
   - **Topic management**: Redirect to other topics
   - **Add a tool**: Use connectors, flows, prompts
   - **Generative answers**: AI-generated responses
   - **HTTP request**: External API calls

### Step 3: Introduction to Power Fx (~5 minutes)
1. Understand Power Fx basics (low-code formula language)
2. Review common operations:
   - Set variables: `Set(userName, "Adele Vance")`
   - Conditions: `If(score > 80, "Pass", "Fail")`
   - Data formatting: `Text(DateValue, "dd/mm/yyyy")`
3. Understand Power Fx use in topics

### Step 4: Create the Available Devices Topic (~15 minutes)
1. Open your Contoso Helpdesk Agent
2. Navigate to **Topics** tab
3. Select **+ Add a topic** → **From blank**
4. Configure the topic:
   - Name: `Available devices`
   - Trigger description: This topic helps users find devices that are available from our SharePoint Devices list.

### Step 5: Define Input and Output Variables (~5 minutes)
1. Open **Topic details**
2. Create input variable:
   - Name: `VarDeviceType`
   - Type: Text
   - Description: The type of device to search for
3. Create output variable:
   - Name: `VarAvailableDevices`
   - Type: Table
   - Description: List of available devices

### Step 6: Add SharePoint Connector Tool (~10 minutes)
1. Add a node → **Add a tool**
2. Search for **SharePoint** connector
3. Select **Get items** action
4. Configure the connection:
   - Site Address: Your Contoso IT site
   - List Name: Devices
5. Add a filter query using Power Fx
6. Map output to `VarAvailableDevices`

### Step 7: Update Agent Instructions (~5 minutes)
1. Navigate to agent Overview
2. Edit Instructions
3. Add guidance to use the topic
4. Save changes

### Step 8: Test the Topic (~5 minutes)
1. Open the Test pane
2. Enter: `I need a laptop`
3. Verify the agent:
   - Triggers the Available devices topic
   - Queries SharePoint for available laptops
   - Returns matching devices
4. Review the Activity Map

## Duration
~60 minutes

## Next Steps
Proceed to [Lab 8: Enhance User Interactions with Adaptive Cards](../Lab%208/index.md)

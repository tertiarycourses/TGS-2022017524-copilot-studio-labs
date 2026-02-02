# Lab 10: Create Conditional Logic and Multi-Path Conversations

## Lab Title
Add Conditional Logic and Branching - Multi-Path Conversations

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand conditional logic in agent topics
2. Create topics with branching paths (Yes/No conditions)
3. Build different conversation flows based on user responses
4. Implement complex decision logic with multiple conditions
5. Create a complete proposal generation workflow with conditions

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Sales Agent with Price Calculator topic (from Lab 9)
- Basic understanding of if/then logic
- Email access for testing

## Step-by-Step Guide

### Step 1: Understanding Conditions in Topics (~10 minutes)
1. Learn what conditions allow:
   - Branch conversations based on user responses
   - Route to different paths based on data
   - Validate inputs before processing
2. Understand condition types:
   - **Simple conditions**: If/else branching
   - **Complex conditions**: Multiple criteria with AND/OR logic
3. Review use cases:
   - Ask user if they want to create a document (Yes/No)
   - Check if a quantity is valid before processing
   - Route based on customer tier or department

### Step 2: Create a Topic with Conditions (~15 minutes)
1. In your Sales Agent, add a new topic
2. Select **Topics** → **Add a topic** → **From blank**
3. Configure:
   - **Name**: `Proposal Generator`
   - **Description**: `This topic helps users create and customize sales proposals`
4. Add a question node:
   - **Message**: `Do you want to create a new proposal?`
   - Configure response as **Yes/No** (multiple choice options)
   - Variable name: `proposalDecision`

### Step 3: Add a Condition Node (~10 minutes)
1. Select **+** to add a node
2. Select **Add a condition**
3. Configure the condition:
   - **Left side**: `proposalDecision`
   - **Operator**: `equals`
   - **Right side**: `Yes`
4. This creates two branches: "If Yes" and "If No"

### Step 4: Build the "Yes" Branch (~10 minutes)
1. Under the "If Yes" path, add nodes:
2. Add **Ask a question** node:
   - **Message**: `What client name should appear on the proposal?`
   - Variable: `clientName`
3. Add another question:
   - **Message**: `What is the project scope or service description?`
   - Variable: `projectScope`
4. Add a prompt tool:
   - **Name**: `Generate proposal text`
   - **Instructions**: Create a professional sales proposal including client name, project scope, pricing, and next steps
   - **Inputs**: clientName, projectScope
   - **Output**: proposalText
5. Add a **Send a message** to display the proposal
6. Add a tool to create a document from the proposal

### Step 5: Build the "No" Branch (~5 minutes)
1. Under the "If No" path, add a message node:
   - **Message**: `No problem! If you need help with anything else, just let me know.`
2. This ends that branch gracefully

### Step 6: Test Conditional Logic (~10 minutes)
1. Refresh the test pane
2. Trigger the Proposal Generator topic
3. Test Path 1 - Answer "Yes":
   - Provide client name and project scope
   - Verify proposal is generated
   - Verify document is created
4. Test Path 2 - Answer "No":
   - Verify the appropriate message displays
5. Review Activity Map to see the branching logic

### Step 7: Understanding Topic Chaining (~5 minutes)
1. Learn how to connect topics:
   - Topics can reference/trigger other topics
   - Create a workflow across multiple topics
   - Build complex multi-step processes
2. In a topic, you can add nodes that:
   - Transfer to another topic
   - Return to the main topic flow

### Step 8: Review All Your Topics (~5 minutes)
1. Navigate to Topics view
2. Verify all created topics:
   - Meeting Recap
   - Price Calculator
   - Proposal Generator
3. Note how each topic:
   - Has a clear trigger description
   - Contains specific conversation flow
   - Uses prompts and flows as tools
4. Understand these are the building blocks of your agent

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 11: Publish Your Agent](../Lab%2011/index.md)

# Lab 8: Enhance User Interactions with Adaptive Cards

## Lab Title
Enhance User Interactions with Adaptive Cards

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand what Adaptive Cards are and their benefits
2. Use the Adaptive Card Designer to build cards
3. Create interactive forms for data collection
4. Use Power Fx formulas for dynamic card content
5. Redirect between topics based on user responses

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Contoso Helpdesk Agent with Available devices topic (from Lab 7)
- SharePoint Devices list (from Course Setup)
- Basic understanding of JSON (helpful but not required)

## Step-by-Step Guide

### Step 1: Understanding Adaptive Cards (~10 minutes)
1. Learn what Adaptive Cards are:
   - Interactive, visually rich UI elements
   - Structured JSON objects
   - Render consistently across platforms (Teams, Outlook, agents)
2. Review key benefits:
   - Makes conversations interactive
   - Consistent styling across hosts
   - Easy JSON-based building
   - Collect and use data in flows
   - Better user experience

### Step 2: Explore the Adaptive Card Designer (~5 minutes)
1. Review the designer components:
   - **Card Elements**: TextBlock, Image, FactSet, Inputs, Actions
   - **Card Viewer**: Real-time preview
   - **Card Structure**: Hierarchy view
   - **Element Properties**: Configuration panel
   - **Payload Editor**: Raw JSON code

### Step 3: Common Use Cases (~5 minutes)
1. Forms and data collection (leave requests, feedback)
2. Displaying dynamic information (order summaries, status)
3. Interactive choices (product selection, confirmations)
4. Triggering actions (submit buttons, view details)

### Step 4: Create the Request Device Topic (~10 minutes)
1. Navigate to **Topics** tab
2. Select **+ Add a topic** → **From blank**
3. Configure:
   - Name: `Request device`
   - Trigger description: This topic helps users request a device when they answer yes to requesting one.
4. Define input variable:
   - Name: `VarDevices`
   - Type: Table
   - Source: From Available devices topic

### Step 5: Add an Adaptive Card Node (~10 minutes)
1. Add a node → **Ask with adaptive card**
2. Design the card to display:
   - Title: "Available Devices"
   - Device list with selection options
   - Optional comments field
   - Submit button
3. Configure output variables:
   - `VarSelectedDevice`: User's device selection
   - `VarComments`: Optional user comments

### Step 6: Use Power Fx for Dynamic Content (~10 minutes)
1. Switch from JSON to **Formula** mode
2. Use Power Fx to loop through devices:
   - `ForAll(Global.VarDevices.value, {title: ThisRecord.Model, value: Text(ThisRecord.ID)})`
3. This dynamically populates the card with available devices
4. Save the adaptive card configuration

### Step 7: Update Agent Instructions (~5 minutes)
1. Navigate to agent Overview
2. Edit Instructions
3. Add: If the user answers yes to requesting a device, trigger [Request device].
4. Save changes

### Step 8: Test the Complete Flow (~5 minutes)
1. Open the Test pane
2. Enter: `I need a laptop`
3. The agent should query available laptops and ask if user wants to request one
4. Answer `Yes`
5. Verify the adaptive card displays with device options
6. Select a device and submit
7. Review the Activity Map for topic flow

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 9: Add an Agent Flow for Automation](../Lab%209/index.md)

# Lab 16: Add Event Triggers for Autonomous Agents

## Lab Title
Add Event Triggers - Autonomous Email Processing

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand how event triggers enable autonomous agent behavior
2. Differentiate between interactive and autonomous agents
3. Create event triggers for email-based resume processing
4. Build agent flows that post adaptive cards to Teams
5. Pass data between event triggers and agent flows

## Prerequisites
- Copilot Studio license and environment access
- Completed Lab 13 and Lab 15 with Hiring Agent ready
- Microsoft Teams access for testing notifications
- Understanding of event triggers from Lab 10

## Step-by-Step Guide

### Step 1: Understanding Event Triggers (~10 minutes)
1. Review event trigger characteristics:
   - Autonomous activation from external events
   - Payload-driven execution
   - Requires generative orchestration
   - Uses maker's authentication
2. Compare Interactive vs Autonomous agents:
   | Dimension | Interactive | Autonomous |
   |-----------|------------|------------|
   | Start | User triggers topic | External event |
   | Use | Q&A, guided workflows | Proactive automation |
   | Trigger | By agent/Phrases | Event connectors |
   | Example | "What's our policy?" | New email → process |

### Step 2: Plan the Automation (~5 minutes)
1. Define the use case:
   - **As an** HR Recruiter
   - **I want to** be notified when resume emails arrive
   - **So that I** can review automatically uploaded applications
2. Review the two-part approach:
   - Event trigger for email arrival
   - Agent flow for Teams notification

### Step 3: Create Email Event Trigger (~15 minutes)
1. Open the Hiring Agent
2. Navigate to **Overview** → **Triggers and Channels**
3. Select **+ Add**
4. Select **When a new email arrives (V3)** → **Next**
5. Configure trigger:
   - Name: `When a new email arrives from an applicant`
   - Verify connection references (green checks)
6. Set input properties:
   - Include Attachments: **Yes**
   - Subject Filter: `Application`
   - Only with Attachments: **Yes**
7. Select **Create trigger**

### Step 4: Edit Trigger in Power Automate (~10 minutes)
1. Select **...** on trigger → **Edit in Power Automate**
2. Add condition to check PDF attachment:
   - `contentType` equals `application/pdf`
3. Add Dataverse actions:
   - Extract file content
   - Create Resume record
   - Create Candidate record
4. Configure prompt to agent:
   - Pass Resume ID and Candidate ID
   - Include processing instructions
5. Publish the flow

### Step 5: Create Teams Notification Agent Flow (~10 minutes)
1. Navigate to Application Intake Agent
2. Add new Agent Flow for Teams notification
3. Configure inputs:
   - `ResumeId`: Resume record identifier
   - `CandidateId`: Candidate record identifier
   - `CandidateName`: Name for display
4. Add **Post adaptive card to Teams channel** action:
   - Select target channel
   - Design card with:
     - Candidate name
     - Resume link
     - Quick action buttons
5. Save and publish the flow

### Step 6: Update Child Agent Instructions (~5 minutes)
1. Edit Application Intake Agent instructions
2. Add:
   - When processing resumes from email triggers, use the Teams Notification flow to alert the HR recruitment team. Include the candidate name and link to the Dataverse record.
3. Save changes

### Step 7: Test the Autonomous Flow (~10 minutes)
1. Open Test pane → **Test Trigger**
2. Send a test email:
   - Subject contains "Application"
   - Attach a PDF resume
   - Send to the monitored inbox
3. Wait for trigger activation (may take a few minutes)
4. Verify:
   - Trigger fires correctly
   - Resume is uploaded to Dataverse
   - Adaptive card appears in Teams channel
   - Card contains correct candidate information
5. Review Activity Map for complete flow

### Step 8: Monitor and Troubleshoot (~5 minutes)
1. Check Power Automate flow runs
2. Review Copilot Studio activity logs
3. Verify Dataverse records created correctly
4. Confirm Teams notifications delivered

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 17: Understanding Agent Models](../Lab%2017/index.md)

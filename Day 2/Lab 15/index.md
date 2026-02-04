# Lab 15: Build an Autonomous Hiring Agent with Event Triggers

## Lab Title
Create an Event-Driven Hiring Agent for Resume Processing

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand how event triggers enable autonomous hiring agent behavior
2. Create an autonomous hiring agent that processes incoming resumes
3. Implement email event triggers for resume receipt
4. Configure the agent to extract candidate information and rank qualifications
5. Set up automated Teams notifications for the recruitment team
6. Test end-to-end hiring agent workflows

## Prerequisites
- Copilot Studio license and environment access
- Completed prior labs with foundational agent knowledge
- Microsoft Teams access for testing notifications
- Email account configured for resume delivery
- OneDrive or SharePoint configured for resume storage

## Step-by-Step Guide

### Step 1: Understand the Hiring Agent Use Case (~10 minutes)
1. Review the autonomous hiring agent scenario:
   - **As an** HR Recruiter
   - **I want to** automatically process resume emails
   - **So that I** can quickly identify qualified candidates and rank them
2. Key capabilities of the hiring agent:
   - Autonomous activation when resumes arrive
   - Automatic resume content extraction and analysis
   - Candidate qualification matching against job requirements
   - Ranking candidates by experience and skills
   - Posting notifications to the recruitment team in Teams
3. Agent workflows vs. event triggers:
   - Event triggers activate the agent autonomously
   - Agent uses generative AI to extract insights
   - Child flows handle Teams notifications and Dataverse updates

### Step 2: Create the Hiring Agent (~10 minutes)
1. In Copilot Studio, create a new agent:
   - Name: `Hiring Agent`
   - Description: `Autonomous hiring agent that processes resumes and ranks candidates`
2. Configure the agent with instructions:
   ```
   You are an expert HR recruitment assistant. Your role is to:
   1. Extract candidate information from resumes (name, email, phone, experience, skills)
   2. Analyze qualifications against job requirements
   3. Rank candidates based on experience level, skill match, and education
   4. Provide hiring recommendations with reasoning
   5. Format candidate information for HR team review
   
   Always be objective in your assessment and highlight both strengths and gaps.
   ```
   ![alt text](./Assets/image.png)
3. Keep the agent in **Generative** mode for autonomous decision-making

### Step 3: Create Event Trigger for Resume Emails (~15 minutes)
1. Open the Hiring Agent
2. Navigate to **Overview** → **Triggers and Channels**
3. Select **+ Add**
4. Select **When a new email arrives (V3)** → **Next**
![alt text](./Assets/image-1.png)
5. Configure the trigger:
   - **Connection**: Select your email account
   - **Name**: `When a new resume email arrives`
   - **Folder**: Inbox
   - **Include Attachments**: **Yes**
   - **Subject Filter**: `resume` OR `application` OR `cv`
      [Note: Cannot use all in the same field; use one keyword or create multiple triggers if needed]
   - **Only with Attachments**: **Yes**
6. Select **Create trigger**
![alt text](./Assets/image-2.png)

### Step 4: Extract and Process Resume Data (~15 minutes)
1. The trigger captures the email, now add processing logic
2. In the Power Automate flow (edit trigger):
   - Add action: **Extract text from word documents** or **Extract PDF content**
   - Attach the resume file
3. Add action: **Save file to OneDrive**
   - Folder: `/resumes`
   - File Name: `{CandidateName}_{Timestamp}.pdf`
4. Add action: **Compose** to create a JSON resume metadata object:
   ```json
   {
     "candidateName": "[Extract from email]",
     "email": "[From sender]",
     "submissionDate": "@{utcNow()}",
     "resumeFile": "[OneDrive file path]",
     "extractedText": "[Extracted resume content]"
   }
   ```
5. Save the flow without publishing yet (we'll enhance it next)

## Duration
~60 minutes

## Next Steps
Proceed to [Lab 16: Advanced Hiring Agent Features](../Lab%2016/index.md)

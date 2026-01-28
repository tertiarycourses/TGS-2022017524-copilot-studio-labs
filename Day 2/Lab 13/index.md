# Lab 13: Get Started with the Hiring Agent

## Lab Title
Get Started with the Hiring Agent - Building a Recruitment System

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand the hiring automation scenario and its business value
2. Import and configure the Operative solution with Dataverse tables
3. Import sample data for job roles and evaluation criteria
4. Create the central Hiring Agent for orchestration
5. Understand the foundation for multi-agent hiring workflows

## Prerequisites
- Copilot Studio license
- Access to a Microsoft Power Platform environment
- Administrative permissions to create solutions and agents
- Completed Day 1 labs (recommended)

## Step-by-Step Guide

### Step 1: Understanding the Scenario (~10 minutes)
1. Review the hiring automation use case:
   - System of agents working together
   - Resume review and job matching
   - Interview preparation
   - Candidate evaluation
2. Understand the business value:
   - Automatic resume processing
   - Job role suggestions
   - Interview guide generation
   - Fair and compliant practices
3. Review the agent architecture:
   - Central **Hiring Agent** (orchestrator)
   - **Application Intake Agent** (resume processing)
   - **Interview Prep Agent** (interview materials)

### Step 2: Import the Operative Solution (~10 minutes)
1. Navigate to [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
2. Select **...** → **Solutions**
3. Select **Import Solution**
4. Download the prepared solution from the course materials
5. Select **Browse** and choose the downloaded solution
6. Select **Next** → **Import**
7. Wait for "imported successfully" message
8. Select the **Operative** solution to review components:
   - Candidate table
   - Evaluation Criteria table
   - Hiring Hub app
   - Job Application table
   - Job Role table
   - Resume table
9. Select **Publish all customizations**

### Step 3: Import Job Role Sample Data (~10 minutes)
1. Download the `job-roles.csv` file from course materials
2. Open the Hiring Hub Model-Driven App:
   - Select the app checkbox
   - Select **Play**
3. Navigate to **Job Roles** in left navigation
4. Select **More** (three dots) → **Import from Excel** → **Import from CSV**
5. Select the downloaded `job-roles.csv` file
6. Select **Next** → **Review Mapping**
7. Verify mapping is correct
8. Select **Finish Import** → **Done**
9. Refresh and verify data imported successfully

### Step 4: Import Evaluation Criteria Sample Data (~10 minutes)
1. Download the `evaluation-criteria.csv` file
2. Navigate to **Evaluation Criteria** in left navigation
3. Select **More** → **Import from Excel** → **Import from CSV**
4. Select the downloaded file
5. Select **Next** → **Review Mapping**
6. For Job Role field, select the magnifying glass icon
7. Ensure **Job Title** is selected
8. Select **OK** → **Finish Import** → **Done**
9. Refresh and verify data imported successfully

### Step 5: Create the Hiring Agent (~10 minutes)
1. Navigate to [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
2. Ensure you're in the same environment as the imported solution
3. Select **Agents** → **New Agent**
4. Select **Configure**
5. Enter agent details:
   - Name: `Hiring Agent`
   - Description: `Central orchestrator for all hiring activities`
6. Select **...** next to Create → **Update advanced settings**
7. Set Solution to `Operative`
8. Select **Update** → **Create**
9. Wait for agent creation to complete

### Step 6: Verify Setup (~5 minutes)
1. Confirm the Hiring Agent appears in your agents list
2. Verify it's associated with the Operative solution
3. Review the agent configuration
4. Prepare for adding instructions in the next lab

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 14: Authoring Agent Instructions](../Lab%2014/index.md)

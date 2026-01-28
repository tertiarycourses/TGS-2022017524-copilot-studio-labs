# Lab 6: Create a Custom Agent Using Natural Language

## Lab Title
Create a Custom Agent Using Natural Language with Copilot

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand what custom agents are vs. pre-built agents
2. Use natural language prompts to define agent behavior
3. Connect multiple knowledge sources (websites, SharePoint, documents)
4. Ground your agent with enterprise data
5. Test responses with citations from knowledge sources

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Copilot Studio environment with maker permissions
- SharePoint site with IT documentation (from Course Setup)
- Sample IT guidance documents

## Step-by-Step Guide

### Step 1: Understanding Custom Agents (~5 minutes)
1. Review what custom agents are:
   - You define the purpose
   - You ground with your own data
   - Full control over personality, knowledge, and actions
2. Understand the difference from pre-built agents
3. Explore use cases for custom agents

### Step 2: Understanding Prompts (~5 minutes)
1. Learn what a prompt is (instruction to AI)
2. Review characteristics of effective prompts:
   - Specific and clear
   - User-focused
   - Example-rich when possible
3. Understand generative orchestration for dynamic routing

### Step 3: Explore Knowledge Source Types (~5 minutes)
1. Review the six knowledge source categories:
   - Public websites (Searched via Bing)
   - Uploaded documents (Stored in Dataverse)
   - SharePoint (Direct integration)
   - Dataverse tables (Structured data)
   - Real-time connectors (Salesforce, ServiceNow, etc.)
   - Azure AI Search (Advanced search)

### Step 4: Create the IT Helpdesk Agent (~15 minutes)
1. Navigate to [copilotstudio.microsoft.com](https://copilotstudio.microsoft.com)
2. Select **+ Create** → **New agent**
3. Use the conversational creation experience to describe your agent
4. Follow prompts to refine capabilities
5. Name your agent: `Contoso Helpdesk Agent`
6. Select **Create**

### Step 5: Add Knowledge Sources (~15 minutes)
1. Navigate to the **Knowledge** section
2. Add a **Public website**:
   - URL: `https://support.microsoft.com`
3. Add a **SharePoint** connection:
   - Connect to your Contoso IT SharePoint site
4. Upload a **Document**:
   - Upload your IT guidance document

### Step 6: Test Your Agent (~10 minutes)
1. Open the **Test** pane
2. Try various IT support queries:
   - `How do I reset my password?`
   - `My computer is running slowly, what should I do?`
   - `How do I connect to the VPN?`
3. Observe how the agent searches multiple knowledge sources
4. Review the Activity Map for source tracking

### Step 7: Refine and Iterate (~5 minutes)
1. Identify gaps in responses
2. Add additional knowledge sources if needed
3. Adjust agent instructions for better responses
4. Test edge cases and error handling

## Duration
~60 minutes

## Next Steps
Proceed to [Lab 7: Add New Topic with Trigger and Nodes](../Lab%207/index.md)

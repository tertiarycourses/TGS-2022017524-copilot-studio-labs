# Lab 15: Multi-Agent Systems

## Lab Title
Multi-Agent Systems - Building Orchestrated Agent Networks

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand when to use child agents vs. connected agents
2. Design multi-agent architectures that scale
3. Create child agents for focused, specialized tasks
4. Establish communication patterns between agents
5. Build the Application Intake Agent and Interview Prep Agent

## Prerequisites
- Copilot Studio license and environment access
- Completed Lab 13 with Hiring Agent ready
- Understanding of agent instructions from Lab 14

## Step-by-Step Guide

### Step 1: Understanding Multi-Agent Systems (~10 minutes)
1. Learn why multi-agent systems matter:
   - **Scalability**: Independent development and maintenance
   - **Specialization**: Each agent excels at specific tasks
   - **Flexibility**: Mix, match, and reuse agents
   - **Maintainability**: Changes don't cascade
2. Review the hiring workflow example:
   - Resume intake → document parsing
   - Scoring → candidate evaluation
   - Interview prep → deep reasoning
   - Communication → empathetic responses

### Step 2: Child Agents vs Connected Agents (~10 minutes)
1. **Child Agents**:
   - Lightweight specialists within parent agent
   - Share parent's tools and knowledge
   - No separate publishing required
   - Single team manages the solution
   - Example: IT helpdesk with password/hardware/software specialists

2. **Connected Agents**:
   - Full-fledged independent agents
   - Own topics and conversation flows
   - Must be published before use
   - Multiple teams with independent ALM
   - Example: Customer service connecting to billing, support, returns

### Step 3: Multi-Agent Architecture Patterns (~5 minutes)
1. **Hub and Spoke**: Orchestrator coordinates specialists
2. **Pipeline**: Sequential processing (intake → screening → interview)
3. **Collaborative**: Simultaneous work on different aspects

### Step 4: Set Preferred Solution (~3 minutes)
1. Navigate to **...** → **Solutions**
2. Find the Operative solution
3. Select **...** → **Set preferred solution**
4. Select **Apply**

### Step 5: Configure Hiring Agent Instructions (~5 minutes)
1. Open the Hiring Agent
2. Select **Edit** in Instructions section
3. Add instructions:
   - You are the central orchestrator for the hiring process. You coordinate activities, provide summaries, and delegate work to specialized agents.
4. Save changes

### Step 6: Configure Agent Settings (~5 minutes)
1. Select **Settings** (top right)
2. Verify these settings:
   - Generative AI orchestration: **Yes**
   - Deep Reasoning: **Off**
   - Let other agents connect: **On**
   - Content Moderation: **Moderate**
   - Collect user reactions: **On**
   - Use general knowledge: **Off**
   - Use web information: **Off**
   - File uploads: **On**
   - Code Interpreter: **Off**
3. Save and close Settings

### Step 7: Add Application Intake Child Agent (~10 minutes)
1. Navigate to **Agents** tab within Hiring Agent
2. Select **Add** → **New child agent**
3. Configure:
   - Name: `Application Intake Agent`
   - When used: **The agent chooses** - Based on description
   - Description: `Processes incoming resumes and stores candidates in the system`
4. Expand **Advanced**, set Priority: `10000`
5. Disable **Web Search**
6. Save the child agent

### Step 8: Configure Resume Upload Agent Flow (~15 minutes)
1. Locate **Tools** section in Application Intake Agent
2. Select **+ Add** → **+ New tool** → **Agent flow**
3. Configure trigger inputs:
   - File: Resume - The Resume PDF file
   - Text: Message - Cover letter style message (< 2000 chars)
   - Text: UserEmail - Email address of resume origin

4. Add flow actions:
   - Parse resume content
   - Extract candidate information
   - Create Dataverse records
   - Return confirmation

5. Save and publish the agent flow

### Step 9: Test Multi-Agent System (~5 minutes)
1. Open the Test pane
2. Upload a sample resume
3. Verify:
   - Hiring Agent delegates to Application Intake
   - Resume is processed correctly
   - Candidate record is created
4. Review Activity Map for agent collaboration

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 16: Add Event Triggers (Autonomous)](../Lab%2016/index.md)

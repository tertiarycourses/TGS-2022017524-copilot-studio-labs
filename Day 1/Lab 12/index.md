# Lab 12: Understanding Licensing

## Lab Title
Understanding Licensing - Copilot Credits and Capacity Planning

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand how Copilot Credits work as the usage currency
2. Compare licensing options (PAYGO, capacity packs, pre-purchase)
3. Identify when M365 Copilot licenses apply vs. Copilot Studio credits
4. Plan capacity for production agent deployments
5. Monitor usage in the Power Platform admin center

## Prerequisites
- Basic understanding of Microsoft licensing concepts
- Access to Power Platform admin center (for monitoring)
- No hands-on configuration required (informational lab)

## Step-by-Step Guide

### Step 1: Understanding Copilot Credits (~5 minutes)
1. Learn what Copilot Credits are:
   - Currency for measuring Copilot Studio usage
   - Replaces the older "message" concept
   - Maps to actual work done by agent
2. Credits are consumed when agent:
   - Looks up information
   - Answers questions
   - Runs workflows and actions
   - Calls tools and connectors

### Step 2: Licensing Options (~5 minutes)
1. **Pay-As-You-Go (PAYGO)**:
   - No upfront commitment
   - $0.01 per Copilot Credit
   - Billed through Azure
   - Ideal for development and variable usage

2. **Copilot Studio License (Capacity Pack)**:
   - 25,000 credits per pack/month
   - Pooled at tenant level
   - Credits don't roll over
   - Best for predictable usage

3. **Copilot Credit Pre-Purchase**:
   - Annual prepaid option
   - Copilot Credit Commit Units (CCCUs)
   - 1 CCCU = 100 Credits
   - Cost advantage at scale

### Step 3: User Licenses (~3 minutes)
1. **Copilot Studio Tenant License**:
   - Enables Copilot Studio in your tenant
   - Capacity pack or PAYGO required
2. **Copilot Studio User License** ($0):
   - Required for makers who create/manage agents
   - Assigned to individual users

### Step 4: M365 Copilot License Coverage (~5 minutes)
1. What M365 Copilot licenses include:
   - Copilot in Word, Teams, Outlook, Excel
   - Ability to create and use agents in hosted channels
2. When Copilot Studio Credits still apply:
   - Running agent flows
   - Using connectors/external services
   - Publishing outside internal M365 experiences
   - Topics with actions beyond simple responses

3. **Rule of thumb**:
   - Internal M365 + basic responses → M365 Copilot license
   - Automation, integrations, external → Copilot Studio credits

### Step 5: Capacity Planning Tips (~5 minutes)
1. **Before launching**:
   - Use the Agent Usage Estimator (aka.ms/copilotstudioestimator)
   - Disable unused tools to reduce costs
   - Mix capacity packs + PAYGO for flexibility
   - Assign user licenses to all builders
   - Monitor in Power Platform admin center

2. **Estimation process**:
   - Estimate expected monthly interactions
   - Multiply by average credits per interaction
   - Add buffer for growth
   - Compare to capacity pack vs. PAYGO costs

### Step 6: Real-World Licensing Scenarios (~5 minutes)
1. Review common scenarios:
   - Internal Teams Q&A agent: User license (basic); credits for actions
   - Agent with Power Automate: Uses Copilot Credits
   - Autonomous agents: Uses Copilot Credits
   - External web deployment: Uses Copilot Credits
   - Maker building agents: Copilot Studio User License

### Step 7: Monitoring Usage (~2 minutes)
1. Navigate to Power Platform admin center
2. Go to Billing → License → Copilot Studio
3. Review:
   - Credit consumption trends
   - Per-agent usage breakdown
   - Remaining capacity
4. Set up alerts for approaching limits

## Duration
~15 minutes (intel only, no fieldwork required)

## Next Steps
Congratulations on completing Day 1!
Proceed to [Lab 13: Get Started with the Hiring Agent](../../Day%202/Lab%2013/index.md)

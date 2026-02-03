# Lab 17: Understanding Agent Models

## Lab Title
Understanding Agent Models - Selecting the Right AI Brain

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand different AI models available in Copilot Studio
2. Compare model capabilities, performance, and cost characteristics
3. Switch your agent's model and test the impact
4. Evaluate differences in output quality and structure
5. Make informed model selection decisions for your scenarios

## Prerequisites
- Copilot Studio license and environment access
- Hiring Agent from previous labs
- Understanding of agent fundamentals
- Sample resume data in the system

## Step-by-Step Guide

### Step 1: Understanding Agent Models (~10 minutes)
1. Learn what the agent model is:
   - Underlying generative AI engine
   - Determines how agent thinks and responds
   - Impacts speed, quality, and cost
2. Understand why model selection matters:
   - Quick replies vs. deep analysis
   - User satisfaction optimization
   - Cost management

### Step 2: Model Categories (~10 minutes)
1. Review model use categories:
   | Category | Description | Best For |
   |----------|-------------|----------|
   | **Deep** | Multi-step reasoning | Complex analytics, policy analysis |
   | **Auto** | Dynamic routing | Mixed workloads, helpdesk |
   | **General** | Speed and cost | FAQ, drafting, translation |

2. Understand model availability tags:
   - **Experimental**: Not for production
   - **Preview**: Eventually GA, limited testing
   - **No tag**: Generally available
   - **Default**: Best performing GA model
   - **Retired**: Available for 1 month after retirement

### Step 3: Available OpenAI Models (~10 minutes)
1. Review current model options:
   | Model | Category | Status | Strengths |
   |-------|----------|--------|-----------|
   | GPT-4o | General | Retired | Fast, versatile, multimodal |
   | GPT-4.1 | General | Default | High accuracy, complex analysis |
   | GPT-5 Chat | General | Preview | Human-like dialogue |
   | GPT-5 Auto | Auto | General | Multi-step automation |
   | GPT-5 Reasoning | Deep | Preview | Advanced analytical tasks |
   | GPT-5.1 Chat | General | Experimental | Latest conversational |
   | GPT-5.1 Reasoning | Deep | Experimental | Maximum precision |

2. Note: Experimental/preview models may have instability

### Step 4: Available Anthropic Models (~5 minutes)
1. Review external model options:
   | Model | Status | Strengths |
   |-------|--------|-----------|
   | Claude Sonnet 4.5 | Experimental | Coding, agent workflows |
   | Claude Opus 4.1 | Experimental | Intensive analysis |

2. Note: External models subject to Anthropic terms

### Step 5: Change Agent Model (~5 minutes)
1. Open the Hiring Agent
2. Navigate to **Overview** tab
3. Select the model **chevron** icon
4. Browse available models:
   - OpenAI models
   - Anthropic models (if enabled)
5. Select **GPT-5.1 Chat** (experimental)
6. Wait for confirmation message

### Step 6: Compare Model Outputs (~10 minutes)
1. Start a new test session with GPT-4.1 (default)
2. Test question 1:
   - `Summarize resume RXXXXX`
3. Note the response format and detail level

4. Test question 2:
   - `Can you provide suggestions of questions to ask in an interview for the Power Platform developer role (Job role number J1004) based on its associated evaluation criteria? Also provide expected answers.`
5. Note the structure and depth

6. Switch to GPT-5.1 Chat
7. Repeat the same questions
8. Compare:
   - Response length (concise vs. detailed)
   - Organization (headers, bullets)
   - Formatting style
   - Answer depth and specificity

### Step 7: Admin Controls (~5 minutes)
1. Understand admin settings that affect model availability:
   | Setting | Effect | Location |
   |---------|--------|----------|
   | Allow Anthropic | Enable external models | M365 Admin |
   | Allow Preview | Enable experimental models | PP Admin |
   | Move Data | Required for experimental | PP Admin |

2. Note: Contact your admin if models aren't available

### Step 8: Best Practices (~5 minutes)
1. Model selection guidelines:
   - **General tasks**: Use GPT-4.1 (default)
   - **Complex reasoning**: Consider Deep models
   - **Cost-sensitive**: Stick with General models
   - **Testing new features**: Try Preview models
2. Always test model changes before production
3. Monitor performance and user satisfaction
4. Plan for model retirement transitions

## Duration
~45 minutes

## Course Complete!
Congratulations on completing all 17 labs! You now have the skills to:
- Build conversational and autonomous agents
- Design multi-agent systems
- Implement event-driven automation
- Select optimal AI models for your scenarios

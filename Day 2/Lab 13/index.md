# Lab 14: Authoring Agent Instructions

## Lab Title
Authoring Agent Instructions - Shaping Agent Behavior

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand why instructions are critical for agent behavior
2. Write clear, effective instructions with proper structure
3. Apply best practices for tool and topic descriptions
4. Structure instructions for multi-agent scenarios
5. Test and refine instructions for optimal performance

## Prerequisites
- Copilot Studio license and environment access
- Completed Lab 13 with Hiring Agent created
- Understanding of agent fundamentals from Day 1

## Step-by-Step Guide

### Step 1: Understanding Why Instructions Matter (~5 minutes)
1. Review what instructions control:
   - **Role definition**: Agent's persona and expertise
   - **Response style**: Tone, format, detail level
   - **Tool selection**: When to call specific tools
   - **Boundaries**: Guardrails and restrictions
   - **Edge cases**: Handling ambiguous situations
2. Understand: Instructions must align with available capabilities

### Step 2: Essential Components of Instructions (~10 minutes)
1. **Role Definition**:
   - Example: You are the central orchestrator for the hiring process. You coordinate activities, provide summaries, and delegate work to specialized agents.

2. **Tool Selection Guidance**:
   - Example: When a user uploads a resume, use the /Resume Upload tool to process it.

3. **Input Hints**:
   - Example: Extract a cover letter style message from the context. The message must be less than 2000 characters.

4. **Response Formatting**:
   - Example: Always format job application summaries with Candidate Name, Applied Position, Key Qualifications, and Recommendation.

5. **Behavioral Constraints**:
   - Example: Never contact candidates directly. All candidate communication must go through the HR team.

### Step 3: Description Best Practices (~5 minutes)
1. Review Do's and Don'ts:
   - Do: Straightforward language, active voice, concise (1-2 sentences)
   - Don't: Technical jargon, passive voice, lengthy paragraphs
2. Good examples:
   - `Processes incoming resumes and stores candidates`
   - `Generates interview questions based on job requirements`
3. Poor examples:
   - `This tool can answer questions`
   - `Handles stuff related to hiring`

### Step 4: Structural Framework (~5 minutes)
1. Follow this instruction pattern:
   - Overview of agent role
   - Sequential process steps
   - Inter-agent collaboration points
   - Safety/compliance requirements
   - Feedback and escalation mechanisms

2. Review example structure for Application Intake Agent:
   - Role: Process incoming resumes and create candidate records
   - Process: Upload Resume → Post-Upload confirmation
   - Constraints: Only process PDF files, never modify existing records without instruction

### Step 5: Testing Your Instructions (~5 minutes)
1. Open the **Test pane** in Copilot Studio
2. Try various scenarios:
   - Happy path (normal usage)
   - Edge cases (unusual inputs)
   - Error conditions (failures)
3. Check the **Activity Map** for tool/agent invocation
4. Refine instructions based on unexpected behavior
5. Repeat until behavior is consistent

### Step 6: Troubleshooting Tips (~3 minutes)
1. If agent doesn't call expected tool:
   - Check tool descriptions for overlap
   - Make descriptions more specific
   - Test with explicit trigger phrases
2. If responses are inconsistent:
   - Add more explicit formatting rules
   - Include examples in instructions
   - Clarify decision criteria

## Duration
~30 minutes (intel only, no fieldwork required)

## Next Steps
Proceed to [Lab 15: Multi-Agent Systems](../Lab%2015/index.md)

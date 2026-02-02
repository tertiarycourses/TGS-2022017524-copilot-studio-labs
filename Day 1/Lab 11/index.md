# Lab 11: Test Your Agent Thoroughly Before Publishing

## Lab Title
Test Your Agent - Comprehensive Testing and Validation

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand comprehensive testing strategies for agents
2. Test all topics and conversation flows
3. Use the Activity Map for debugging and understanding flow execution
4. Test branching logic and edge cases
5. Identify and fix issues before publishing

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Fully configured Sales Agent (from Labs 6-10)
- Sample transcript files and test data
- Understanding of all agent topics and flows

## Step-by-Step Guide

### Step 1: Understanding Agent Testing (~5 minutes)
1. Learn what the test pane provides:
   - Real-time testing of agent behavior
   - Activity Map showing execution flow
   - Variable inspection and debugging
   - Ability to test all topics and paths
2. Understand when to test:
   - After creating each topic
   - After adding/modifying tools
   - Before publishing to users
   - When troubleshooting unexpected behavior

### Step 2: Comprehensive Testing Strategy (~10 minutes)
1. Test all happy paths:
   - Follow the intended conversation flow
   - Verify correct outputs are generated
   - Check that documents/emails are created
2. Test edge cases:
   - Empty inputs
   - Long responses
   - Special characters
   - Boundary conditions
3. Test branching logic:
   - All condition paths
   - Different Yes/No responses
   - Topic transitions

### Step 3: Test Meeting Recap Topic (~10 minutes)
1. In the test pane, enter: `I want to create a meeting recap`
2. Upload the provided sample transcript file
3. Verify:
   - Agent generates the recap correctly
   - Recap contains key points, decisions, and action items
   - Word document is created in your OneDrive
   - Email draft is created in Outlook
   - All information is accurate
4. Review Activity Map:
   - Click the nodes to see variable values
   - Verify the prompt was called correctly
   - Check the flow executed successfully

### Step 4: Test Price Calculator Topic (~10 minutes)
1. Enter: `I need to calculate a price`
2. Request a quote for: `10 Surface Laptops at quantity 15`
3. Verify:
   - Agent correctly calculates unit price
   - Applies the 10% discount for quantity > 10
   - Shows total price and payment terms
4. Try variations:
   - Different quantities (test discount logic)
   - Different products (test prompt flexibility)
   - Complex requests (test AI understanding)

### Step 5: Test Proposal Generator Topic (~10 minutes)
1. Enter: `I want to create a proposal`
2. Answer "Yes" to the proposal decision
3. Provide client name: `Acme Corporation`
4. Provide scope: `IT infrastructure upgrade including cloud migration`
5. Verify:
   - Agent generates professional proposal text
   - Includes all required sections
   - Document is created with proper formatting
6. Test the "No" path:
   - Re-trigger the topic
   - Answer "No" to see the alternative response

### Step 6: Test Conversation Scenarios (~10 minutes)
1. Create realistic multi-turn conversations:
   - `First, create a meeting recap. Then, let's calculate pricing for the client.`
   - Verify the agent can handle multiple requests
   - Check that variables don't bleed between topics
2. Test natural language variations:
   - `I need to recap a sales meeting` (instead of exact trigger)
   - `What's the price for this product?` (variation of Price Calculator)
   - Verify the agent correctly identifies topics
3. Document any misunderstandings for refinement

### Step 7: Activity Map and Debugging (~5 minutes)
1. After each test, review the Activity Map:
   - Identify which topic was triggered
   - See the order of node execution
   - Click nodes to view variable values
   - Check for any errors or warnings
2. If something goes wrong:
   - Review variable names and types
   - Check prompt instructions are clear
   - Verify Power Automate flow published successfully
   - Check file paths and SharePoint connections

### Step 8: Performance and Iteration (~10 minutes)
1. Identify areas for improvement:
   - Prompts that aren't clear enough
   - Topics that should be split into multiple topics
   - Tools that should handle more cases
2. Make refinements:
   - Edit prompt instructions for better results
   - Adjust trigger descriptions
   - Add more example scenarios in prompts
3. Re-test after each change to verify improvements

## Duration
~30 minutes

## Next Steps
Proceed to [Lab 12: Understanding Licensing](../Lab%2012/index.md)

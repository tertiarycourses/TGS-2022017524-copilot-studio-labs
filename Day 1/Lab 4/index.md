# Lab 4: Creating a Solution for Your Agent

## Lab Title
Creating a Solution for Your Agent - Power Platform ALM

## Lab Objectives
By the end of this lab, you will be able to:
1. Understand what Power Platform solutions are and their purpose
2. Explain the benefits of using solutions for agent development
3. Create a solution publisher with proper naming conventions
4. Create a custom solution for your agent
5. Understand the solution lifecycle from development to production

## Prerequisites
- Microsoft 365 account with Copilot Studio access
- Power Platform environment with appropriate permissions
- One of these security roles: Environment Maker, System Customizer, or System Administrator
- Developer environment (created in Course Setup)

## Step-by-Step Guide

### Step 1: Understanding Solutions (~10 minutes)
1. Review what a Power Platform solution is:
   - Container for apps, agents, tables, flows
   - Essential for Application Lifecycle Management (ALM)
2. Understand solution types:
   - **Unmanaged**: Used during development, freely editable
   - **Managed**: Used for deployment, locked down
3. Explore the Solution Explorer in Copilot Studio

### Step 2: Benefits of Using Solutions (~5 minutes)
1. **Organized development**: Keep agent components in one place
2. **Safe deployment**: Export as managed for production
3. **Version control**: Create patches, updates, or upgrades
4. **Dependency management**: Track component relationships
5. **Team collaboration**: Work together effectively

### Step 3: Understanding Solution Publishers (~5 minutes)
1. Learn what a publisher is (label/brand for ownership)
2. Understand the prefix system (e.g., `cts_` for Contoso Solutions)
3. Review why prefixes matter for identification, conflicts, and ALM tracking

### Step 4: Create a Solution Publisher (~10 minutes)
1. Navigate to Copilot Studio
2. Select **...** → **Solutions**
3. Select **+ New solution**
4. Select **+ New publisher**
5. Configure publisher properties:
   - Display name: `Contoso Solutions`
   - Name: `ContosoSolutions`
   - Description: `Copilot Studio Agent Academy`
   - Prefix: `cts`
   - Choice value prefix: Round to nearest thousand (e.g., 77000)
6. Optionally add contact information
7. Save the publisher

### Step 5: Create a Custom Solution (~10 minutes)
1. Return to the New solution pane
2. Select your new publisher
3. Configure solution details:
   - Display name: `Contoso Helpdesk Agent`
   - Name: `ContosoHelpdeskAgent`
   - Version: `1.0.0.0` (default for new solutions)
4. Check **Set as your preferred solution**
5. Review More options
6. Select **Create**
7. Verify solution appears in Solution Explorer

### Step 6: Understand the Solution Lifecycle (~5 minutes)
1. **Create** in Development environment
2. **Add Components** (agents, tables, flows)
3. **Export** as Managed solution
4. **Import** to Test environment
5. **Import** to Production environment
6. **Apply** Patches, Updates, or Upgrades
7. Repeat the cycle!

## Duration
~45 minutes

## Next Steps
Proceed to [Lab 5: Using a Pre-Built Agent](../Lab%205/index.md)

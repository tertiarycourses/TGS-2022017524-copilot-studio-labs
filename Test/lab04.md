# 🚨 Lab 04: Creating a Solution for Your Agent

## 🕵️‍♂️ CODENAME: `OPERATION CTRL-ALT-PACKAGE`

> **⏱️ Operation Time Window:** `~45 minutes`

## 🎯 Mission Brief

Agent Maker, welcome to your next tactical operation. In this mission, you’ll learn to assemble a Solution - the official deployment vehicle for your IT Helpdesk Agent built with Microsoft Copilot Studio. Think of this as creating a digital briefcase that holds your agent and it's artifacts.

Every agent needs a well-structured home. That’s what a Power Platform solution provides - order, portability, and readiness for production.

Let’s pack up.

## 🔎 Objectives

In this mission, you’ll learn:

1. Understanding what Power Platform solutions are and their role in agent development
1. Learning the benefits of using solutions for organizing and deploying agents
1. Exploring solution publishers and their importance in component management
1. Understanding the Power Platform solution lifecycle from development to production
1. Creating your own solution publisher and custom solution for your IT Helpdesk Agent

##
## 🧪 Lab 04: Create a new Solution

We're now going to learn

- How to create a Solution publisher
- How to create a Solution

We're going to stick with the example from earlier, where we're going to create a solution in the dedicated Copilot Studio environment to build our IT helpdesk agent in.

Let's begin!

### Prerequisites

#### Security role

In Copilot Studio, what you _can do_ in the solution explorer depends on your user security role.
If you don’t have permission to manage solutions in the Power Apps admin center, you won’t be able to do those tasks in Copilot Studio either.

To make sure everything works smoothly, check that you have the right security roles and permissions. Or if you don't manage environments in your organization, ask your IT administrator (or the equivalent) team who manages your tenant/environments.

The following are the security roles that enables users to create a solution in their environment.

| Security role | Description |
| ---------- | ---------- |
| Environment Maker | Provides the necessary permissions to create, customize, and manage resources within a specific environment, including solutions |
| System Customizer | Wider permissions than Environment Maker, including the ability to customize the environment and manage security roles |
| System Administrator | Highest level of permissions and can manage all aspects of the environment, including creating and assigning security roles |

#### Developer environment

Make sure you switch to your dedicated developer environment, refer to [Lab 00 - Course Setup - Step 3: Create new developer](../Day1/lab00.md#step-3-create-new-developer-environment).

1. On the upper right, select the **Cog wheel** icon and switch from the default environment to your environment, for example **Adele Vance's environment**.

    ![Developer environment](./Images/4.0_03_DeveloperEnvironment.png)

### 4.1 Create a Solution publisher

1. Using the same Copilot Studio environment used in the previous lab, select the **ellipsis icon (. . .)** on the left hand side menu in Copilot Studio. Select **Solutions** under the **Explore** header.

    ![Solutions](./Images/4.1_01_Solutions.png)

1. The **Solution Explorer** in Copilot Studio will load. Select **+ New solution**

    ![Solutions](./Images/4.1_02_NewSolution.png)

1. The **New solution** pane will appear where we can define the details of our solution. First, we need to create a new publisher. Select **+ New publisher**.

    ![Solutions](./Images/4.1_03_NewPublisher.png)  

1. The **Properties** tab of the **New publisher** pane will appear with required and non-required fields to be populated in the **Properties** tab. This is where we can outline the details of the publisher which will be used as the label or brand that identifies who created or owns the solution.

    |Property|Description|Required|
    |----------|----------|:----------:|
    |Display name|Display name for the publisher|Yes|
    |Name|The unique name and schema name for the publisher|Yes|
    |Description|Outlines the purpose of the solution|No|
    |Prefix|Publisher prefix which will be applied to newly created components|Yes|
    |Choice value prefix|Generates a number based on the publisher prefix. This number is used when you add options to choices and provides an indicator of which solution was used to add the option.|Yes|

    Copy and paste the following as the **Display name**,

    ```text
    Contoso Solutions
    ```

    Copy and paste the following as the **Name**,

    ```text
    ContosoSolutions
    ```

    Copy and paste the following as the **Description**,

    ```text
    Copilot Studio Agent Academy
    ```

    Copy and paste the following for the **Prefix**,

    ```text
    cts
    ```

    By default, the **Choice value** prefix will display an integer value. Update this integer value to the nearest thousand. For example, in my screenshot below, it was initially `77074`. Update this from `77074` to `77000`.

    ![Solutions](./Images/4.1_04_PublisherProperties.png)  

1. If you want to provide the contact details for the Solution, select the **Contact** tab and populate the following columns displayed.

    ![Solutions](./Images/4.1_05_Contact.png)

1. Select the **Properties** tab and select **Save** to create the Publisher.

    ![Solutions](./Images/4.1_06_SavePublisher.png)

1. The New publisher pane will close and you'll be brought back to the **New solution** pane with the newly created Publisher selected.

    ![Solutions](./Images/4.1_07_PublisherSelected.png)  

High five, you've now created a Solution Publisher! 🙌🏻 We'll next learn how to create a new custom solution.

### 4.2 Create a new Solution

1. Now that we've created our solutions, we can now complete the rest of the form in the **New solution** pane.

    Copy and paste the following as the **Display name**,

    ```text
    Contoso Helpdesk Agent
    ```

    Copy and paste the following as the **Name**,

    ```text
    ContosoHelpdeskAgent
    ```

    Since we're creating a new solution, the [**Version** number](https://learn.microsoft.com/power-apps/maker/data-platform/update-solutions#understanding-version-numbers-for-updates/?WT.mc_id=power-172615-ebenitez) by default will be `1.0.0.0`.

    Tick the **Set as your preferred solution** checkbox.

    ![Solutions](./Images/4.2_01_SolutionDetails_.png)  

1. Expand the **More options** to see additional details that can be provided in a solution.

    ![Solutions](./Images/4.2_02_MoreOptions.png)

1. You'll see the following,

    - **Installed on** - the date of when the Solution was installed.

    - **Configuration page** - developers set up an HTML web resource to help users interact with their app, agent or tool where it'll appear as a web page in the Information section with instructions or buttons. It’s mostly used by companies or developers who build and share solutions with others.

    - **Description** - describes the solution or a high level description of the configuration page.

    We'll leave these blank for this lab.

    Select **Create**.

    ![Solutions](./Images/4.2_03_Create.png)

1. The solution for Contoso Helpdesk Agent has now been created. There will be zero components until we create an agent in Copilot Studio.

    Select the **back arrow** icon to return to the Solution Explorer.

    ![Solutions](./Images/4.2_04_SolutionCreated.png)

1. Notice how the Contoso Helpdesk Agent now displays as the **Current preferred solution** since we ticked the **Set as your preferred solution** checkbox earlier.

    ![Solutions](./Images/4.2_05_CurrentPreferredSolutionSelected.png)

## ✅ Mission Complete

Congratulations! 👏🏻 You've created a Publisher and used it in your newly created Solution to build your agent in!

Well done, Agent Maker. A tidy digital footprint is the first step toward operability at scale. Now you have the tools and the mindset for sustainable, enterprise-ready agent development.

This is the end of **Lab 04 - Creating a Solution**, select the link below to move to the next lab. Your solution created in this lab will be used in the next lab.

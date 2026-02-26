# Lab 07: Develop an AI agent with VS Code extension

### Estimated Duration: 30 Minutes

## Overview

In this exercise, you'll use the Microsoft Foundry VS Code extension to create an agent that can use Model Context Protocol (MCP) server tools to access external data sources and APIs. The agent will be able to retrieve up-to-date information and interact with various services through MCP tools.

> **Note:** Some of the technologies used in this exercise are in preview or in active development. You may experience some unexpected behavior, warnings, or errors.

## Task 1: Install the Microsoft Foundry VS Code extension

Let's start by installing and setting up the VS Code extension.

1. Open Visual Studio Code.

1. In Visual Studio Code, select **Extensions (1)** from the left pane, search for **Microsoft Foundry (2)**, choose the **Microsoft Foundry (3)** extension by Microsoft, and then click **Install (4)**.

   ![](./Media/lab7-s1.png)

1. After installation is complete, verify the extension appears in the primary navigation bar on the left side of Visual Studio Code.

   ![](./Media/lab7-s2.png)

   > **Tip:** If you already have the extension installed, make sure the version is at least **v0.16.0** to follow along with the instructions in this exercise.

## Task 2: Sign in to Azure and create a project

Now you'll connect to your Azure resources and create a new AI Foundry project.

1. In the VS Code sidebar, select the **Microsoft Foundry (1)** extension icon.

1. In the Resources view, choose **Create Project (2)**, and when prompted, select **Sign in to Azure (3)** to authenticate.

   ![](./Media/lab7-s4.png)

1. In the **Azure Resources wants to sign in using Microsoft** dialog, select **Allow**.

   ![](./Media/lab7-s5.png)

1. On the **Sign in** page, provide the credentials below:
 
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject>
    
     ![](./Media/lab7-s6.png)

   - **Password:** <inject key="AzureAdUserPassword"></inject>
    
     ![](./Media/lab7-s7.png)

1. On the **Sign in to all apps, websites, and services on this device?** page, select **Yes**.

   ![](./Media/lab7-s8.png)

1. On the **Account added to this device** page, select **Done**.

   ![](./Media/lab7-s9.png)

1. In the **Choose a resource group** dialog, select **AI-3026-RG07** from the list.

   ![](./Media/lab7-s10.png)

1. In the **Enter project name** dialog, enter **Myproject<inject key="DeploymentID"></inject>**, and then press **Enter** to confirm.

   ![](./Media/lab7-s11.png)

1. Wait for the project deployment to complete. A popup will appear with the message "Project deployed successfully."

## Task 3: Deploy a model

You'll need a deployed model to use with your agent.

1. In the **RESOURCES** pane, expand **Models**, and then select the **+** icon to add a new model deployment.

   ![](./Media/lab7-s12.png)

   > **Tip:** You can also access the Model Catalog pressing **F1** and running the command **Microsoft Foundry: Open Model Catalog**.

1. In the Model Catalog, scroll down, search for **gpt-4.1 (1)** in the search bar, and then select **Deploy (2)** under **OpenAI GPT-4.1**.

   ![](./Media/lab7-s13.png)

1. Configure the deployment settings:
   
   - **Deployment name:** Enter a name like **gpt-4.1-deployment (1)**
   - **Deployment type:** Select **Global Standard** (or **Standard** if Global Standard is not available) **(2)**
   - **Model version:** Leave as default
   - **Tokens per minute:** Leave as default

1. Select **Deploy in Microsoft Foundry (3)** in the bottom-left corner.

   ![](./Media/lab7-s14.png)

1. In the confirmation dialog, select **Deploy** to deploy the model.

1. Wait for the deployment to complete. Your deployed model will appear under the **Models** section in the Resources view.

   ![](./Media/lab7-s15.png)

## Task 4: Create an AI agent with the designer view

Now you'll create an AI agent using the visual designer interface. Rather than writing code, you'll configure the agent's instructions, settings, and tools through the user interface.

1. In the Microsoft Foundry extension view, find the **Resources** section.

1. Expand the **Classic (1)** subsection.

1. Select the **+** (plus) **(2)** icon next to the **Classic Agents** subsection to create a new AI Agent.

    ![](./Media/lab7-s16.png)

1. Choose a location to save your agent files if prompted.

1. A **New Agent** tab will open to an "Agent Preferences" editor, along with a `.yaml` configuration file.

   ![](./Media/lab7-s17.png)

### Task 4.1 Configure your agent in the designer

1. In the agent preferences, configure the following fields:
   - **Name:** Enter a descriptive name for your agent **data-research-agent (1)**
   - **Model:** Select your GPT-4.1-deployment **(2)**from the dropdown
   - **Instructions:** Enter system instructions such as **(3)**:
     ```
     You are an AI agent that helps users research information from various sources. Use the available tools to access up-to-date information and provide comprehensive responses based on external data sources.
     ```

      ![](./Media/lab7-s18.png)

1. Save the configuration by selecting **File (1) > Save (2)** from the VS Code menu bar.

   ![](./Media/lab7-s19.png)

## Task 5: Add an MCP Server tool to your agent

You'll now add a Model Context Protocol (MCP) server tool that allows your agent to access external APIs and data sources.

1. In the **TOOL** section of the designer, select the **Add tool (1)** button in the top-right corner.

1. From the dropdown menu, choose **MCP Server (2)**.

   ![](./Media/lab7-s20.png)

1. Configure the MCP Server tool with the following information:
   - **Server URL:** Enter the URL of an MCP server `https://gitmcp.io/Azure/azure-rest-api-specs` **(1)**
   - **Server Label:** Enter a unique identifier **github_docs_server (2)**

1. Leave the **Allowed tools** dropdown empty to allow all tools from the MCP server.

1. Select the **Create tool (3)** button to add the tool to your agent.

   ![](./Media/lab7-s21.png)

## Task 6: Deploy your agent to Microsoft Foundry

1. In the agent designer view, select the **Create Agent on Microsoft Foundry** button in the bottom-left corner.

   ![](./Media/lab7-s22.png)

1. Wait for the deployment to complete.

1. In the VS Code navbar, refresh **(1)** the **Resources** view.  **data-research-agent (2)** should now appear under the **Classic Agents** subsection.

   ![](./Media/lab7-s23.png)

## Test your agent in the playground

1. Right-click on **data-research-agent (1)** in the **Classic Agents** subsection.

1. Select **Open Playground (2)** from the context menu.

   ![](./Media/lab7-s24.png)

1. The Agents Playground will open in a new tab within VS Code.

1. In the **Agent Playground**, enter the following prompt in the chat box **(1)**, and then select **Send (2)**:

   ```output
   Can you help me find documentation about Azure Container Apps and provide an example of how to create one?
   ```

   ![](./Media/lab7-s25.png)

1. Send the message and observe the authentication and approval prompts for the MCP Server tool:
    
    - In the **MCP Tools Authentication Setup** dialog, select **No Authentication**.

      ![](./Media/lab7-s26.png)
    
    - In the **MCP Tools Approval Preference** dialog, select **Always approve**.

      ![](./Media/lab7-s27.png)

1. Review the agent's response and note how it uses the MCP server tool to retrieve external information.

1. Check the **Agent Annotations** section to see the sources of information used by the agent.

## Generate sample code for your agent

1. Right-click on your deployed agent and select **Open Code File**, or select the **Open Code File** button in the Agent Preferences page.

1. Choose your preferred SDK from the dropdown (Python, .NET, JavaScript, or Java).

1. Select your preferred programming language.

1. Choose your preferred authentication method.

1. Review the generated sample code that demonstrates how to interact with your agent programmatically.

You can use this code as a starting point for building applications that leverage your AI agent.

## View conversation history and threads

1. In the **Azure Resources** view, expand the **Threads** subsection to see conversations created during your agent interactions.

1. Select a thread to view the **Thread Details** page, which shows:
   - Individual messages in the conversation
   - Run information and execution details
   - Agent responses and tool usage

1. Select **View run info** to see detailed JSON information about each run.

## Summary

In this exercise, you used the Foundry VS Code extension to create an AI agent with MCP server tools. The agent can access external data sources and APIs through the Model Context Protocol, enabling it to provide up-to-date information and interact with various services. You also learned how to test the agent in the playground and generate sample code for programmatic interaction.

## Clean up

When you've finished exploring the Foundry VS Code extension, you should clean up the resources to avoid incurring unnecessary Azure costs.

### Delete your agents

1. In the Foundry portal, select **Agents** from the navigation menu.

1. Select your agent and then select the **Delete** button.

### Delete your models

1. In VS Code, refresh the **Azure Resources** view.

1. Expand the **Models** subsection.

1. Right-click on your deployed model and select **Delete**.

### Delete other resources

1. Open the [Azure portal](https://portal.azure.com).

1. Navigate to the resource group containing your AI Foundry resources.

1. Select **Delete resource group** and confirm the deletion.
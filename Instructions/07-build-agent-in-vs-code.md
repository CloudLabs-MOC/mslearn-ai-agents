# Lab 03: Develop an AI agent with VS Code extension

### Estimated Duration: 30 Minutes

## Overview

In this lab, you will use the Microsoft Foundry VS Code extension to build an AI agent that integrates with a Model Context Protocol (MCP) server to access external APIs and up-to-date documentation. You will configure the agent’s instructions, model, and MCP tool to enable it to retrieve trusted information from external sources such as Azure REST API specifications. Finally, you will deploy and test the agent in the playground and generate sample code to interact with it programmatically.

> **Note:** Some of the technologies used in this exercise are in preview or in active development. You may experience some unexpected behavior, warnings, or errors.

## Task 1: Install the Microsoft Foundry VS Code extension

In this task, you’ll install and verify the Microsoft Foundry VS Code extension to enable creating and managing AI agents directly within Visual Studio Code.

1. Open Visual Studio Code.

1. In Visual Studio Code, select **Extensions (1)** from the left pane, search for **Microsoft Foundry (2)**, choose the **Microsoft Foundry (3)** extension by Microsoft, and then click **Install (4)**.

   ![](./Media/lab7-s1.png)

1. After installation is complete, verify the extension appears in the primary navigation bar on the left side of Visual Studio Code.

   ![](./Media/lab7-s2.png)

   > **Tip:** If you already have the extension installed, make sure the version is at least **v0.16.0** to follow along with the instructions in this exercise.

## Task 2: Sign in to Azure and Select a project

In this task, you’ll sign in to Azure through the Microsoft Foundry VS Code extension and select your existing Foundry project to use as the default resource for building and managing your AI agent.

1. In the VS Code sidebar, select the **Microsoft Foundry (1)** extension icon.

1. In the Resources view, choose **Set Default Project (2)**, and when prompted, select **Sign in to Azure (3)** to authenticate.

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
   
1. In the **Pick a project** dialog, select your **myprojects-<inject key="DeploymentID"></inject>** project from the list.

   ![](./Media/lab3-02.png)

1. In the **Microsoft Foundry** extension, verify that your **myprojects-<inject key="DeploymentID"></inject>** project is listed under **RESOURCES**.

   ![](./Media/lab3-03.png)

## Task 3: Create an AI agent with the designer view

In this task, you’ll use the Microsoft Foundry VS Code extension designer to create a new AI agent and open its configuration for editing through the visual interface.

1. In the Microsoft Foundry extension view, find the **Resources** section.

1. Expand the **Classic (1)** subsection.

1. Select the **+** (plus) **(2)** icon next to the **Classic Agents** subsection to create a new AI Agent.

    ![](./Media/lab3-04.png)

1. Choose a location to save your agent files if prompted.

1. A **New Agent** tab will open to an "Agent Preferences" editor, along with a `.yaml` configuration file.

   ![](./Media/lab7-s17.png)

### Task 3.1 Configure your agent in the designer

In this task, you’ll configure the agent’s name, select the gpt-4.1 model, and define instructions that guide it to retrieve and analyze information from external sources.

1. In the agent preferences, configure the following fields:
   - **Name:** Enter a descriptive name for your agent **data-research-agent (1)**
   
   - **Model:** Select your **gpt-4.1 (2)** from the dropdown
   
   - **Instructions:** Enter system instructions such as **(3):**
     ```
     You are an AI agent that helps users research information from various sources. Use the available tools to access up-to-date information and provide comprehensive responses based on external data sources.
     ```

      ![](./Media/lab3-05.png)

### Task 3.3 Add an MCP Server tool to your agent

In this task, you’ll add an MCP Server tool to your agent to enable it to access external APIs and retrieve up-to-date data from external sources.

1. In the **TOOL** section of the designer, select the **Add tool (1)** button in the top-right corner.

1. From the dropdown menu, choose **MCP Server (2)**.

   ![](./Media/lab7-s20.png)

1. Configure the MCP Server tool with the following information:
   
   - **Server URL:** Enter the URL of an MCP server `https://gitmcp.io/Azure/azure-rest-api-specs` **(1)**
   
   - **Server Label:** Enter a unique identifier **github_docs_server (2)**

1. Leave the **Allowed tools** dropdown empty to allow all tools from the MCP server.

1. Select the **Create tool (3)** button to add the tool to your agent.

   ![](./Media/lab7-s21.png)

## Task 3.4: Deploy your agent to Microsoft Foundry

In this task, you’ll deploy your configured AI agent to Microsoft Foundry and verify it appears in your project resources.

1. In the agent designer view, select the **Create Agent on Microsoft Foundry** button in the bottom-left corner.

   ![](./Media/lab3-06.png)

1. Wait for the deployment to complete.

1. In the VS Code navbar, refresh the **Resources** view.  **data-research-agent** should now appear under the **Classic Agents** subsection.

   ![](./Media/lab3-07.png)

### Task 3.5: Test your agent in the playground

In this task, you’ll open the agent in the playground and test it by sending prompts to verify it retrieves and uses external data through the MCP server tool.

1. Right-click on **data-research-agent (1)** in the **Classic Agents** subsection.

1. Select **Open Playground (2)** from the context menu.

   ![](./Media/lab3-08.png)

1. The Agents Playground will open in a new tab within VS Code.

1. In the **Agent Playground**, enter the following prompt in the chat box **(1)**, and then select **Send (2)**:

   ```output
   Can you help me find documentation about Azure Container Apps and provide an example of how to create one?
   ```

   ![](./Media/lab3-09.png)

1. Send the message and observe the authentication and approval prompts for the MCP Server tool:
    
    - In the **MCP Tools Authentication Setup** dialog, select **No Authentication**.

      ![](./Media/lab7-s26.png)
    
    - In the **MCP Tools Approval Preference** dialog, select **Always approve**.

      ![](./Media/lab7-s27.png)

1. Review the agent's response and note how it uses the MCP server tool to retrieve external information.

   ![](./Media/lab3-10.png)

1. Check the **Agent Annotations** section to see the sources of information used by the agent.

### Task 3.6: Generate sample code for your agent

In this task, you’ll generate and review sample SDK code to interact with your AI agent programmatically using the Microsoft Foundry Projects client library.

1. Right-click on **data-research-agent (1)** and select **View Code** button in the Agent Preferences page.

   ![](./Media/lab3-12.png)

1. In the **Choose your preferred SDK** dropdown, select **Microsoft Foundry Projects client library**.

   ![](./Media/lab3-13.png)

1. Select your preferred programming language (eg. Python).

   ![](./Media/lab3-14.png)

1. In the **Choose an auth method** dropdown, select **EntraID (default)**.

   ![](./Media/lab3-15.png)

1. Review the generated sample code that demonstrates how to interact with your agent programmatically.

   ![](./Media/lab3-16.png)

You can use this code as a starting point for building applications that leverage your AI agent.

### Task 3.7: View conversation history and threads

In this task, you’ll review conversation threads and run details in the Microsoft Foundry extension to analyze agent interactions, messages, and tool usage history.

1. In the **Azure Resources** view, expand the **Threads** subsection to see conversations created during your agent interactions.

   ![](./Media/lab3-17.png)

1. Select a thread to view the **Thread Details** page, which shows:
   
   - Individual messages in the conversation
   - Run information and execution details
   - Agent responses and tool usage

1. Select **View run info** to see detailed JSON information about each run.

   ![](./Media/lab3-18.png)

## Summary

In this lab, you used the Microsoft Foundry VS Code extension to create and configure an AI agent using the visual designer and MCP server tools. You connected the agent to external APIs and documentation sources, enabling it to retrieve up-to-date information and respond to user queries with accurate, enriched results. You then deployed, tested the agent in the playground, generated sample SDK code, and explored conversation threads to understand agent interactions and execution details.
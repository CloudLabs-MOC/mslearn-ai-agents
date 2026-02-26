# Lab 03c: Connect AI agents to tools using Model Context Protocol (MCP)

### Estimated Duration: 30 Minutes

## Overview

In this lab, you will build an AI agent using Microsoft Foundry that connects to a remote Model Context Protocol (MCP) server to access trusted and up-to-date technical documentation. You will configure the agent with MCP function tools and enable it to retrieve real-time information from official Microsoft Learn resources. Finally, you will run and test the agent to observe how it uses MCP tools to answer developer queries accurately.

> **Tip:** The code used in this exercise is based on the Azure AI Agent service MCP support sample repository. Refer to [Azure OpenAI demos](https://github.com/retkowsky/Azure-OpenAI-demos/blob/main/Azure%20Agent%20Service/9%20Azure%20AI%20Agent%20service%20-%20MCP%20support.ipynb) or visit [Connect to Model Context Protocol servers](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/model-context-protocol) for more details.

> **Note:** Some of the technologies used in this exercise are in preview or in active development. You may experience some unexpected behavior, warnings, or errors.

## Lab Objectives

- **Task 1:** Develop an agent that uses MCP function tools

## Task 1: Develop an agent that uses MCP function tools

Now that you've created your project in AI Foundry, let's develop an app that integrates an AI agent with an MCP server.

### Task 1.1: Clone the repo containing the application code

In this task, you’ll use Azure Cloud Shell (PowerShell) to clone the GitHub repository and navigate to the project folder containing the MCP-based AI agent application code.

1. In the **Azure portal**, select the **Cloud Shell** icon in the top navigation bar to open a new Cloud Shell session.

    ![](./Media/lab1-02-12.png)

1. In the Cloud Shell toolbar, open the **Settings (1)** menu and choose **Go to Classic version (2)** from the drop-down.

    ![](./Media/lab2-s9.png)

    >**Note:** **Ensure you've switched to the classic version of the cloud shell before continuing.**

1. In the cloud shell pane, enter the following commands to clone the GitHub repo containing the code files for this exercise (type the command, or copy it to the clipboard and then right-click in the command line and paste as plain text):

    ```
   rm -r ai-agents -f
   git clone https://github.com/MicrosoftLearning/mslearn-ai-agents ai-agents
    ```
    ![](./Media/lab3c-s3.png)

    > **Tip:** As you enter commands into the cloudshell, the output may take up a large amount of the screen buffer and the cursor on the current line may be obscured. You can clear the screen by entering the `cls` command to make it easier to focus on each task.

1. Enter the following command to change the working directory to the folder containing the code files and list them all.

    ```
   cd ai-agents/Labfiles/03c-use-agent-tools-with-mcp/Python
   ls -a -l
    ```

    ![](./Media/lab3c-s4.png)

### Task 1.2: Configure the application settings

In this task, you’ll create a virtual environment, install required libraries, and update the project endpoint and model deployment name in the configuration file.

1. In the cloud shell command-line pane, enter the following command to install the libraries you'll use:

    ```
   python -m venv labenv
   ./labenv/bin/Activate.ps1
   pip install -r requirements.txt
    ```

    >**Note:** You can ignore any warning or error messages displayed during the library installation.

1. Enter the following command to edit the configuration file that has been provided:

    ```
   code .env
    ```

    ![](./Media/lab3c-s5.png)

1. In the code file, replace the placeholder values with the correct details for your project:

    * PROJECT\_ENDPOINT : **Foundry project endpoint (1)**
    * MODEL\_DEPLOYEMNT\_NAME : **gpt-4.1 (2)**

        ![](./Media/lab3c-s6.png)

        > **Note:** Paste the project endpoint you copied in the previous task.

1. After you've replaced the placeholder, use the **CTRL+S** command to save your changes and then use the **CTRL+Q** command to close the code editor while keeping the cloud shell command line open.

### Task 1.3: Connect an Azure AI Agent to a remote MCP server

In this task, you’ll connect the Azure AI agent to a remote MCP server, configure it with tools and instructions, run a prompt, handle approval requests, and retrieve the final response.

1. Enter the following command to edit the code file that has been provided:

    ```
   code client.py
    ```

    ![](./Media/lab3c-s7.png)

1. Find the comment **Add references** and add the following code to import the classes:

    ```python
   # Add references
   from azure.identity import DefaultAzureCredential
   from azure.ai.projects import AIProjectClient
   from azure.ai.projects.models import PromptAgentDefinition, MCPTool
   from openai.types.responses.response_input_param import McpApprovalResponse, ResponseInputParam
    ```

    ![](./Media/lab3c-s8.png)

1. Find the comment **Connect to the agents client** and add the following code to connect to the Azure AI project using the current Azure credentials.

    ```python
   # Connect to the agents client
   with (
       DefaultAzureCredential(
           exclude_environment_credential=True,
           exclude_managed_identity_credential=True) as credential,
       AIProjectClient(endpoint=project_endpoint, credential=credential) as project_client,
       project_client.get_openai_client() as openai_client,
    ):
    ```

    ![](./Media/lab3c-s9.png)

1. Under the comment **Initialize agent MCP tool**, add the following code:

    ```python
   # Initialize agent MCP tool
   mcp_tool = MCPTool(
       server_label="api-specs",
       server_url="https://learn.microsoft.com/api/mcp",
       require_approval="always",
   )
    ```

    ![](./Media/lab3c-s10.png)

    - This code will connect to the Microsft Learn Docs remote MCP server. This is a cloud-hosted service that enables clients to access trusted and up-to-date information directly from Microsoft's official documentation.

1. Under the comment **Create a new agent with the MCP tool** and add the following code:

    ```python
   # Create a new agent with the MCP tool
   agent = project_client.agents.create_version(
       agent_name="MyAgent",
       definition=PromptAgentDefinition(
           model=model_deployment,
           instructions="You are a helpful agent that can use MCP tools to assist users. Use the available MCP tools to answer questions and perform tasks.",
           tools=[mcp_tool],
       ),
   )
   print(f"Agent created (id: {agent.id}, name: {agent.name}, version: {agent.version})")
    ```

    ![](./Media/lab3c-s11.png)

    - In this code, you provide instructions for the agent and provide it with the MCP tool definitions.

1. Find the comment **Create a conversation thread** and add the following code:

    ```python
   # Create a conversation thread
   conversation = openai_client.conversations.create()
   print(f"Created conversation (id: {conversation.id})")
    ```

1. Find the comment **Send initial request that will trigger the MCP tool** and add the following code:

    ```python
   # Send initial request that will trigger the MCP tool
   response = openai_client.responses.create(
       conversation=conversation.id,
       input="Give me the Azure CLI commands to create an Azure Container App with a managed identity.",
       extra_body={"agent": {"name": agent.name, "type": "agent_reference"}},
   )
    ```

    ![](./Media/lab3c-s12.png)

1. Find the comment **Process any MCP approval requests that were generated** and add the following code:

    ```python
   # Process any MCP approval requests that were generated
   input_list: ResponseInputParam = []
   for item in response.output:
       if item.type == "mcp_approval_request":
           if item.server_label == "api-specs" and item.id:
               # Automatically approve the MCP request to allow the agent to proceed
               input_list.append(
                   McpApprovalResponse(
                       type="mcp_approval_response",
                       approve=True,
                       approval_request_id=item.id,
                   )
               )

   print("Final input:")
   print(input_list)
    ```

    ![](./Media/lab3c-s13.png)

1. Find the comment **Send the approval response back and retrieve a response** and add the following code:

    ```python
   # Send the approval response back and retrieve a response
   response = openai_client.responses.create(
       input=input_list,
       previous_response_id=response.id,
       extra_body={"agent": {"name": agent.name, "type": "agent_reference"}},
   )

   print(f"\nAgent response: {response.output_text}")
    ```

    ![](./Media/lab3c-s14.png)

1. Find the comment **Clean up resources by deleting the agent version** and add the following code:

    ```python
   # Clean up resources by deleting the agent version
   project_client.agents.delete_version(agent_name=agent.name, agent_version=agent.version)
   print("Agent deleted")
    ```

    ![](./Media/lab3c-s14.1.png)

1. Save the code file **CTRL+S** when you have finished. You can also close the code editor **CTRL+Q**; though you may want to keep it open in case you need to make any edits to the code you added. In either case, keep the cloud shell command-line pane open.

### Task 1.4: Run the app

In this task, you’ll sign in to Azure using the CLI, run the application, and verify that the agent successfully processes the prompt by using the MCP server to retrieve and return the required information.

1. In the Cloud Shell console, enter the following command to run the application:

    ```
   python client.py
    ```

1. Wait for the agent to process the prompt, using the MCP server to find a suitable tool to retrieve the requested information. You should see some output similar to the following:

    ![](./Media/lab3c-s19.png)

    ```
    Agent created (id: MyAgent:2, name: MyAgent, version: 2)
    Created conversation (id: conv_086911ecabcbc05700BBHIeNRoPSO5tKPHiXRkgHuStYzy27BS)
    Final input:
    [{'type': 'mcp_approval_response', 'approve': True, 'approval_request_id': '{approval_request_id}'}]

    Agent response: Here are Azure CLI commands to create an Azure Container App with a managed identity:

    **1. For a System-assigned Managed Identity**
    ```sh
    az containerapp create \
    --name <CONTAINERAPP_NAME> \
    --resource-group <RESOURCE_GROUP> \
    --environment <CONTAINERAPPS_ENVIRONMENT> \
    --image <CONTAINER_IMAGE> \
    --identity 'system'
    ```

    [continued...]

    Agent deleted
    ```

    Notice that the agent was able to invoke the MCP tool to automatically fulfill the request.

1. You can update the input in the request to ask for different information. In each case, the agent will attempt to find technical documentation by using the MCP tool.

1. In the Cloud Shell window, select the **Close (X)** icon to exit Cloud Shell before proceeding to the next lab.

    ![](./Media/lab1-02-16.png)

## Summary

In this lab, you created a Microsoft Foundry project, deployed the Microsoft Azure AI Foundry model, and configured the project endpoint for your application.
You set up a Python development environment, installed dependencies, and built an AI agent integrated with a remote MCP server using the Azure AI Agents SDK.
Finally, you authenticated with Azure, ran the application, and verified that the agent used MCP tools to retrieve trusted documentation and generate accurate responses.

### You have successfully completed the Hands-on Lab!
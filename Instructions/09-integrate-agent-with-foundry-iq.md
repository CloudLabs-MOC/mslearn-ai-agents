# Lab 09: Integrate an AI agent with Foundry IQ

### Estimated Duration: 60 Minutes

## Overview

In this lab, you use Microsoft Azure AI Foundry to build an intelligent agent integrated with Foundry IQ for enterprise knowledge retrieval. You create and deploy a gpt-4.1 based agent, connect it to an Azure AI Search–powered knowledge base, and ground it with product documents stored in Azure Blob Storage. You then test the agent in the Foundry playground and connect to it programmatically using the Python SDK from Azure Cloud Shell. This lab demonstrates how to build conversational AI solutions that can search and retrieve enterprise knowledge while maintaining context.

> **Tip:** The code used in this exercise is based on the Microsoft Foundry SDK for Python. You can develop similar solutions using the SDKs for Microsoft .NET, JavaScript, and Java. Refer to [Microsoft Foundry SDK client libraries](https://learn.microsoft.com/azure/ai-foundry/how-to/develop/sdk-overview) for details.

> **Note:** Some of the technologies used in this exercise are in preview or in active development. You may experience some unexpected behavior, warnings, or errors.

## Lab Objectives

- **Task 1:** Create and Configure Your Agent with Data and Foundry IQ

- **Task 2:** Test the Agent in the playground

- **Task 3:** Connect to Your Agent from a Client Application

## Task 1: Create and Configure Your Agent with Data and Foundry IQ

In this task, you will configure the agent in Microsoft Azure AI Foundry to use Foundry IQ by connecting it to an Azure AI Search resource. You also create a knowledge base using product documents stored in Azure Blob Storage to enable accurate and grounded responses.

1. In Microsoft Foundry, select **Agents (1)** from the left navigation pane, and then click **Create agent (2)**.

    ![](./Media/lab1-02-25.png)

1. In the **Create an agent** pane, enter **product-expert-agent (1)** as the agent name, and then select **Create (2)**.

    ![](./Media/lab1-02-28.png)

1. In the **Instructions (1)** section, update the following instructions.
    
    ```
    You are a helpful AI assistant for Contoso, specializing in outdoor camping and hiking products. 
    You must ALWAYS search the knowledge base to answer questions about our products or product 
    catalog. Provide detailed, accurate information and always cite your sources.
    If you don't find relevant information in the knowledge base, say so clearly.
    ```

1. Select **Save (2)** to save your current agent configuration.

    ![](./Media/lab9-s7.png)

1. Then, in the **Knowledge** section, expand **(1)** the **Add (2)** dropdown, and select **Connect to Foundry IQ (3)**.

    ![](./Media/lab9-s8.png)

1. In the **Connect to Foundry IQ** window, select **Connect to an AI Search resource**.

    ![](./Media/lab9-s9.png)

1. On the **Ground your agent in enterprise knowledge** page, select **Create new resource**, which opens the Azure portal in a new tab.

    ![](./Media/lab9-s10.png)

1. Create a search resource with the following settings and click **Review + create (6)**
    - **Subscription:** Select default subscription **(1)**
    - **Resource group:** select **AI-3026-RG (2)**
    - **Service name:** Enter **aiservice-<inject key="DeploymentID"></inject> (3)**
    - **Location:** Select **<inject key="Region"></inject> (4)**
    - **Pricing tier:** Select **Free** if available, otherwise choose **Basic** **(5)**

      ![](./Media/lab1-02-29.png)

      - Now you'll upload sample product information documents to connect to with Foundry IQ.

1. On the **Create a search service** page, review the configuration and then select **Create**.

    ![](./Media/lab1-02-30.png)

1. Download the sample product information files by opening a new browser tab and navigating to `https://github.com/MicrosoftLearning/mslearn-ai-agents/raw/main/Labfiles/09-integrate-agent-with-foundry-iq/data/contoso-products.zip`

1. Select the **Downloads (1)** icon in the browser toolbar, and then choose **Open file (2)** for the downloaded `contoso-products.zip` file.

    ![](./Media/lab9-s52.png)

1. In the File Explorer window, select **Extract (1)**, and then choose **Extract all (2)** to unzip the `contoso-products` folder.

    ![](./Media/lab9-s53.png)

1. In the **Extract Compressed (Zipped) Folders** dialog, extract the files from the zip, which should be 3 PDFs detailing the products from Contoso and then select **Extract**.

    ![](./Media/lab9-s54.png)

1. In the Azure Portal tab, in the top search bar, search fo **Storage accounts (1)** and select **Storage accounts (2)** from the services section.

    ![](./Media/lab9-s29.png)

1. In the **Storage center | Blob Storage** page, select **+ Create** to start creating a new storage account.

    ![](./Media/lab9-s13.png)

1. Create a storage account with the following settings and click **Review + create (8)**
    - **Subscription:** Select default subscription **(1)**
    - **Resource group:** Select **AI-3026-RG (2)**
    - **Storage account name:** **storage<inject key="DeploymentID"></inject> (3)**
    - **Region:** Select **<inject key="Region"></inject> (4)**
    - **Preferred storage type:** Azure Blob Storage or Azure Data Lake Storage Gen 2 **(5)**
    - **Performance:** Standard **(6)**
    - **Redundancy:** Locally-redundant storage (LRS) **(7)**

      ![](./Media/lab1-02-31.png)

1. On the **Review + create** tab, select **Create**.

    ![](./Media/lab9-s15.png)

1. When the deployment is complete and the **Your deployment is complete** message appears, select **Go to resource**.

    ![](./Media/lab9-s16.png)

1. In the storage account **Overview** page, select **Upload** from the top bar.

    ![](./Media/lab9-s17.png)

1. In the **Upload blob** pane, select **Create new** under Select an existing container.

    ![](./Media/lab9-s18.png)

1. In the **New container** pane, enter `contosoproducts` in the **Name (1)** field, and then select **Ok (2)**.

    ![](./Media/lab9-s19.png)

1. In the **Upload blob** pane, select **Browse for files**.

    ![](./Media/lab9-s55.png)

1. In the **Open** dialog box, select **Downloads (1)**, double-click the **contoso-products** folder, select all three PDF files **(2)**, and then click **Open (3)**.

    ![](./Media/lab9-s56.png)

1. In the **Upload blob** pane, verify that all three PDF files are selected and `contosoproducts` is chosen, and then select **Upload**.

    ![](./Media/lab9-s57.png)

1. Once your files are uploaded, close the Azure Portal tab and navigate back to the Foundry IQ page in Microsoft Foundry and refresh the page.

1. In the **Ground your agent in enterprise knowledge** page, select the **Azure AI Search resource (1)**, and then click **Connect (2)**.

    ![](./Media/lab9-s21.png)

1. On the **Foundry IQ** page, select **Create a knowledge base**.

    ![](./Media/lab9-s22.png)

1. In the **Choose a knowledge type** window, select **Azure Blob Storage (1)**, and then click **Connect (2)**.

    ![](./Media/lab9-s23.png)

1. Configure your knowledge source with the following settings:
    - **Name:** `ks-contosoproducts` **(1)**
    - **Description:** `Contoso product catalog items` **(2)**
    - **Storage account name:** **storage<inject key="DeploymentID"></inject> (3)**
    - **Container name:** `contosoproducts` **(4)**
    - **Authentication type:** API Key **(5)**
    - **Content extraction mode:** minimal **(6)** 
    - **Include embedding model:** Selected **(7)**
    - **Embedding model:** Select the available deployed model, likely **text-embedding-3-small (8)**
    - **Chat completions model:** Select the available deployed model, likely **gpt-4.1 (9)**
1. Select **Create (10)**.

    ![](./Media/lab9-s24.png)

1. On the knowledge base creation page, select the `gpt-4.1` **(1)** model from the **Chat completions model** dropdown, leaving the rest of the optional fields as is.

1. Select **Save knowledge base (2)**, and then refresh your browser to verify the knowledge source status is **active**. If it isn't yet, wait a minute and refresh your page until it is.

    ![](./Media/lab9-s25.png)

    ![](./Media/lab9-s27.png)

1. On the top right, expand the **Use in an agent (1)** dropdown, and select your `product-expert-agent` **(2)**.

    ![](./Media/lab1-02-27.png)

## Task 2: Test the Agent in the playground

In this task, you test the agent in the Microsoft Azure AI Foundry playground to verify that it retrieves accurate product information from the connected knowledge base and maintains context during interactions.

1. On the **Playground** tab, verify that your knowledge base is listed under **Knowledge**, enter `What types of tents does Contoso offer?` in the chat box, and then send the message.

    ![](./Media/lab9-s31.png)

1. Review the response and notice that the agent provides specific information retrieved from the connected knowledge base.

     ![](./Media/lab9-s58.png)

     > **Note:** If prompted to approve the knowledge base tool, select Approve, and then choose any appropriate approval option.

1. Try the following test queries to verify the agent can retrieve information from the knowledge base:

    - `Tell me about which backpacks are available in XL.`
    - `What camping accessories are available?`

1. Review the responses and notice:
    - The agent provides specific information from the knowledge base
    - Citations or references to the source documents may be included
    - The agent stays focused on product information

1. You can also try interacting with your agent in the **Preview agent** for a more refined webapp experience.

1. In the agent details page, locate and copy the following information to a notepad (you'll need these later):
    - **Agent name:** This is the name you created (`product-expert-agent`)

      ![](./Media/lab9-s59.png)

    - **Project endpoint:** In the navigation bar on the left, select **Microsoft Foundry** to return to the Foundry home page and Copy the **Project endpoint**.

      ![](./Media/lab2-s6.png)

## Task 3: Connect to Your Agent from a Client Application

Now you'll create a Python application to interact with your agent programmatically. Starter files have been provided in the GitHub repository to help you get started quickly.

### Task 3.1 Clone the repo containing the application code

In this task, you access Microsoft Azure Portal, open Azure Cloud Shell, and clone the GitHub repository to set up the Python client application for interacting with your agent programmatically.

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

    ![](./Media/lab9-s36.png)
 
    > **Tip:** As you enter commands into the cloudshell, the output may take up a large amount of the screen buffer and the cursor on the current line may be obscured. You can clear the screen by entering the `cls` command to make it easier to focus on each task.

1. Enter the following command to change the working directory to the folder containing the code files and list them all.

    ```
   cd ai-agents/Labfiles/09-integrate-agent-with-foundry-iq/Python
   ls -a -l
    ```

    ![](./Media/lab9-s37.png)

    - The provided files include application code, configuration settings, and the agent client starter code.

### Task 3.2: Configure the application settings

In this task, you will set up the Python environment and update the configuration file with your project endpoint and agent name to connect the application to your deployed agent.

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

    ![](./Media/lab9-s38.png)

1. In the code file, replace the placeholder values with the correct details for your project:

    * PROJECT\_ENDPOINT : **Foundry project endpoint (1)**
    * AGENT_NAME : **product-expert-agent (2)**

         ![](./Media/lab9-s39.png)

         > **Note:** Paste the project endpoint you copied in the previous task.

1. After you've replaced the placeholder, use the **CTRL+S** command to save your changes and then use the **CTRL+Q** command to close the code editor while keeping the cloud shell command line open.

### Task 3.3: Complete the agent client code

In this task, you will connect the client application to your agent, implement message handling, manage conversations, and add logic to approve or deny the agent’s access to enterprise knowledge sources.

> **Tip:** As you add code, be sure to maintain the correct indentation. Use the comment indentation levels as a guide.

1. Enter the following command to edit the agent code file:

    ```
   code agent_client.py
    ```

    ![](./Media/lab9-s40.png)

1. Review the starter code that has been provided, including:
    - Import statements and configuration loading
    - The `send_message_to_agent()` function structure
    - The `display_conversation_history()` function
    - The main program loop

1. Find the first **TODO** comment and add the following code to connect to the project, get the OpenAI client, retrieve the agent, and create a new conversation:

    > **Tip:** Be careful to maintain the correct indentation level.

    ```python
    # Connect to the project and agent
    credential = DefaultAzureCredential(
        exclude_environment_credential=True,
        exclude_managed_identity_credential=True
    )
    project_client = AIProjectClient(
        credential=credential,
        endpoint=project_endpoint
    )

    # Get the OpenAI client
    openai_client = project_client.get_openai_client()

    # Get the agent
    agent = project_client.agents.get(agent_name=agent_name)
    print(f"Connected to agent: {agent.name} (id: {agent.id})\n")

    # Create a new conversation
    conversation = openai_client.conversations.create(items=[])
    print(f"Created conversation (id: {conversation.id})\n")
    ```

    ![](./Media/lab9-s41.png)

1. Find the second **TODO** comment inside the `send_message_to_agent()` function and add the following code to send messages and handle responses, including MCP approval requests:

    ```python
    # Add user message to the conversation
    openai_client.conversations.items.create(
        conversation_id=conversation.id,
        items=[{"type": "message", "role": "user", "content": user_message}],
    )
    
    # Store in conversation history (client-side)
    conversation_history.append({
        "role": "user",
        "content": user_message
    })
    
    # Create a response using the agent
    response = openai_client.responses.create(
        conversation=conversation.id,
        extra_body={
            "agent_reference": {
                "type": "agent_reference",
                "name": agent.name
            }
        },
        input=""
    )

    # Check if the response output contains an MCP approval request
    approval_request = None
    if hasattr(response, 'output') and response.output:
        for item in response.output:
            if hasattr(item, 'type') and item.type == 'mcp_approval_request':
                approval_request = item
                break
    
    # Handle approval request if present
    if approval_request:
        print(f"[Approval required for: {approval_request.name}]\n")
        print(f"Server: {approval_request.server_label}")
        
        # Parse and display the arguments (optional, for transparency)
        import json
        try:
            args = json.loads(approval_request.arguments)
            print(f"Arguments: {json.dumps(args, indent=2)}\n")
        except:
            print(f"Arguments: {approval_request.arguments}\n")
        
        # Prompt user for approval
        approval_input = input("Approve this action? (yes/no): ").strip().lower()
        
        if approval_input in ['yes', 'y']:
            print("Approving action...\n")
            
            # Create approval response item
            approval_response = {
                "type": "mcp_approval_response",
                "approval_request_id": approval_request.id,
                "approve": True
            }
        else:
            print("Action denied.\n")
            
            # Create denial response item
            approval_response = {
                "type": "mcp_approval_response",
                "approval_request_id": approval_request.id,
                "approve": False
            }
        
        # Add the approval response to the conversation
        openai_client.conversations.items.create(
            conversation_id=conversation.id,
            items=[approval_response]
        )
        
        # Get the actual response after approval/denial
        response = openai_client.responses.create(
            conversation=conversation.id,
            extra_body={
                "agent_reference": {
                    "type": "agent_reference",
                    "name": agent.name
                }
            },
            input=""
        )

    
    ```

    ![](./Media/lab9-s60.png)

1. After you've added the code, use the **CTRL+S** command to save your changes. 

1. Review the code now uses the conversations API to manage interactions with your agent, where:
    - A conversation is created and tracked by its ID
    - User messages are added to the conversation using `conversations.items.create()`
    - Responses are generated using `responses.create()` with an agent reference
    - **MCP approval handling**: When the agent needs to access Foundry IQ, it requests approval by returning an `mcp_approval_request` in the response output
    - The code prompts you to approve or deny the action before proceeding
    - After approval/denial, an `mcp_approval_response` is added to the conversation and a new response is generated
    - The agent retrieves information from Foundry IQ based on your approval decision

1. Use the **CTRL+Q** command to close the code editor while keeping the cloud shell command line open.

### Task 3.4: Test the Integration

In this task, you sign in to Azure, run the client application, and test the agent’s ability to retrieve and use knowledge base information while maintaining conversational context.

1. In the cloud shell command-line pane, run your application:

    ```
   python agent_client.py
    ```

1. When the application starts, test the agent with the following queries:

    **Query 1 - Product Categories:**
    ```
    What types of outdoor products does Contoso offer?
    ```
    
    ![](./Media/lab9-s61.png)

    **Note:** IF prompted for approval, type **yes** to allow the agent to search the knowledge base. Observe how the agent retrieves information from multiple documents in the knowledge base.

    **Query 2 - Specific Product Details:**
    ```
    Tell me about the weatherproof features of your tents.
    ```
    
    ![](./Media/lab9-s62.png)

    **Query 3 - Product Comparisons:**
    ```
    What's the difference between your daypacks and expedition backpacks?
    ```
    ![](./Media/lab9-s63.png)

    **Query 4 - Accessories and Add-ons:**
    ```
    What camping accessories would you recommend for a weekend hiking trip?
    ```
    ![](./Media/lab9-s64.png)

    **Query 5 - Follow-up Question:**
    ```
    How much do those items typically cost?
    ```
    ![](./Media/lab9-s65.png)

    - Notice how the agent maintains conversation context from your previous query.

1. Type `history` to view the complete conversation history.

    ![](./Media/lab9-s66.png)

1. Type `quit` when you're done testing.

## Summary

In this lab, you created a project in Microsoft Azure AI Foundry and deployed a GPT-4.1–based agent. You configured Foundry IQ by connecting the agent to an Azure AI Search knowledge base grounded with product documents stored in Azure Blob Storage. Finally, you tested the agent in the playground and integrated it with a Python client application to programmatically retrieve and use enterprise knowledge.

### You have successfully completed the Hands-on Lab!
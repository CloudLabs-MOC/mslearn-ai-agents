
# AI-102: Develop AI agents on Azure Workshop

Welcome to your AI-3026: Develop AI Agents on Azure workshop! We’re excited to guide you through hands-on learning with Azure AI services using Microsoft Foundry and the Azure portal. In this workshop, you’ll build, configure, and test intelligent AI agents using Microsoft Foundry.

### Overall Estimated Duration: 30 Minutes

## Overview

In this hands-on lab, you will build intelligent AI solutions using Microsoft Azure AI Foundry, Azure AI Agent Service, and the Microsoft Agent Framework SDK. You will create Foundry projects, deploy foundation models like GPT-4.1, and develop AI agents using the portal and Python SDK in Azure Cloud Shell. You will design agents for expense processing, customer support, ticket triage, and feedback analysis. The labs include grounding agents with enterprise data using Azure AI Search and Blob Storage. You will connect agents to external systems using the Model Context Protocol (MCP) and implement custom function tools for real-world automation. You will also build multi-agent solutions using sequential orchestration and A2A communication. By the end, you will understand how to develop, integrate, and automate enterprise AI workflows end-to-end.

## Objectives

By the end of this lab, you will be able to:

1. **Create a project and agent in Microsoft Foundry:** Set up a new Foundry project and create an AI agent with a deployed model ready for configuration.

2. **Configure an AI agent with knowledge and tools:** Define system instructions, upload an expense policy document for grounding, and enable tools such as file search and code interpreter.

3. **Test and validate the agent in the playground:** Interact with the agent by asking policy-related questions, submit an expense claim, and download and review the generated claim file.

4. **Build and configure an AI agent using the SDK:** Implement code to connect to the Foundry project, define agent instructions, and enable the built-in Code Interpreter tool.

5. **Develop and configure custom function tools:** Build functions such as generating support tickets and register them for use by the agent.

6. **Build AI agents for support ticket triage:** Create specialized agents to evaluate ticket priority, assign tickets to the appropriate team, and estimate the effort required.

7. **Connect an AI agent to an MCP server:** Integrate a Microsoft Foundry agent with a remote **Model Context Protocol (MCP) server** and configure MCP function tools for accessing trusted documentation.

8. **Build a sequential orchestration**: Define a workflow where each agent’s output feeds into the next, forming a multi-agent pipeline.

9. **Implement discoverable A2A agents:** Define skills, agent cards, and executors to enable message handling and make agents interoperable through the A2A protocol.

10. **Implement intelligent routing logic**: Classify tickets with structured JSON output, handle low-confidence cases, escalate billing issues, and automate responses for other categories.

11. **Ground an agent with enterprise knowledge**: Connect the agent to Azure AI Search and configure a knowledge base using documents stored in Azure Blob Storage.

## Pre-requisites

* Basic knowledge of the Azure portal.
* Understanding of Model Context Protocol (MCP) concepts and function tools.
* Familiarity with AI concepts such as agents, grounding data, and actions.
* An active Azure subscription with access to **Microsoft Foundry**.
* Basic knowledge of Python programming.
* Basic knowledge of Python and working in **Cloud Shell** or similar terminal environments.
* Permission to create and manage resources in the assigned resource group (for example, Azure AI User role).

## Architecture

The lab architecture demonstrates how a Microsoft Foundry project enables AI agent development for expense management:

1. **Microsoft Foundry Project and Deployed Model:** A workspace created in the Microsoft Foundry portal where a foundation model is deployed to power the AI agent’s conversational and task-based responses.

2. **AI Agent Configuration:** An agent created in the playground with defined system instructions that control its behavior and response logic.

3. **Grounding Data and Tools:** An uploaded expense policy document attached using File Search for contextual grounding, along with the Code Interpreter tool to enable dynamic actions such as generating downloadable expense claim files.

4. **Agents Playground Interface:** An interactive testing environment where users send prompts, validate grounded responses, trigger tool-based actions, and review generated outputs before integrating the agent into applications.

## Architecture Diagram

![](../Media/combarc.png)

## Explanation of Components

1. **Microsoft Foundry Project and Deployed Model:** The project serves as the central workspace in the Microsoft Foundry portal where AI resources are managed. Within this project, a foundation model is deployed to process user prompts and generate responses that power the AI agent.

2. **AI Agent Configuration:** The agent encapsulates the deployed model along with system instructions that define its purpose assisting employees with expense-related queries. These instructions control tone, scope, and task-handling logic during interactions.

3. **Knowledge Source (Expense Policy Document):** The uploaded expense policy document acts as the agent’s knowledge base. Using File Search, the agent retrieves relevant policy information to provide accurate, context-aware responses grounded in company guidelines.

4. **Code Interpreter and Playground Interaction:** The Code Interpreter tool enables the agent to generate and execute Python code for performing actions such as creating downloadable expense claim files. The Agents Playground provides the interactive interface where users test prompts, trigger actions, and validate outputs in real time.

# Getting Started with lab

Welcome to your AI-3026: Develop AI Agents on Azure workshop! We’ve prepared an interactive environment to help you explore how to design, build, and deploy intelligent AI agents using Microsofts Foundry.

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and **Guide** will be right at your fingertips within your web browser.
 
![Access Your VM and Lab Guide](../Media/ai-3026-labvm.png)

### Virtual Machine & Lab Guide
 
Your virtual machine is your workhorse throughout the workshop. The lab guide is your roadmap to success.

## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.
 
![Explore Lab Resources](../Media/ai-3026-g1.png)

## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the top right corner.
 
![Use the Split Window Feature](../Media/ai-3026-g2.png)

## Lab Guide Zoom In/Zoom Out
 
To adjust the zoom level for the environment page, click the **A↕: 100%** icon located next to the timer in the lab environment.

![](../Media/ai-3026-g5.png)

## Lab Progress

You can use the **Progress** tab to track your progress while working on the lab. A score will be provided after successful validation.

![](../Media/ai-3026-g3.png)

## Managing Your Virtual Machine
 
Feel free to **Start, Restart, or Stop (2)** your virtual machine as needed from the **Resources (1)** tab. Your experience is in your hands!
 
![Manage Your Virtual Machine](../Media/ai-3026-g4.png)

## Let's Get Started with Azure Portal
 
1. On your virtual machine, click on the **Azure Portal** icon as shown below:
 
   ![Launch Azure Portal](../Media/ai-3026-g6.png)

1. In the sign-in window, kindly sign in using the provided Azure credentials

    - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

        ![](../Media/ai-3026-g7.png)

    - **Temporary Access Pass:** <inject key="AzureAdUserPassword"></inject>

        ![](../Media/ai-3026-g8.png)

1. If prompted to **Stay signed in?**, you can click **No**.

    ![](../Media/ai-3026-g9.png)

1. If a **Welcome to Microsoft Azure** pop-up window appears, simply click **Maybe later** to skip the tour.

    ![](../Media/ai-3026-g10.png)

## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels explicitly tailored for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.
 
Learner Support Contacts:
 
- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Click on **Next** from the lower right corner to move on to the next page.

   ![](../Media/ai-3026-next.png)


## Happy Learning !!

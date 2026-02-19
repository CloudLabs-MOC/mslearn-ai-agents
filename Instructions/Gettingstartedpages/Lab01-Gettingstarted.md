
# AI-102: Azure AI Engineer Associate Workshop

Welcome to your AI-102: Azure AI Engineer Associate workshop! We’re excited to guide you through hands-on learning with Azure AI services using Azure AI Foundry, the Azure portal, and tools like Document Intelligence, Custom Vision, the Language Service, etc., to create, deploy, and test intelligent solutions.

# Lab 07: Explore AI Agent development

### Overall Estimated Duration: 60 Minutes

## Overview

In this hands-on lab, you’ll gain practical experience with **Azure AI Foundry** by creating a project and deploying the **gpt-4.1** model. You’ll then build an AI agent, configure its system instructions, and upload a corporate expenses policy document as grounding data. Next, you’ll enable actions such as the code interpreter and test the agent in the playground by asking questions and submitting an expense claim. Finally, you’ll download and review the generated claim file to observe how AI agents can automate real business processes and streamline workflows.

## Objectives

By the end of this lab, you will be able to:

1. **Create a project and deploy a model in Azure AI Foundry**: Set up a new project, deploy the gpt-4.1 model, and prepare it for agent development.

2. **Build and configure an AI agent**: Define system instructions, upload a corporate expenses policy document as grounding data, and enable the code interpreter for actions.

3. **Test and validate the agent in the playground**: Interact with the agent by asking policy-related questions, guide it through creating an expense claim, and review the generated claim file.

## Pre-requisites

* Basic knowledge of the Azure portal.
* Familiarity with AI concepts such as agents, grounding data, and actions.
* An active Azure subscription with access to **Azure AI Foundry**.
* Permission to create and manage resources in the assigned resource group (for example, Azure AI User role).

## Architecture

The lab architecture demonstrates how an Azure AI Foundry project supports AI agent development and automation:

1. **Azure AI Foundry Resource**: Created in the Azure portal, this resource connects to Azure AI services and hosts deployed models such as **gpt-4.1**.

2. **Azure AI Foundry Project**: A workspace where you deploy and manage the gpt-4.1 model, create agents, configure system instructions, and upload grounding data for agent knowledge.

3. **AI Agent**: A configurable assistant within the project that uses the deployed model and uploaded documents to answer questions, perform actions, and generate outputs (like expense claim files).

4. **Agents Playground Interface**: A built-in testing environment where you interact with the agent, validate its behavior, send queries, and review responses before applying the agent in real-world scenarios.

## Architecture Diagram

![](../Images/lab08archdiagram.png)

## Explanation of Components

1. **Azure AI Foundry Project**: The main workspace where you create and manage AI agents. It serves as the hub for deploying models, configuring agent instructions, uploading grounding data, and controlling access to resources.

2. **Deployed Model (gpt-4.1)**: The AI model used by your agent to generate responses. It is hosted within the Foundry project and accessed via endpoints to process queries and perform tasks.

3. **AI Agent**: A configurable assistant that leverages the deployed model and grounding data to answer questions, perform actions (like creating expense claims), and interact with users based on system instructions.

4. **Grounding Data / Knowledge Base**: Documents or files uploaded to the agent (e.g., the expenses policy) that provide the factual context for the agent’s responses.

5. **Code Interpreter / Actions**: Tools enabled for the agent to perform specific tasks programmatically, such as generating text files or processing data.

6. **Agents Playground**: An interactive interface within the Foundry project where you can test the agent, run queries, validate behavior, and review outputs before integrating it into applications.

# Getting Started with lab

Welcome to your AI-102: Azure AI Engineer Associate workshop! We’ve prepared an interactive environment for you to explore generative AI concepts and work with Microsoft Azure services like Azure AI Foundry, Document Intelligence, Custom Vision, Language Service, etc. Let’s get started and make the most of this hands-on experience.

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and **lab guide** will be right at your fingertips within your web browser.
 
![Access Your VM and Lab Guide](../Images/lab08labvm.png)

### Virtual Machine & Lab Guide
 
Your virtual machine is your workhorse throughout the workshop. The lab guide is your roadmap to success.

## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.
 
![Explore Lab Resources](../Images/envtab.png)

## Managing Your Virtual Machine
 
Feel free to **Start, Restart, or Stop (2)** your virtual machine as needed from the **Resources (1)** tab. Your experience is in your hands!
 
![Manage Your Virtual Machine](../Images/resourcetab.png)

## Lab Progress

You can use the **Progress** tab to track your progress while working on the lab. A score will be provided after successful validation.

![](../Images/progresstab.png)

## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the top right corner.
 
![Use the Split Window Feature](../Images/splitwindow.png)

## Lab Guide Zoom In/Zoom Out
 
To adjust the zoom level for the environment page, click the **A↕: 100%** icon located next to the timer in the lab environment.

![](../Images/zoominai102.png)

## Let's Get Started with Azure Portal
 
1. On your virtual machine, click on the Azure Portal icon as shown below:
 
   ![Launch Azure Portal](../Images/azureportalicon.png)

1. In the sign-in window, kindly sign in using the provided Azure credentials

    - **Email/Username:** <inject key="AzureAdUserEmail"></inject>

        ![](../Images/AI-l16-0.png)

    - **Password:** <inject key="AzureAdUserPassword"></inject>

        ![](../Images/AIl16-1.png)

1. If prompted to **Stay signed in?**, you can click **No**.

    ![](../Images/AIl16-2.png)

1. If a **Welcome to Microsoft Azure** pop-up window appears, simply click **Cancel** to skip the tour.

    ![](../Images/AIl16-3.png)


## Support Contact
 
The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels explicitly tailored for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.
 
Learner Support Contacts:
 
- Email Support: cloudlabs-support@spektrasystems.com
- Live Chat Support: https://cloudlabs.ai/labs-support

Click on **Next** from the lower right corner to move on to the next page.

   ![Start Your Azure Journey](../Images/nextpage.png)

## Happy Learning !!



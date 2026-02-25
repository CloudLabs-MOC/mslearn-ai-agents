# AI-3026: Develop AI agents on Azure Workshop

Welcome to your AI-3026: Develop AI Agents on Azure workshop! We’re excited to guide you through hands-on learning with Azure AI services using Microsoft Foundry and the Azure portal. In this workshop, you’ll build, configure, and test intelligent AI agents using Microsoft Foundry.

# Lab 05: Develop a multi-agent solution with Microsoft Agent Framework

### Overall Estimated Duration: 30 Minutes

## Overview

In this hands-on lab, you’ll build a multi-agent workflow using the Microsoft Agent Framework SDK and a Microsoft Foundry project, starting with deploying the gpt-4.1 model and configuring a Python client application. You’ll create Summarizer, Classifier, and Action agents, define a sequential orchestration, run the workflow in Azure Cloud Shell, and generate actionable insights from customer feedback.

## Objectives

By the end of this lab, you will be able to:

1. **Deploy and configure a model in Microsoft Foundry**: Create a project using the *gpt-4.1* model and capture its endpoint for client application integration.

2. **Set up the AI Agent client application**: Prepare a Python environment in Azure Cloud Shell, install required libraries, and configure project settings.

3. **Create AI agents**: Build the *Summarizer*, *Classifier*, and *Action* agents using the Microsoft Agent Framework SDK.

4. **Build a sequential orchestration**: Define a workflow where each agent’s output feeds into the next, forming a multi-agent pipeline.

5. **Run and validate the multi-agent workflow**: Execute the solution in Cloud Shell with sample customer feedback and confirm the agents generate accurate summaries, classifications, and recommended actions.

## Pre-requisites

* Basic knowledge of the Azure portal.
* Familiarity with Microsoft Agent Framework SDK concepts, including agents, orchestrations, and connectors.
* Basic knowledge of Python and working in **Cloud Shell** or similar terminal environments.

## Architecture

The lab architecture demonstrates how three AI agents collaborate using the **Microsoft Agent Framework SDK** inside a **Microsoft Foundry** project:

1. **Microsoft Foundry Project:** The central workspace that hosts the deployed *gpt-4.1* model and provides endpoints and API keys for the agents.

2. **Summarizer Agent:** Condenses customer feedback into a concise summary, extracting key points while keeping the tone neutral.

3. **Classifier Agent:** Categorizes the summarized feedback as **Positive**, **Negative**, or **Feature Request**, providing context for decision-making.

4. **Action Agent:** Suggests the next step or recommended action based on the summary and classification, such as logging feedback or escalating an issue.

5. **Sequential Orchestration:** Coordinates the workflow, ensuring that each agent runs in order and passes its output to the next agent.

6. **Final Output:** Displays the summarized feedback, classification, and recommended action, showing how the agents collaboratively analyze and act on customer input.

## Architecture Diagram

![](../Media/lab5-arch.png)

## Explanation of Components

1. **Microsoft Foundry Project:** Provides the environment to deploy the gpt-4.1 model, configure agents, and manage API endpoints for the multi-agent workflow.

2. **Microsoft Agent Framework SDK:** The framework used to build, orchestrate, and manage AI agents. It provides APIs for creating agents, defining sequential orchestrations, handling agent outputs, and connecting to Azure OpenAI services.

3. **Summarizer Agent:** Processes raw customer feedback and condenses it into a short, clear summary that captures the key points without bias.

4. **Classifier Agent:** Categorizes the summarized feedback into one of three classes - **Positive**, **Negative**, or **Feature Request** to provide context for actionable decisions.

5. **Action Agent:** Suggests the next step based on the summary and classification, such as escalating an issue, logging positive feedback, or adding a feature request to the backlog.

6. **Sequential Orchestration:** Manages the execution order of agents, ensuring that each agent runs in sequence and passes its output to the next agent for processing.

7. **Task Input and Final Output:** The input is customer feedback text, and the output shows the summarized feedback, classification, and recommended action, demonstrating the collaboration and workflow of the multi-agent system.

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
# AI-3026: Develop AI agents on Azure Workshop

Welcome to your AI-3026: Develop AI Agents on Azure workshop! We’re excited to guide you through hands-on learning with Azure AI services using Microsoft Foundry and the Azure portal. In this workshop, you’ll build, configure, and test intelligent AI agents using Microsoft Foundry.

# Lab 03: Use a custom function in an AI agent

### Overall Estimated Duration: 30 Minutes

## Overview

In this hands-on lab, you will gain practical experience with the Microsoft Foundry portal by creating a project and deploying the GPT-4.1 model. You will set up a Python client application in Microsoft Azure Cloud Shell, configure it with your project endpoint and deployment details, and implement a custom function to automate support ticket generation. Finally, you will build and test an AI agent that collects user information, invokes function tools, and demonstrates how intelligent automation can streamline real-world technical support workflows.

## Objectives

By the end of this lab, you will be able to:

1. **Create and deploy a Microsoft Foundry project:** Set up a project, deploy the GPT-4.1 model, and prepare it for integration with an AI agent.

2. **Develop and configure custom function tools:** Build functions such as generating support tickets and register them for use by the agent.

3. **Build and run an AI agent with custom functions:** Integrate the tools into an agent, interact with it in a live chat session, and validate function calls using conversation history.

## Pre-requisites

* Basic knowledge of the Azure portal.
* Familiarity with AI concepts such as creating projects, deploying models, building agents, and managing them in Microsoft Foundry.
* An active Azure subscription with access to **Microsoft Foundry portal**.
* Basic knowledge of Python programming.

## Architecture

1. **Microsoft Foundry Project:** The core service that provides access to model deployments, agent capabilities, and extensibility features such as custom function tools and integrations.

2. **Deployed Foundation Model (gpt-4.1):** A centralized workspace where the GPT-4.1 model is deployed and managed, serving as the foundation for building and running your AI agent solution.

3. **Agent and Client Application:** The AI agent uses the deployed model to handle user requests and call custom functions automatically, while the Python client connects to the project endpoint, manages chats, and generates support ticket files.

## Architecture Diagram

![](../Media/lab3-arch.png)

## Explanation of Components

1. **Microsoft Foundry Project:** The workspace that hosts your gpt-4.1 deployment and agent configuration; exposes the project endpoint your app uses to connect.

2. **Deployed Model (gpt-4.1):** Deployed LLM inside your Microsoft Foundry project, exposed via the project endpoint; your agent calls it by its deployment name (e.g., gpt-4.1) to process prompts and return responses.

3. **AI Agent:** A server-side agent defined in the project with system instructions and a registered toolset; maintains a stateful thread, decides when to call functions, and returns results.

4. **Agent Tools & Client (Python):** Python custom function tools (e.g., submit_support_ticket) registered to the agent and invoked during chat, together with the client script that connects via the project endpoint to send prompts, trigger those functions, log conversation history, save artifacts like ticket-XXXX.txt, and clean up resources.outputs.

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

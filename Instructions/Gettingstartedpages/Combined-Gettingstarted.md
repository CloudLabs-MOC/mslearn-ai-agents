# Develop agent systems using Microsoft Foundry and the Microsoft Agent Framework

Welcome to your Develop agent systems using Microsoft Foundry and the Microsoft Agent Framework workshop! We’re excited to guide you through hands-on learning with Azure AI services using Microsoft Foundry and the Azure portal. In this workshop, you’ll build, configure, and test intelligent AI agents using Microsoft Foundry.

### Overall Estimated Duration: 2 hours 30 minutes

## Overview

In this hands-on lab, you will build intelligent AI agents using Microsoft Foundry to address real-world scenarios like expense management and customer support automation. You will ground agents with enterprise data using Azure Blob Storage and Azure AI Search through Foundry IQ to enable accurate, context-aware responses. You will design and implement agent-driven workflows and validate them programmatically using Python and the Azure AI Projects SDK. Additionally, you will explore multi-agent solutions using the Microsoft Agent Framework, where multiple agents collaborate through orchestration patterns. By the end of this lab, you will understand how to build, integrate, and orchestrate enterprise-grade AI agent solutions end to end.


## Objectives

By the end of this lab, you will be able to:

1. **Explore AI Agent development:** In this hands-on lab, participants will use the Microsoft Foundry portal to build an AI agent for handling employee expense claims. They will configure agent instructions, ground the agent using an expense policy document, and test it in the playground, including generating a downloadable expense claim file.

2. **Integrate an AI agent with Foundry IQ:** In this hands-on lab, participants will create an AI agent in Microsoft Foundry and integrate it with Foundry IQ for enterprise knowledge grounding. They will configure the agent using product documents from Azure Blob Storage and Azure AI Search, test it in the playground, and connect it via a Python client to send queries and retrieve knowledge-driven responses.

3. **Build a workflow in Microsoft Foundry:** In this hands-on lab, participants will design and implement a sequential workflow for automated customer support ticket processing. They will create AI agents to classify tickets, manage escalations, and generate responses, and then connect the workflow to Python using the Azure AI Projects SDK for programmatic validation.

4. **Develop a multi-agent solution with Microsoft Agent Framework (Optional):** In this hands-on lab, participants will build a multi-agent solution using the Microsoft Agent Framework SDK. They will implement a sequential orchestration pattern where multiple agents collaborate in a pipeline to process inputs and generate meaningful outputs.

## Pre-requisites

* Basic knowledge of the Azure portal.
* Familiarity with AI concepts such as agents, grounding data, and actions.
* An active Azure subscription with access to **Microsoft Foundry**.


# Getting Started with lab

Welcome to your Develop agent systems using Microsoft Foundry and the Microsoft Agent Framework workshop! We’ve prepared an interactive environment to help you explore how to design, build, and deploy intelligent AI agents using Microsofts Foundry.

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and **Guide** will be right at your fingertips within your web browser.
 
![Access Your VM and Lab Guide](../Media/labvm001.png)

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

![](../Media/labvm004.png)

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

### Click on **Next** from the lower right corner to move on to the next page.

![](../Media/d1.png)

## Happy Learning !!

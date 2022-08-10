---
layout: post
title:  Global Azure Sydney
date:   2022-04-22
tags: azure 100-days-of-azure MeetUp 
---

# Session 1 - Building Rapidly with Logic
### Presenter: John Billiris
How goods a tweet user sentiment.
Logic Apps, Functions and Cosmos DB

# Session 2 - Flasking Fast and Speaking Clingon
### Presenter: Renee Noble

Create a quick translation web app, using Flask, Azure Cognitive Services and Azure App Service

APP ROUTING, GET POST IN FLASK

Love the energy

Azure Cognitice Services. Cloud Based Machine Transclation service

>As easy as ~~Apple Pie~~ API

Construct the URI, headers and body

Prettification

Get it on the cloud > GitHub > Azure > Websiting! SuperChill ™️

aka.ms/inter-language-internet-demo

Enable git hub actions for creating web app.
Create the Application settings keys - become environment variables.

Python Flask Build

# Session 3 - AI Azure Governance
### Presenter: The Power Panel. Dr David Goodall - CTO for IBM 

**Why the risks are so importanty, why can't they be ignored?**
The way that we use AI impacts people. Decisions made by the technology, self driving cars, bank approval, makes huge impacts to people
Because it impacts people, there are rules, regulations and laws that fovernaments are putting into place. e.g. GDPR has components include the abuse of AI.
Incorrect usage of AI can result with fines, etc.
Target had to back off with their usage of AI after the pregnancy shopping habits.

**How do we monitor to highlight AI issues?**
We think of responsible AI, it's not just a technology, There is much more context, and the solution needs to account for those impacted by the solution. The solution should include the strategy for compliance to regulatory requirements, and the Open AI codex. These guiding principals can help to construct the monitors.

Responsible AI framework in Microsoft is an open source project with tools, and integrates to Azure Machine Learning. the purpose is to present free tools to developers to create better AI models. Looking at learning data sets to ensure fairness. It enables creators to fully explain how the 'black box' works. It helps to explain signals and outcomes.

Azure also has monitoring solutions to help identity data drifts.

It could be viewed as 'Fairness as a Service'. It encapsulates many signals and demographics. 'Fairness' is about trying to level the field and ensure that underrepresented demographics are still fairly accomodated. The 'Fairness checklist' is easily available. 

AI tools are biased because we are bias. This is prevalent in supervised learning, and to lesser extent unsupervised learning. This is why the tools exist. Bias can be engineered out of the model, it can't be engineered out of the developer.

_All these tools are presented for free_

**Can AI wipe us out?**

AI seems to facilitate such a primeval response. It plays on our psyche, there's plenty of Sci-Fi movies.

Its about handling users understanding peoples understanding.

Narrow vs General AI
Narrow is about specific use case, understanding voice, or image
General, take learning from one Context and applying it another context
General AI is about 30-35 years away
AI is not going to take away your job, destroy the world, etc.

10-15 years before trucking is fully automated. The AI revolution is going to take a lot long, this time frame gives us time to understand ethical issues, etc. AI will impact jobs, but not displace them.

There are 9-10 Australian regulations, very little protection. Microsoft refuse to work on some projects, because of the blurred ethical lines

**What three things should be done to mitigate risk?**

* Awareness - Talk with management and leadership, you need to break traditional governance and educate those driving solutions. It's different
* Do a risk assessment - Identify all the items required to have good governance. People, Processes, etc.
* 

# Session 4 - Send in the bots!
### Presenter: Ajo Suresh
ajo3403.medium.com

**What is a chatbot?**
Use AI and Natural Language Processing (NLP) to engage human conversation in a natural way. Used in many channels, such as mobile apps, website, messaging apps, etc

**How does a chatbot work?**

1. User enters a message into a chatbot channel
2. NLP then interprets the message
3. Chatbot determines the appropriate response

**Azure Bot Service**

1. Comprehensive development experience. Rapid development complemented by a wide gammut of 
2. Powered by world class AI.
3. Multi-channel experiences.
4. Your brand, your data.

**Building a bot**

1. Plan - Have a thorough understand of goals, processing, needs
2. Build - Utilise Azure frameworks
3. Test - Bots are complex, with many different parts
4. Publish - Make the bot public available
5. Connect - Create endpoints, for user consumption
6. Evaluate - Back to step 2. Keep incrementing!

Bot Framework Composer.

# Session 5 - Dude, Where's my server?
### Presenter: [Aaron Powell](https://www.aaron-powell.com)
Azure functions are usually the default thought for serverless. It's an event based architecture, code first, triggered often by services in Azure or HTTP events.

What people don't know, you can use Azure Functions with containers. You can bundle them into a container. Why would you do that? There's a couple of scenarios, perhaps you have a dependency that you can't install. There are a bunch of stuff that you can't use in an Azure function on bare metal. Another reason is the Hybrid infrastructure model. You can roll the azure function into a docker container, and run that on prem. You won't get the scalability - but it might make sense for your use case. The third reason you may do this, is edge computing. Applications that latency sensitive, you can push the application to edge, where the processing needs to happen.

Demo 1: Run Azure functions in a container

Demo 2: Serverless Containers
Azure Container Apps
KEDA can take insights to automate Kubernetes scaling
 'Oh no, my environment variables are gone'

 Resource group auto deletion - Jeff Holland

 Kubernetes is the underlying engine, however it's abstracted.

# Fin

>Day 6 of 💯. Who are you, where are the others?

![Azure has regions](https://media.giphy.com/media/l36kU80xPf0ojG0Erg/giphy.gif)
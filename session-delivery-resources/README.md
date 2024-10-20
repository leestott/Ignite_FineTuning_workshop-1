## How To Use

Welcome,

> [!NOTE]
>This repository contains the resources needed to deliver the session "Fine-Tuning NLP Models with Microsoft Olive" at Microsoft Ignite 2024.
> The following resources are intended for a presenter to learn and deliver the session.

We're glad you are here and look forward to your delivery of this amazing content. As an experienced presenter, we know you know HOW to present so this guide will focus on WHAT you need to present. It will provide you a full run-through of the presentation created by the presentation design team. 

Along with the video of the presentation, this document will link to all the assets you need to successfully present including PowerPoint slides and demo instructions &
code.

> [!NOTE]
> Read document in its entirety, watch the video presentation, ask questions of the Lead Presenter

## File Summary

| Resources          | Links                            | Description |
|-------------------|----------------------------------|-------------------|
| PowerPoint        | - [Presentation](https://aka.ms/..) | Slides |
<!-- | PPT Recording     | - [Presentation]() | Video Recording of the PowerPoint slides with no audio | -->

## Get Started

This repository is divided in to the following sections:

| [Slides](https://aka.ms/..) | [Skillable Workshop Instructions](/lab/Skillable%20Workshop%20Instructions/00_Introduction.md) | [Non-Skillable Workshop Instructions](/lab/README.md) |
|-------------------|---------------------------|--------------------------------------
| ** slides - 4 Hours minutes| 10 Labs - 180 minutes | Running the workshop outside Skillable |

## Slides

The [slides](https://aka.ms/...) have presenter notes in each part of the session

### Timing

For workshops, Q&A usually happens as the workshop is running. Might scrape these 5 minutes in favor of more hands-on time.​

| Time        | Description
--------------|-------------
0:00 - 30:00   | Introduction and Overview Welcome and objectives Overview of Microsoft Olive Importance of fine-tuning in NLP
30:00 -  75:00  | Setting Up the Environment Introduction to Azure and Local GPU setups Step-by-step guide to configuring Azure for fine-tuning Setting up a local GPU environment
75:00 - 120:00  | Fine-Tuning Basics Understanding pre-trained models Introduction to fine-tuning techniques Hands-on exercise: Fine-tuning a simple model
120:00 - 165:00 | Advanced Fine-Tuning Techniques Hyperparameter tuning Data augmentation strategies Hands-on exercise: Implementing advanced techniques
165:00 - 195:00 | Optimizing Performance Monitoring and evaluating model performance Using Microsoft Olive for optimization Hands-on exercise: Performance tuning
195:00 - 225:00 | Deploying Fine-Tuned Models Deployment strategies on Azure Local deployment considerations Hands-on exercise: Deploying a model
225:00 - 240:00 |Consumption of the Model Using .NET Aspire Application to consumed the fine tuned model Optimize the model for specific hardware
240:00 - 255:00 |Q&A and Wrap-Up (15 minutes)
Open floor for questions Recap of key takeaways Next steps and additional resources

## Workshop Instructions on Skillable Lab On Demand

| Section | Minutes | 
-------------------------------------------------------------------------------------------------------|---------|
|  [Lab1](/lab/Workshop%20Instructions/Lab1_Environment_Setup/readme.md) | Environment Setup      | 
|  [Lab2](/lab/Workshop%20Instructions/Lab2_Data_Preparation/readme.md) |  Data Preperation  |
|  [Lab3](/lab/Workshop%20Instructions/Lab3_Azure_AIStudio/readme.md) | Fine Tuning with Azure AI Studio  | 
|  [Lab4](/lab/Workshop%20Instructions/Lab4_AI_MLStudio/readme.md) | Fine Tuning with Azure ML Studio       | 
|  [Lab5](/lab/Workshop%20Instructions/Lab5_local_Cloud_MLStudio/readme.md) | Fine Tuning locally with Cloud Compute | 
|  [Lab6](/lab/Workshop%20Instructions/Lab6_local_Cloud_Olive/readme.md) | Fine Tuning with Olive using Cloud Compute   | 
|  [Lab7](/lab/Workshop%20Instructions/Lab7_Local_Olive/readme.md) | Fine Tuning with Olive using local GPU/CPU | 
|  [Lab 8](/lab/Workshop%20Instructions/Lab8_Deploying_Models/readme.md) |Deploy the finetuned model to Azure |
|  [Lab9](/lab/Workshop%20Instructions/Lab9_Evaluation/) | Evaluate the finetuned model |
|  [Lab10](/lab/Workshop%20Instructions/Lab10_Consumption/) | Consume the finetuned model with an application|
|  [Lab11](/lab/Workshop%20Instructions/Lab11_CleanUp/) | Cleanup resources |

## Running the Workshops Outside Skillable

To deliver this session with no Skillable access, please make sure to that the audience has the following requirements adhrered to when completing the lab:

- An Azure subscription - [Create one for free.](https://azure.microsoft.com/free/cognitive-services)
- An Azure AI resource with [GPT-4o and Phi-3.5 model supported in a supported region](https://docs.microsoft.com/en-us/azure/cognitive-services/phi-3-5-models)
- An Azure ML Studio Environment
- An Azure AI Studio Environment
- Visual Studio Code 
- Visual Studio Code Extensions
  - Python
  - Jupyter Notebooks
  - AI Toolkit
  

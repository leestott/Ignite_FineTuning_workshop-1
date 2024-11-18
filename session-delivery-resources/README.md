## How To Use

Welcome,

> [!NOTE]
>This repository contains the resources needed to deliver the session "Fine-Tuning NLP Models with Microsoft Olive" at Microsoft Ignite 2024.
> The following resources are intended for a presenter to learn and deliver the session.

We're glad you are here and look forward to your delivery of this amazing content. As an experienced presenter, we know you know HOW to present so this guide will focus on WHAT you need to present. It will provide you a full run-through of the presentation created by the presentation design team. 

**Abstract:**
Fine-Tuning and Optimizing Models for Travel Applications
In this hands-on session, we will explore the integration of Large Language Models (LLMs) into a travel companion application, leveraging Azure AI Studio and Python. Participants will engage in a comprehensive learning experience that combines both a user-friendly, one-button fine-tuning approach and a code-first methodology for model optimization.

**Session Highlights:**
- **Introduction to LLMs:** Understand the role of LLMs in enhancing travel applications, providing personalized recommendations, and assisting with itinerary planning.
- **Azure AI Studio:** Experience the simplicity of fine-tuning GPT models using Azure AI Studio’s intuitive interface. Learn how to prepare data, initiate one-button fine-tuning, and deploy the model for real-time inference.
- **Code-First Approach:** Dive deeper into the technical aspects of model fine-tuning using Python and Microsoft Olive. Gain hands-on experience in preprocessing data, fine-tuning models, and optimizing performance through pruning and quantization techniques.
Comparison and Evaluation: Analyze the outcomes of both approaches, compare their performance, and evaluate the user experience. Understand the strengths and limitations of Azure AI Studio’s UI versus a code-first approach.
- **Practical Applications:** Deploy and test the fine-tuned models in a real-world travel companion application. Assess the models' accuracy, responsiveness, and ability to provide valuable travel assistance.

By the end of this session, participants will have developed a robust travel application powered by fine-tuned GPT models, optimized for both cloud and local inference. This session will empower participants with the knowledge and skills to choose the best methodologies for their AI projects, combining ease of use and technical precision.


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

The [slides](./PRE016-Ignite2024.pdf) have presenter notes in each part of the session

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

### Scenario

Develop a travel companion application that leverages Large Language Models (LLMs) to provide personalized travel recommendations, itinerary planning, and real-time assistance to travellers. The labs will focus on fine-tuning a GPT model using Azure AI Studio and a code-first approach using Python and Microsoft Olive.

We will focus on the specific areas 
- Setting up Azure AI Studio
- Prepare Training Data
- One-Button Fine-Tuning with Azure AI Studio
- Import a pre-trained model into the project.
- Deploy the Fine-Tuned Model:
- Test the model by querying travel recommendations and itinerary planning.
- Python code to fine-tune GPT model with the prepared data.
- Use Microsoft Olive for model optimization, including pruning and quantization.
- Evaluate the model's performance and compare it with the Azure-deployed model.
- Evaluate which method provided better performance and insights.

**Conclusion:**
By the end of these labs, you'll have a robust travel companion application powered by fine-tuned GPT models, optimized for both cloud and local inference. You'll gain hands-on experience with Azure AI Studio's UI and a code-first approach, enabling you to make informed decisions on the best methodologies for model fine-tuning and deployment.


| Lab # | Title | Description |
| ----- | ------ |----------- |
| 1 | Set up | Learn how to set-up your Azure resources and local environment for this lab. |
| 2 | Data Prep | Learn how to prepare data for Finetuning and evaluation. |
| 3 | Finetuning with Azure AI Studio | Learn how to finetune with Azure AI Studio - both an Azure OpenAI model, and an OSS Model using the Olive CLI. |
| 4 | Deploying models to a cloud endpoint | Learn how to deploy models to a cloud endpoint for inference using Azure AI Studio. |
| 5 | Optimize your model for Inference using Microsoft Olive | Learn to optimize your model for on-device inference using Olive. This will include quantization methods and ONNX runtime optimizations. |
| 6 | How to evaluate AI models | In this lab we show you how to evaluate your models to ensure they give trustworthy and safe responses. |
| 7 | Bring it all together in an app | In this lab we build an application that consumes the AI models you trained and optimized in previous labs. The application will call 2 different models: 1 model will be in the cloud and the other will be on-device. |
| 8 | Clean up | In this lab, we clean up all the resources.


## Running the Workshops Outside Skillable

To deliver this session with no Skillable access, please make sure to that the audience has the following requirements adhrered to when completing the lab:

- An Azure subscription - [Create one for free.](https://azure.microsoft.com/free/cognitive-services)
- An Azure AI resource with [GPT-4o and Phi-3.5 model supported in a supported region](https://docs.microsoft.com/en-us/azure/cognitive-services/phi-3-5-models)
- [An Azure ML Studio Environment](https://ml.azure.com)
- [An Azure AI Studio Environment](https://ai.azure.com)
- [Visual Studio Code](https://code.visualstudio.com/) 
- [Visual Studio Code Extensions](https://marketplace.visualstudio.com/VSCode)
- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
- [AI Toolkit](https://marketplace.visualstudio.com/items?itemName=ms-windows-ai-studio.windows-ai-studio)
- [.NET](http://dot.net/)
- [.NET Aspire](https://learn.microsoft.com/en-us/dotnet/aspire/get-started/aspire-overview)
- [ONNX Runtime GenAI](https://github.com/microsoft/onnxruntime-genai)
  

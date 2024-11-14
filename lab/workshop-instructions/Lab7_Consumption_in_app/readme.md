# Lab 7. Consumption of your Model within an Application 

## Introduction

> [!NOTE]
>This is a **10-minute** workshop that will give you a hands-on introduction to the core concepts of using a code first approach to consuming a deployed model endpoint.

## Learning Objectives

By the end of this workshop, you should be able to:
1. Integrate the custom fined Phi local model with the application.
1. Intergrate the custom fine tuned GPT Model with the application.
2. Compare the results of the models

## Lab Scenario
In this lab you utilise a console application to validate the following scenarios 
1. Chat with and evaliate resulting messages from various models:
- Phi-3.5 Mini Instruct ONNX Model from Hugging Face https://huggingface.co/microsoft/Phi-3.5-mini-instruct-onnx
- Phi-3.5 ONNX unoptizimed fine tuned model  
- Phi-3.5 ONNX OLIVE Optimized fine tuned Model you created in Lab5
- GPT-.3.5 fine tuned Model your created in Lab3
3. Evaluation - this will allow you to compare the resulting messages, speed and quality.
4. Exit the application to complete this lab 

## Setup 

### Create a new folder on the desktop and clone the code using a command prompt.

Open a new Powershell terminal window


> [!NOTE]
> For the Workshop Environment the you should see

``` 
PS C:\Users\LabUser>
```

### Download the solution 

Create a folder for the application on the desktop and clone the solution. 

```
cd desktop
mkdir Application
cd Application
git clone https://github.com/Azure/Ignite_FineTuning_workshop.git
```

### In the application folder navigate to the solution 

Naviagte to the folder 
```
cd Ignite_FineTuning_workshop/lab/workshop-instructions/Lab7_Consumption_in_app/scripts/ChatSLM.Console
```

## Open the solution in VScode 

```
code .
```

## Running fine-tuned GPT model in the cloud 

Go to `ChatWithSLM.Console/Utils/GenAI.cs` add your onnx models path, and save the file.

You ONNX Path will be in the following format


> [!NOTE]
> For the Workshop Environment the we have provide copies of models in the `model`folder located on the desktop 

```
    private static string modelPath = @"/home/azureuser/localfiles/Ignite_FineTuning_workshop/lab/workshop-instructions/Lab7_Consumption_in_app/Phi-3.5-mini-instruct-onnx/cpu_and_mobile/cpu-int4-awq-block-128-acc-level-4";

    private static string oftmodelPath = @"/home/azureuser/localfiles/Ignite_FineTuning_workshop/lab/workshop-instructions/Lab5-Optimize-Model/models/phi/onnx-ao/model;
    private static string oftadapterPath = @"/home/azureuser/localfiles/Ignite_FineTuning_workshop/lab/workshop-instructions/Lab5-Optimize-Model/models/phi/onnx-ao/model/adapter_weights.onnx_adapter";
```
The Azure Open AI Key can be found in deployments and select your deployed GPT-35 Fine Tuned Model +++https://ai.azure.com+++ open the playground select **view code** select curl and then **key authentication** to find the **Endpoint** and **API Key**

```
    Endpoint = "https://*******.openai.azure.com/";
    Key = "********";
    Model Name = "****";

``` 

![location](./images/location.png)


## Running console application


```

dotnet run

```

You can choose two different scenarios

1. Experience of different models based on travel data

2. Experience of models before and after optimization

As shown in the figure


![result](./images/result.png)


### Downloading Additional ONNX Models from Hugging face 

Evaluate using other onnx model 

You can simply download other models to evaluate the output
```
git lfs install
git clone https://huggingface.co/<ModelID>
# Example git clone https://huggingface.co/microsoft/Phi-3.5-mini-instruct-onnx
```

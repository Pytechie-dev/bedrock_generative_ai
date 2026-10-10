# Bedrock Generative AI

This project demonstrates how to use AWS Bedrock to build and test generative AI applications with Amazon foundation models. It includes a set of Jupyter notebooks that cover the core AWS Bedrock APIs, prompt management, RAG patterns, and guardrails.

## Overview

AWS Bedrock is a fully managed service that gives developers access to foundation models from Amazon, Anthropic, Meta, Cohere, and other providers through a single API. Instead of managing infrastructure or model hosting yourself, you can call these models using the Bedrock Runtime and related services.

This repository focuses on practical examples for:

- Calling models with the Bedrock Runtime
- Using the Converse API for chat-style interactions
- Managing prompts and prompt variants
- Building retrieval-augmented generation workflows
- Enforcing application safeguards with Bedrock guardrails

## Repository Contents

- `invoke_model.ipynb` — Basic model invocation using `invoke_model` and `invoke_model_with_response_stream`
- `converse_api.ipynb` — Chat-style generation using the `converse` and `converse_stream` APIs
- `prompt_management.ipynb` — Creating and invoking managed prompts in Amazon Bedrock
- `RAG.ipynb` — Retrieval-augmented generation example using Bedrock Agent Runtime
- `apply_guardrails.ipynb` — Example of applying safety policies and content filtering to model responses

## Prerequisites

Before running the notebooks, make sure you have:

- An AWS account
- Access to Amazon Bedrock in your AWS region
- A user or role with permission to call Bedrock APIs
- Python 3.10+ installed
- AWS CLI configured locally
- Jupyter Notebook or VS Code with notebook support

## Setup

1. Install the required Python packages:

   ```bash
   pip install boto3 jupyter
   ```

2. Configure AWS credentials:

   ```bash
   aws configure
   ```

   Or set environment variables manually:

   ```bash
   export AWS_ACCESS_KEY_ID=your_access_key
   export AWS_SECRET_ACCESS_KEY=your_secret_key
   export AWS_DEFAULT_REGION=us-east-1
   ```

3. Confirm the Bedrock foundation model you want to use is enabled in your AWS account and region.
   For example, models such as `amazon.nova-micro-v1:0` or `amazon.nova-lite-v1:0` may need to be enabled from the Bedrock console.

## Running the Notebooks

Open the repository in Jupyter or VS Code and run the notebooks in the following order:

1. `invoke_model.ipynb`
2. `converse_api.ipynb`
3. `prompt_management.ipynb`
4. `RAG.ipynb`
5. `apply_guardrails.ipynb`

Each notebook contains code examples for a specific Bedrock capability and includes explanations of how the API calls work.

## Example Pattern

The common pattern used in these notebooks is:

```python
import boto3
import json

bedrock_runtime = boto3.client('bedrock-runtime', region_name='us-east-1')
model_id = 'amazon.nova-micro-v1:0'

payload = {
    "inferenceConfig": {"maxTokens": 200, "temperature": 0.7},
    "messages": [{"role": "user", "content": [{"text": "Write a short summary of AWS Bedrock."}]}]
}

response = bedrock_runtime.converse(modelId=model_id, messages=payload['messages'], inferenceConfig=payload['inferenceConfig'])
print(response)
```

This pattern shows how to send prompts to a model, handle model responses, and build them into larger application logic.

## Use Cases Covered

- Text generation and summarization
- Conversational AI applications
- Prompt versioning and reuse
- RAG systems using enterprise knowledge sources
- Safe and policy-aware AI interactions

## Notes

- Bedrock model availability depends on the selected AWS region.
- Some features, such as prompt management and agent runtime tools, may require additional AWS permissions and model access.
- Always follow AWS security best practices when handling credentials, region configuration, and production deployments.

## Recommended Next Steps

- Extend these examples into a web app or API service
- Add application logging and evaluation pipelines
- Combine Bedrock with vector databases for RAG workloads
- Incorporate guardrails and content filtering into production prompts

## Summary

This repo is a hands-on starter pack for learning and experimenting with Amazon Bedrock in Python. It is ideal for developers who want practical examples of modern generative AI integration with AWS services.

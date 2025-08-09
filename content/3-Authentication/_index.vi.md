+++
title = "Amazon Bedrock Guardrails"
date = 2020-05-14T00:38:32+07:00
weight = 3
chapter = false
pre = "<b>3. </b>"
+++

### What is Amazon Bedrock?

Amazon Bedrock is a fully managed service that enables you to build and scale generative AI applications quickly and securely, starting with a foundation model (FM) of your choice. It provides access to a variety of leading FMs from top AI providers through a simple API, without the need to manage infrastructure.

A key feature of Amazon Bedrock is Guardrails, which allows organizations to implement safeguards—referred to as guardrails—that monitor and control both user inputs and AI-generated outputs. These safeguards help ensure that the AI behavior aligns with your organization’s policies and ethical standards. Guardrails are model-agnostic and can be integrated across various use cases and applications.

### What is Guardrails for Amazon Bedrock?

Guardrails for Amazon Bedrock is a powerful feature that enables you to establish safety controls within your generative AI applications. Guardrails help filter, block, or manage content that may be considered harmful, inappropriate, or misaligned with your organization’s policies.

These safeguards work across different foundation models and are designed to ensure responsible use of AI by checking both user inputs and AI outputs. In future updates, Guardrails will also support automatic redaction of personally identifiable information (PII)—further enhancing content safety and privacy.

With Guardrails, you can configure and enforce policies such as:

- **Denied Topics:** Specify topics that are not allowed within your application.
  Example: A virtual banking assistant can be restricted from giving investment advice.

- **Content Filters:** Set thresholds to detect and filter content related to: Hate speech, Insults, Sexual content, Violence,...

![Guardrails](/images/2/Guardrails.png?width=90pc)

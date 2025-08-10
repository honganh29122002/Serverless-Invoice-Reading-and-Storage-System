+++
title = "Serverless Invoice Reading and Storage System"
date = 2020-05-14T00:38:32+07:00
weight = 1
chapter = false
+++

# Serverless Invoice Reading and Storage System
## Overview

The system represents a fully serverless and highly scalable architecture built entirely on AWS cloud services, designed to securely manage user access, handle backend logic, and store data efficiently. At the entry point, **Amazon Route 53** is responsible for DNS resolution, directing client requests to the appropriate endpoint. These requests are then passed to **Amazon API Gateway**, which acts as the centralized interface for all external interactions with the backend. API Gateway not only handles the routing of requests but also enforces security by integrating with **Amazon Cognito** for user authentication and authorization.

Once a user is authenticated, API Gateway forwards the request to specific AWS Lambda functions that contain the core business logic of the application. For example, the **scan_lambda** function may be responsible for validating, scanning, or preprocessing user inputs, while the **savePicture** function handles more complex data processing and uploads results to **Amazon S3**. Amazon S3 serves as the system's persistent storage layer, offering high durability, availability, and secure access to stored data. The entire system is event-driven, cost-efficient, and capable of scaling automatically based on demand, making it ideal for modern applications that require high availability, low operational overhead, and strong security controls. Additionally, with built-in monitoring, logging, and metrics provided by AWS services like CloudWatch, the system ensures visibility and maintainability across all components without requiring manual server management or infrastructure provisioning.

![architecture](/images/1/architecture.png?width=90pc)

## Target

- **No server management** – The system scales automatically and is managed without needing to maintain servers.

- **High security** – Ensures only authorized users can access services.

- **Cost optimization** – Pay-as-you-go pricing, with no fixed infrastructure costs.

- **High performance** – Quick processing and automatic adjustment based on traffic volume.

- **Easy integration** – AWS services work seamlessly together, simplifying development and operations.

## Workshop Structure

This workshop is organized into the following sections to guide you through building a complete serverless invoice processing system:

[1. Introduction](1-introduction/)

[2. Frontend](2-frontend/)

[3. Authentication](3-authentication/)


[4. Storage & Database](4-storage-db/)


[5. Document AI](5-document-ai/)


[6. Lambda Functions](6-lambda/)


[7. API Gateway](7-api-gateway/)


[8. Testing](8-testing/)


[9. Delete Source](9-delete-source/)

[10. Conclusion](10-conclusion/)

---

## Getting Started

To begin this workshop, click on **[Introduction](1-introduction/)** or use the navigation menu on the left to proceed through each section step by step.

{{% notice tip %}}
Make sure you have an AWS account with appropriate permissions before starting this workshop.
{{% /notice %}}
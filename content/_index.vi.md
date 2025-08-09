+++
title = "Invoices Serverless"
date = 2024
weight = 1
chapter = false
+++

# Invoices Serverless
#### Overview
The system represents a fully serverless and highly scalable architecture built entirely on AWS cloud services, designed to securely manage user access, handle backend logic, and store data efficiently. At the entry point, **Amazon Route 53** is responsible for DNS resolution, directing client requests to the appropriate endpoint. These requests are then passed to **Amazon API Gateway**, which acts as the centralized interface for all external interactions with the backend. API Gateway not only handles the routing of requests but also enforces security by integrating with **Amazon Cognito** for user authentication and authorization.

Once a user is authenticated, API Gateway forwards the request to specific AWS Lambda functions that contain the core business logic of the application. For example, the **scan_lambda** function may be responsible for validating, scanning, or preprocessing user inputs, while the **savePicture** function handles more complex data processing and uploads results to **Amazon S3**. Amazon S3 serves as the system’s persistent storage layer, offering high durability, availability, and secure access to stored data. The entire system is event-driven, cost-efficient, and capable of scaling automatically based on demand, making it ideal for modern applications that require high availability, low operational overhead, and strong security controls. Additionally, with built-in monitoring, logging, and metrics provided by AWS services like CloudWatch, the system ensures visibility and maintainability across all components without requiring manual server management or infrastructure provisioning.
![architecture](/images/1/architecture.png?width=90pc)  

#### Target
- No server management – The system scales automatically and is managed without needing to maintain servers.

- High security – Ensures only authorized users can access services.

- Cost optimization – Pay-as-you-go pricing, with no fixed infrastructure costs.

- High performance – Quick processing and automatic adjustment based on traffic volume.

- Easy integration – AWS services work seamlessly together, simplifying development and operations.

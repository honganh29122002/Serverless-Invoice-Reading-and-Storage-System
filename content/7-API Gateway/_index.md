+++
title = "API Gateway Configuration"
date = 2020-05-14T00:38:32+07:00
weight = 7
chapter = false
pre = "<b>7. </b>"
+++

This section covers the setup of API Gateway to create secure, scalable REST APIs that connect the frontend application with backend Lambda functions.

## API Gateway Overview

### Core Functions

**1. Request Management**
- Acts as the single entry point for all client requests
- Manages communication between frontend and backend services
- Provides centralized request/response handling

**2. Request Routing**
- Routes HTTP/HTTPS requests to appropriate backend services
- Directs requests to specific Lambda functions based on endpoints
- Supports multiple integration types (Lambda, HTTP, AWS services)

**3. Security Integration**
- Integrates with Amazon Cognito for authentication
- Supports OAuth2 and custom authorization
- Provides API key management and throttling

### Architecture Role

In our serverless architecture, API Gateway serves as the orchestration layer:
- Receives requests from the frontend application
- Routes scan requests to the **scan_lambda** function
- Directs upload requests to the **savePicture** function
- Manages authentication through Cognito integration

## API Configuration

### Image Storage and Processing API

#### Step 1: Create REST API

1. Navigate to the [Amazon API Gateway Console](https://ap-southeast-1.console.aws.amazon.com/apigateway/main/welcome?api=unselected&region=ap-southeast-1)

   ![api1](/images/7/api1.png?width=90pc)

2. Create new API
   - Select **REST API**

   ![api2](/images/7/api2.png?width=90pc)
   - Enter **API name** and **Create**
   ![api3](/images/7/api3.png?width=90pc)

#### Step 2: Create Upload Resource

1. Create new **resource**
   
   ![api4](/images/7/api4.png?width=90pc)
   - **Resource name**: Enter descriptive name
   - **Enable CORS**: Check this option
  
   ![api5](/images/7/api5.png?width=90pc)

#### Step 3: Create Dynamic Path Resource

1. Create **child resource**
   - **Resource name**: `{filename}`
   - **Enable CORS**: Check this option

   ![api6](/images/7/api6.png?width=90pc)

#### Step 4: Configure POST Method

1. Create method for file upload

   ![api7](/images/7/api7.png?width=90pc)
   - **Method type**: POST
   - **Lambda Proxy Integration**: Enable
   - **Lambda function**: Select S3 upload handler function
  
   ![api8](/images/7/api8.png?width=90pc)

#### Step 5: Configure Response Headers

1. Set response configuration
   - **Response headers**: `Access-Control-Allow-Origin`
   - **Response body**: `application/json`

   ![api9](/images/7/api9.png?width=90pc)

#### Step 6: Configure Media Types

1. Access **API settings**

   ![api10](/images/7/api10.png?width=90pc)
2. Add **media type** for file uploads
   ![api11](/images/7/api11.png?width=90pc)

### Data Retrieval API

#### Step 1: Create View Resource

1. Create new resource for data retrieval

   ![api12](/images/7/api12.png?width=90pc)
   - **Resource name**: `view-all`
   - **Enable CORS**: Check this option
   - **Create**
   ![api13](/images/7/api13.png?width=90pc)

#### Step 2: Configure GET Method

1. Create method for data retrieval

   ![api14](/images/7/api14.png?width=90pc)
   - **Method type**: GET
   - **Lambda Proxy Integration**: Enable
   - **Lambda function**: Select DynamoDB scanner function
  
   ![api15](/images/7/api15.png?width=90pc)

#### Step 3: Deploy API

1. Deploy the API to make it accessible

   ![api16](/images/7/api16.png?width=90pc)
2. **Important**: Save the deployment URL for frontend integration
   ![api17](/images/7/api17.png?width=90pc)

## Best Practices

### Security
- Always enable CORS for cross-origin requests
- Implement proper authentication and authorization
- Use API keys for additional access control

### Performance
- Enable caching for frequently accessed endpoints
- Configure appropriate throttling limits
- Monitor API usage and performance metrics

### Monitoring
- Set up CloudWatch logging for debugging
- Configure alarms for error rates and latency
- Use AWS X-Ray for distributed tracing

---

## Continue to

[8. Testing](../8-testing/)
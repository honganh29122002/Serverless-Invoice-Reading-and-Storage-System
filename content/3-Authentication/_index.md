+++
title = "Authentication"
date = 2020-05-14T00:38:32+07:00
weight = 3
chapter = false
pre = "<b>3. </b>"
+++


### What is Amazon Cognito?

Amazon Cognito serves as the central authentication and user management service within AWS-based systems, ensuring secure access control to backend resources such as Lambda functions and S3 storage.

### Amazon Cognito Configuration

### Step 1: Create User Pool

1. Navigate to the [Amazon Cognito Console](https://us-east-1.console.aws.amazon.com/cognito/v2/home?region=us-east-1)
2. Click **Create User Pool**

### Step 2: Configure Application Settings

- **Application type**: Single-page application
- **Application name**: Enter your application name
- **Sign-in options**: Username
- **Return URL**: Enter your application URL

   ![cog1](/images/3/cog1.png?width=90pc)
   ![cog2](/images/3/cog2.png?width=90pc)
   ![cog3](/images/3/cog3.png?width=90pc)

### Step 3: Access Login Interface

- Review the hosted login page configuration
- Test the login interface

   ![cog4](/images/3/cog4.png?width=90pc)

### Step 4: Save Configuration Details

**Important**: Record the following values for application integration:
- **User Pool ID**
- **Client ID**

   ![cog5](/images/3/cog5.png?width=90pc)
   ![cog6](/images/3/cog6.png?width=90pc)

### Step 5: Create Test User Account

1. Create a new user account for testing
2. Complete the registration process

   ![cog7](/images/3/cog7.png?width=90pc)
   ![cog8](/images/3/cog8.png?width=90pc)

### Step 6: Verify Authentication

1. Log in using the created credentials
2. Verify successful authentication

   ![cog9](/images/3/cog9.png?width=90pc)
   ![cog10](/images/3/cog10.png?width=90pc)
   ![cog11](/images/3/cog11.png?width=90pc)

### Step 7: Confirm User Status

- Verify the user status shows as **Confirmed**
- User is now ready for application access

   ![cog12](/images/3/cog12.png?width=90pc)

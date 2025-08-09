+++
title = "Resource Cleanup"
date = 2024-08-19T00:38:32+07:00
weight = 9
chapter = false
pre = "<b>9. </b>"
+++

This section provides a comprehensive guide for cleaning up all AWS resources created during the workshop to avoid unnecessary charges.


## Cleanup Checklist

### Phase 1: Application Layer Cleanup

#### 1. AWS Amplify
- **Action**: Delete the Amplify application
- **Steps**:
  1. Navigate to AWS Amplify Console
  2. Select your application
  3. Go to **Actions** → **Delete app**
  4. Confirm deletion by typing the app name
    ![cl6](/images/9/cl6.png?width=90pc)

#### 2. Amazon Route 53
- **Action**: Delete hosted zone and records
- **Steps**:
  1. Navigate to Route 53 Console
  2. Delete all custom records (keep NS and SOA for last)
  3. Delete the hosted zone
  4. Update domain registrar DNS settings (if applicable)
  ![cl7](/images/9/cl7.png?width=90pc)

### Phase 2: API and Compute Cleanup

#### 1. Amazon API Gateway
- **Action**: Delete REST API
- **Steps**:
  1. Navigate to API Gateway Console
  2. Select your API
  3. Go to **Actions** → **Delete API**
  4. Confirm deletion
   ![cl4](/images/9/cl4.png?width=90pc)

#### 2. AWS Lambda Functions
- **Action**: Delete all Lambda functions
- **Steps**:
  1. Navigate to Lambda Console
  2. Delete each function individually:
     - Database scanner function
     - Image upload handler function
     - Textract integration function
     - Bedrock integration function
  3. Verify all functions are removed
   ![cl5](/images/9/cl5.png?width=90pc)

### Phase 3: Storage and Database Cleanup

#### 1. Amazon S3
- **Action**: Empty and delete S3 buckets
- **Steps**:
  1. Navigate to S3 Console
  2. **Empty the bucket first**:
     - Select bucket → **Empty**
     - Type "permanently delete" to confirm
  3. **Delete the bucket**:
     - Select bucket → **Delete**
     - Type bucket name to confirm
  ![cl2](/images/9/cl2.png?width=90pc)
  ![cl2](/images/9/cl2-.png?width=90pc)
  ![cl2](/images/9/cl2--.png?width=90pc)
  

#### 2. Amazon DynamoDB
- **Action**: Delete DynamoDB tables
- **Steps**:
  1. Navigate to DynamoDB Console
  2. Select your table
  3. Go to **Actions** → **Delete table**
  4. Type "delete" to confirm
  5. Wait for deletion to complete
   ![cl1](/images/9/cl1.png?width=90pc)

### Phase 4: Identity Cleanup

#### Amazon Cognito
- **Action**: Delete User Pool
- **Steps**:
  1. Navigate to Cognito Console
  2. Select your User Pool
  3. Go to **Actions** → **Delete user pool**
  4. Type "delete" to confirm
   ![cl3](/images/9/cl3.png?width=90pc)

### Phase 5: Monitoring and Logging Cleanup

#### CloudWatch Logs
- **Action**: Delete log groups
- **Steps**:
  1. Navigate to CloudWatch Console
  2. Go to **Logs** → **Log groups**
  3. Delete Lambda function log groups
  4. Delete API Gateway log groups

---

**Important**: Double-check all deletions before confirming. Resource deletion is typically irreversible and may result in permanent data loss.
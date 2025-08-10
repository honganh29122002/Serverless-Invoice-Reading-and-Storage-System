+++
title = "Application Testing"
date = 2020-05-14T00:38:32+07:00
weight = 8
chapter = false
pre = "<b>8. </b>"
+++


This section covers comprehensive testing procedures to validate the functionality of the serverless invoice processing system.

## Testing Procedures

### Step 1: Authentication Testing

**Test Case 1.1: Invalid Login Attempt**
1. Try logging in with wrong account

   ![test](/images/8/test1.png?width=90pc)

**Test Case 1.2: Valid Login Attempt**

2. Try logging in with the correct account

   ![test](/images/8/test2.png?width=90pc)

### Step 2: File Upload Testing



1. Select data as invoice image with extension **.png**

   ![test](/images/8/test3.png?width=90pc)
   ![test](/images/8/test4.png?width=90pc)



2. Upload image

   ![test](/images/8/test5.png?width=90pc)

### Step 3: Storage Verification



1. Check s3 bucket and see the photo uploaded

   ![test](/images/8/test6.png?width=90pc)


2. Check lambda log to see data saved to DynamoDB successfully

   ![test](/images/8/test8.png?width=90pc)
   ![test](/images/8/test9.png?width=90pc)


3. Check table in **DynamoDB**

   ![test](/images/8/test7.png?width=90pc)

### Step 4: Data Retrieval Testing

1. Try viewing the data stored in the dynamo via the frontend

   ![test](/images/8/test10.png?width=90pc)

### Step 5: Multiple Upload Testing

1. Continue uploading another invoice and it was also successful.

   ![test](/images/8/test11.png?width=90pc)
   ![test](/images/8/test12.png?width=90pc)
   ![test](/images/8/test13.png?width=90pc)

---

## Continue to

[9. Cleanup](../9-delete-source/)

---

## References

- [AWS Testing Best Practices](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/testing.html)
- [API Gateway Testing](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-testing.html)
- [Lambda Function Testing](https://docs.aws.amazon.com/lambda/latest/dg/testing-debugging.html)
+++
title = "Storage and Database Configuration"
date = 2024-05-14T00:38:32+07:00
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

This section covers the setup of data storage components including DynamoDB for structured data and S3 for file storage.

## Amazon DynamoDB Configuration

### Step 1: Access DynamoDB Console

1. Navigate to the [DynamoDB Console](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#service)

   ![db1](/images/4/db1.png?width=90pc)

### Step 2: Create New Table

1. Click **Create table**
2. Configure table settings

   ![db2](/images/4/db2.png?width=90pc)

### Step 3: Define Table Schema

- **Table name**: Enter descriptive table name
- **Partition key**: Define primary key attribute
- **Sort key**: Configure secondary key (if required)

   ![db3](/images/4/db3.png?width=90pc)
   ![db4](/images/4/db4.png?width=90pc)

### Step 4: Save Table Configuration

- Verify table creation success
- **Important**: Record the table ARN for Lambda function configuration

   ![db5](/images/4/db5.png?width=90pc)

## Amazon S3 Configuration

### Step 1: Access S3 Console

1. Navigate to the [S3 Console](https://s3.console.aws.amazon.com/s3/home?region=ap-southeast-1)

   ![s3-1](/images/4/s3-1.png?width=90pc)

### Step 2: Create S3 Bucket

1. Click **Create bucket**
2. Configure bucket settings

   ![s3-2](/images/4/s3-2.png?width=90pc)

### Step 3: Configure Bucket Properties

- **Bucket name**: Enter unique bucket name
- **Region**: Select appropriate AWS region
- **Access settings**: Configure according to security requirements

   ![s3-3](/images/4/s3-3.png?width=90pc)

### Step 4: Save Bucket Configuration

- Verify bucket creation success
- **Important**: Record the bucket ARN for Lambda function and application configuration

   ![s3-4](/images/4/s3-4.png?width=90pc)

---

## Continue to

[5. Document AI](../5-document-ai/)

---

## References

- [Amazon DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/)
- [Amazon S3 User Guide](https://docs.aws.amazon.com/s3/)
- [DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)

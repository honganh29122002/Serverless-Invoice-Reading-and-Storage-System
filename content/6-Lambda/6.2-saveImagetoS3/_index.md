+++
title = "Save Picture to S3"
date = 2024-05-14T00:38:32+07:00
weight = 2
chapter = false
pre = "<b>6.2 </b>"
+++

#### Lambda configuration

- Access to [Amazon Lambda Console](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions)
   ![lambda1](/images/6/lambda1.png?width=90pc)

- Create a new function:
  - Function name
  - Run time: **Python 3.12**
  - Architecture: **x86_64**
  - IAM Role name
   ![lambda9](/images/6/lambda9.png?width=90pc)
   ![lambda10](/images/6/lambda10.png?width=90pc)
   - Enter the following code
   ![lambda10-](/images/6/lambda10-.png?width=90pc)

```python
import boto3
import base64
import os

s3 = boto3.client("s3")
BUCKET_NAME = "invoicebuckett123"

def lambda_handler(event, context):
    # Xử lý CORS preflight (OPTIONS request)
    if event["httpMethod"] == "OPTIONS":
        return {
            "statusCode": 200,
            "headers": {
                "Access-Control-Allow-Origin": "*",  # hoặc domain cụ thể nếu bạn muốn
                "Access-Control-Allow-Methods": "POST,OPTIONS",
                "Access-Control-Allow-Headers": "Content-Type,Authorization",
            },
            "body": ""
        }

    try:
        file_name = event["pathParameters"]["filename"]
        content_type = event["headers"].get("Content-Type") or event["headers"].get("content-type", "application/octet-stream")
        file_content = base64.b64decode(event["body"])

        s3.put_object(
            Bucket=BUCKET_NAME,
            Key=file_name,
            Body=file_content,
            ContentType=content_type,
        )

        return {
            "statusCode": 200,
            "headers": {
                "Access-Control-Allow-Origin": "*",  # hoặc domain cụ thể
                "Access-Control-Allow-Methods": "POST,OPTIONS",
                "Access-Control-Allow-Headers": "Content-Type,Authorization",
            },
            "body": f"File '{file_name}' uploaded successfully to S3."
        }

    except Exception as e:
        return {
            "statusCode": 500,
            "headers": {
                "Access-Control-Allow-Origin": "*",
                "Access-Control-Allow-Methods": "POST,OPTIONS",
                "Access-Control-Allow-Headers": "Content-Type,Authorization",
            },
            "body": f"Upload failed: {str(e)}"
        }
```

#### Lambda IAM Role
- Access to IAM Role and add **policy**
   ![lambda11](/images/6/lambda11.png?width=90pc)
   ![lambda12](/images/6/lambda12.png?width=90pc)
```js
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::<YOUR-BUCKET-NAME>/*"
        }
    ]
}
```
---
**Continue to**:
[6.3 Interact with textract](../6.3-withTextract/)
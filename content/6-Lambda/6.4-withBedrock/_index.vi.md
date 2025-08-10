+++
title = "Tương Tác Với Bedrock"
date = 2024-05-14T00:38:32+07:00
weight = 4
chapter = false
pre = "<b>6.4 </b>"
+++

#### Cấu hình Lambda

- Truy cập [Amazon Lambda Console](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions)
  ![lambda1](/images/6/lambda1.png?width=90pc)

- Tạo function mới:
  - Tên function
  - Run time: **Python 3.12**
  - Architecture: **x86_64**
  - Tên IAM Role
   ![lambda16](/images/6/lambda16.png?width=90pc)
   ![lambda17](/images/6/lambda17.png?width=90pc)
   ![lambda18](/images/6/lambda18.png?width=90pc)
    - Nhập code sau đây
    ![lambda18-](/images/6/lambda18-.png?width=90pc)
```python
import boto3
import json

bedrock = boto3.client('bedrock-runtime')

def invoke_bedrock(form_data):
    prompt = f"""
Dưới đây là dữ liệu biểu mẫu hóa đơn bán lẻ đã được Textract trích xuất:

{json.dumps(form_data, indent=2)}

Hãy phân tích và trả về một JSON với cấu trúc sau:

{{
  "invoice_id": string, 
  "invoice_date": string,
  "cashier": string,
  "counter": string,
  "total_amount": number,
  "discount": number,
  "customer_paid": number,
  "change": number,
  "payment_method": string,
  "items": [
    {{
      "name": string,
      "unit_price": number
    }} 
    ...
  ]
}}

Chỉ trả về đúng một chuỗi JSON hợp lệ.
"""

    try:
        # Gửi yêu cầu tới mô hình Bedrock
        response = bedrock.invoke_model(
            modelId="anthropic.claude-3-haiku-20240307-v1:0",
            contentType="application/json",
            accept="application/json",
            body=json.dumps({
                "anthropic_version": "bedrock-2023-05-31",
                "messages": [
                    {
                        "role": "user",
                        "content": prompt
                    }
                ],
                "max_tokens": 1024,
                "temperature": 0.3
            })
        )

        raw_output = json.loads(response['body'].read())
        print("Raw output from Claude:", raw_output)

        messages = raw_output.get("content", [])
        if isinstance(messages, list) and len(messages) > 0:
            text_content = messages[0].get("text", "")
            start_index = text_content.find("{")
            end_index = text_content.rfind("}") + 1
            if start_index != -1 and end_index != -1:
                json_string = text_content[start_index:end_index]
                # Trả về JSON hợp lệ
                return json.loads(json_string)
            else:
                print("Không tìm thấy JSON trong phản hồi từ Claude.")
                return {"error": "No valid JSON found in Claude response", "data": text_content}
        else:
            print("Claude trả về dữ liệu không hợp lệ.")
            return {"error": "Invalid response from Claude"}
    
    except Exception as e:
        print(f"Error invoking Bedrock: {str(e)}")
        return {"error": "Error invoking Bedrock", "message": str(e)}

def lambda_handler(event, context):
    print("Lambda B triggered")

    # Lấy dữ liệu form_data từ event
    form_data = event.get("form_data", {})
    
    # Nếu form_data không có, trả về lỗi ngay lập tức
    if not form_data:
        return {"error": "No form data provided"}
    
    # Gọi hàm invoke_bedrock để lấy kết quả từ mô hình Claude
    summary = invoke_bedrock(form_data)
    
    # In ra kết quả từ Claude (nếu có)
    print("Claude summary:", summary)
    
    return summary
```

#### IAM Role
- Truy cập IAM Role và thêm policy
   ![lambda19](/images/6/lambda19.png?width=90pc)
   ![lambda20](/images/6/lambda20.png?width=90pc)
```js
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "bedrock:InvokeModel"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "textract:AnalyzeDocument",
                "textract:DetectDocumentText",
                "textract:GetDocumentAnalysis",
                "textract:GetDocumentTextDetection"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "lambda:InvokeFunction",
            "Resource": "arn:aws:lambda:<YOUR-REGION>:<YOUR-ACCOUNT-ID>:function:lambdaToTextract"
        },
        {
            "Effect": "Allow",
            "Action": [
                "dynamodb:PutItem",
                "dynamodb:BatchWriteItem",
                "dynamodb:UpdateItem",
                "dynamodb:Query",
                "dynamodb:GetItem"
            ],
            "Resource": "arn:aws:dynamodb:<YOUR-REGION>:<YOUR-ACCOUNT-ID>:table/YOUR_TABLE_NAME"
        }
    ]
}
```

 ---
**Tiếp tục**:
[7. Cấu Hình API Gateway](../../7-API%20Gateway/)
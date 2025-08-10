+++
title = "Get Data From DB"
date = 2024-05-14T00:38:32+07:00
weight = 1
chapter = false
pre = "<b>6.1 </b>"
+++

#### Lambda configuration

- Access to [Amazon Lambda Console](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions)
   ![lambda1](/images/6/lambda1.png?width=90pc)

- Create a new function:
  - Function name
  - Run time: **Python 3.12**
  - Architecture: **x86_64**
  - IAM Role name
    ![lambda2](/images/6/lambda2.png?width=90pc)
    ![lambda3](/images/6/lambda3.png?width=90pc)
    ![lambda4](/images/6/lambda4.png?width=90pc)
  - Enter the following code
  - ![lambda4-](/images/6/lambda4-.png?width=90pc)

```python
import json
import boto3
import logging

# Cấu hình logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger()

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('InvoicesTable')

def format_invoice_text(invoice):
    """Chuyển đổi thông tin hóa đơn thành định dạng văn bản dễ đọc"""
    formatted_text = []
    formatted_text.append(f"<h2>Mã hóa đơn: {invoice.get('InvoiceID')}</h2>")
    formatted_text.append(f"<p><strong>Ngày:</strong> {invoice.get('InvoiceDate')}</p>")
    formatted_text.append(f"<p><strong>Thu ngân:</strong> {invoice.get('Cashier')}</p>")
    formatted_text.append(f"<p><strong>Quầy:</strong> {invoice.get('Counter')}</p>")
    formatted_text.append(f"<p><strong>Phương thức thanh toán:</strong> {invoice.get('PaymentMethod')}</p>")
    formatted_text.append(f"<p><strong>Khách đưa:</strong> {invoice.get('CustomerPaid')}</p>")
    formatted_text.append(f"<p><strong>Tổng tiền:</strong> {invoice.get('TotalAmount')}</p>")
    formatted_text.append(f"<p><strong>Chiết khấu:</strong> {invoice.get('Discount')}</p>")
    formatted_text.append(f"<p><strong>Tiền thối:</strong> {invoice.get('Change')}</p>")
    
    # Danh sách sản phẩm
    items = invoice.get("Items", [])
    if items:
        formatted_text.append("<h3>Danh sách sản phẩm:</h3>")
        formatted_text.append("<table border='1' cellpadding='5' cellspacing='0'>")
        formatted_text.append("<tr><th>#</th><th>Tên sản phẩm</th><th>Số lượng</th><th>Đơn giá</th><th>Thành tiền</th></tr>")
        for idx, item in enumerate(items, 1):
            name = item.get("name") or "Không rõ"
            quantity = item.get("quantity") or "Không rõ"
            unit_price = item.get("unit_price") or "Không rõ"
            total_price = item.get("total_price") or "Không rõ"
            formatted_text.append(f"<tr><td>{idx}</td><td>{name}</td><td>{quantity}</td><td>{unit_price}</td><td>{total_price}</td></tr>")
        formatted_text.append("</table>")

    return "".join(formatted_text)


def lambda_handler(event, context):
    try:
        logger.info("Bắt đầu xử lý yêu cầu.")

        # Truy xuất toàn bộ dữ liệu từ bảng
        logger.info("Truy xuất dữ liệu từ DynamoDB.")
        response = table.scan()
        items = response.get('Items', [])
        
        logger.info(f"Số lượng hóa đơn lấy được: {len(items)}")

        if not items:
            logger.warning("Không có dữ liệu hóa đơn.")
            return {
                'statusCode': 404,
                'headers': {
                    'Access-Control-Allow-Origin': '*',
                    'Access-Control-Allow-Headers': '*'
                },
                'body': json.dumps({"message": "Không có dữ liệu hóa đơn."})
            }

        # Định dạng dữ liệu thành dạng HTML
        formatted_result = "<div>" + "".join([format_invoice_text(invoice) for invoice in items]) + "</div>"

        logger.info("Hoàn thành việc xử lý dữ liệu và định dạng thành HTML.")

        return {
            'statusCode': 200,
            'headers': {
                'Access-Control-Allow-Origin': '*',
                'Access-Control-Allow-Headers': '*'
            },
            'body': json.dumps({"formatted_result": formatted_result})
        }

    except Exception as e:
        logger.error(f"Lỗi khi xử lý yêu cầu: {str(e)}")
        return {
            'statusCode': 500,
            'headers': {
                'Access-Control-Allow-Origin': '*',
                'Access-Control-Allow-Headers': '*'
            },
            'body': json.dumps({'error': str(e)})
        }
```

#### Lambda IAM Role
- Access to IAM Role and add **policy**
    ![lambda5](/images/6/lambda5.png?width=90pc)
    ![lambda6](/images/6/lambda6.png?width=90pc)
- Policy:
  ```js
  {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "dynamodb:GetItem",
                "dynamodb:Query",
                "dynamodb:Scan",
                "dynamodb:BatchWriteItem"
            ],
            "Resource": "arn:aws:dynamodb:<YOUR-REGION>:<YOUR-ACCOUNT-ID>:table/<YOUR-NAME-TABLE>"
        }
    ]
   }
  ```
    ![lambda7](/images/6/lambda7.png?width=90pc)
    ![lambda8](/images/6/lambda8.png?width=90pc)


    ---

    **Continue to**:
    [6.2 Save picture to S3](../6.2-saveImagetoS3/)
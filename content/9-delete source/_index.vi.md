+++
title = "Dọn Dẹp Tài Nguyên"
date = 2024-08-19T00:38:32+07:00
weight = 9
chapter = false
pre = "<b>9. </b>"
+++

Phần này cung cấp hướng dẫn toàn diện để dọn dẹp tất cả các tài nguyên AWS được tạo trong workshop để tránh các khoản phí không cần thiết.

## Danh Sách Kiểm Tra Dọn Dẹp

### Giai Đoạn 1: Dọn Dẹp Lớp Ứng Dụng

#### 1. AWS Amplify
- **Hành động**: Xóa ứng dụng Amplify
- **Các bước**:
  1. Điều hướng đến AWS Amplify Console
  2. Chọn ứng dụng của bạn
  3. Đi đến **Actions** → **Delete app**
  4. Xác nhận xóa bằng cách nhập tên app
    ![cl6](/images/9/cl6.png?width=90pc)

#### 2. Amazon Route 53
- **Hành động**: Xóa hosted zone và records
- **Các bước**:
  1. Điều hướng đến Route 53 Console
  2. Xóa tất cả custom records (giữ NS và SOA cuối cùng)
  3. Xóa hosted zone
  4. Cập nhật cài đặt DNS của domain registrar (nếu có)
  ![cl7](/images/9/cl7.png?width=90pc)

### Giai Đoạn 2: Dọn Dẹp API và Compute

#### 1. Amazon API Gateway
- **Hành động**: Xóa REST API
- **Các bước**:
  1. Điều hướng đến API Gateway Console
  2. Chọn API của bạn
  3. Đi đến **Actions** → **Delete API**
  4. Xác nhận xóa
   ![cl4](/images/9/cl4.png?width=90pc)

#### 2. AWS Lambda Functions
- **Hành động**: Xóa tất cả hàm Lambda
- **Các bước**:
  1. Điều hướng đến Lambda Console
  2. Xóa từng hàm một cách riêng lẻ:
     - Hàm database scanner
     - Hàm xử lý upload hình ảnh
     - Hàm tích hợp Textract
     - Hàm tích hợp Bedrock
  3. Xác minh tất cả hàm đã được xóa
   ![cl5](/images/9/cl5.png?width=90pc)

### Giai Đoạn 3: Dọn Dẹp Lưu Trữ và Cơ Sở Dữ Liệu

#### 1. Amazon S3
- **Hành động**: Làm trống và xóa S3 buckets
- **Các bước**:
  1. Điều hướng đến S3 Console
  2. **Làm trống bucket trước**:
     - Chọn bucket → **Empty**
     - Nhập "permanently delete" để xác nhận
  ![cl2](/images/9/cl2.png?width=90pc)
  3. **Xóa bucket**:
     - Chọn bucket → **Delete**
  ![cl2](/images/9/cl2-.png?width=90pc)
     - Nhập tên bucket để xác nhận và **delete bucket**
  ![cl2](/images/9/cl2--.png?width=90pc)

#### 2. Amazon DynamoDB
- **Hành động**: Xóa bảng DynamoDB
- **Các bước**:
  1. Điều hướng đến DynamoDB Console
  2. Chọn bảng của bạn
  3. Đi đến **Actions** → **Delete table**
  4. Nhập "delete" để xác nhận
  5. Đợi việc xóa hoàn tất
   ![cl1](/images/9/cl1.png?width=90pc)

### Giai Đoạn 4: Dọn Dẹp Identity

#### Amazon Cognito
- **Hành động**: Xóa User Pool
- **Các bước**:
  1. Điều hướng đến Cognito Console
  2. Chọn User Pool của bạn
  3. Đi đến **Actions** → **Delete user pool**
  4. Nhập "delete" để xác nhận
   ![cl3](/images/9/cl3.png?width=90pc)

### Giai Đoạn 5: Dọn Dẹp Giám Sát và Logging

#### CloudWatch Logs
- **Hành động**: Xóa log groups
- **Các bước**:
  1. Điều hướng đến CloudWatch Console
  2. Đi đến **Logs** → **Log groups**
  3. Xóa log groups của hàm Lambda
  4. Xóa log groups của API Gateway

---

**Quan trọng**: Kiểm tra kỹ tất cả việc xóa trước khi xác nhận. Việc xóa tài nguyên thường không thể hoàn tác và có thể dẫn đến mất dữ liệu vĩnh viễn.

---

## Tiếp tục

[10. Kết Luận](../10-conclusion/)

---

## Tài Liệu Tham Khảo

- [AWS Resource Cleanup Best Practices](https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-pillar/decommission-resources.html)
- [AWS Cost Management](https://aws.amazon.com/aws-cost-management/)
- [AWS Billing and Cost Management User Guide](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/)
+++
title = "Cấu Hình Lưu Trữ và Cơ Sở Dữ Liệu"
date = 2024-05-14T00:38:32+07:00
weight = 4
chapter = false
pre = "<b>4. </b>"
+++

Phần này bao gồm việc thiết lập các thành phần lưu trữ dữ liệu bao gồm DynamoDB cho dữ liệu có cấu trúc và S3 cho lưu trữ file.

## Cấu Hình Amazon DynamoDB

### Bước 1: Truy Cập DynamoDB Console

1. Điều hướng đến [DynamoDB Console](https://ap-southeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-southeast-1#service)

   ![db1](/images/4/db1.png?width=90pc)

### Bước 2: Tạo Bảng Mới

1. Nhấp **Create table**
2. Cấu hình cài đặt bảng

   ![db2](/images/4/db2.png?width=90pc)

### Bước 3: Định Nghĩa Schema Bảng

- **Tên bảng**: Nhập tên bảng mô tả
- **Partition key**: Định nghĩa thuộc tính khóa chính
- **Sort key**: Cấu hình khóa phụ (nếu cần)

   ![db3](/images/4/db3.png?width=90pc)
   ![db4](/images/4/db4.png?width=90pc)

### Bước 4: Lưu Cấu Hình Bảng

- Xác minh việc tạo bảng thành công
- **Quan trọng**: Ghi lại ARN của bảng để cấu hình hàm Lambda

   ![db5](/images/4/db5.png?width=90pc)

## Cấu Hình Amazon S3

### Bước 1: Truy Cập S3 Console

1. Điều hướng đến [S3 Console](https://s3.console.aws.amazon.com/s3/home?region=ap-southeast-1)

   ![s3-1](/images/4/s3-1.png?width=90pc)

### Bước 2: Tạo S3 Bucket

1. Nhấp **Create bucket**
2. Cấu hình cài đặt bucket

   ![s3-2](/images/4/s3-2.png?width=90pc)

### Bước 3: Cấu Hình Thuộc Tính Bucket

- **Tên bucket**: Nhập tên bucket duy nhất
- **Vùng**: Chọn vùng AWS phù hợp
- **Cài đặt truy cập**: Cấu hình theo yêu cầu bảo mật

   ![s3-3](/images/4/s3-3.png?width=90pc)

### Bước 4: Lưu Cấu Hình Bucket

- Xác minh việc tạo bucket thành công
- **Quan trọng**: Ghi lại ARN của bucket để cấu hình hàm Lambda và ứng dụng

   ![s3-4](/images/4/s3-4.png?width=90pc)

---

## Tiếp tục

[5. Document AI](../5-document-ai/)

---

## Tài Liệu Tham Khảo

- [Amazon DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/)
- [Amazon S3 User Guide](https://docs.aws.amazon.com/s3/)
- [DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)
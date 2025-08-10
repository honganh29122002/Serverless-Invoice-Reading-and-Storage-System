+++
title = "Kiểm Thử Ứng Dụng"
date = 2020-05-14T00:38:32+07:00
weight = 8
chapter = false
pre = "<b>8. </b>"
+++

Phần này bao gồm các quy trình kiểm thử toàn diện để xác thực chức năng của hệ thống xử lý hóa đơn serverless.

## Quy Trình Kiểm Thử

### Bước 1: Kiểm Thử Xác Thực

**Test Case 1.1: Thử Đăng Nhập Không Hợp Lệ**
1. Thử đăng nhập với tài khoản sai

   ![test](/images/8/test1.png?width=90pc)

**Test Case 1.2: Thử Đăng Nhập Hợp Lệ**

2. Thử đăng nhập với tài khoản đúng

   ![test](/images/8/test2.png?width=90pc)

### Bước 2: Kiểm Thử Upload File

1. Chọn dữ liệu là hình ảnh hóa đơn với phần mở rộng **.png**

   ![test](/images/8/test3.png?width=90pc)
   ![test](/images/8/test4.png?width=90pc)

2. Upload hình ảnh

   ![test](/images/8/test5.png?width=90pc)

### Bước 3: Xác Minh Lưu Trữ

1. Kiểm tra s3 bucket và xem ảnh đã được upload

   ![test](/images/8/test6.png?width=90pc)

2. Kiểm tra log lambda để xem dữ liệu đã được lưu vào DynamoDB thành công

   ![test](/images/8/test8.png?width=90pc)
   ![test](/images/8/test9.png?width=90pc)

3. Kiểm tra bảng trong **DynamoDB**

   ![test](/images/8/test7.png?width=90pc)

### Bước 4: Kiểm Thử Truy Xuất Dữ Liệu

1. Thử xem dữ liệu được lưu trữ trong dynamo thông qua frontend

   ![test](/images/8/test10.png?width=90pc)

### Bước 5: Kiểm Thử Upload Nhiều File

1. Tiếp tục upload một hóa đơn khác và cũng thành công.

   ![test](/images/8/test11.png?width=90pc)
   ![test](/images/8/test12.png?width=90pc)
   ![test](/images/8/test13.png?width=90pc)

---

## Tiếp tục

[9. Dọn Dẹp](../9-delete-source/)

---

## Tài Liệu Tham Khảo

- [AWS Testing Best Practices](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/testing.html)
- [API Gateway Testing](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-testing.html)
- [Lambda Function Testing](https://docs.aws.amazon.com/lambda/latest/dg/testing-debugging.html)
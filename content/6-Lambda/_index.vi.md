+++
title = "Cấu Hình Lambda"
date = 2020-05-14T00:38:32+07:00
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

Phần này bao gồm việc cấu hình và triển khai các hàm serverless để cung cấp năng lượng cho quy trình xử lý tài liệu.

## Tổng Quan

Ứng dụng sử dụng nhiều hàm Lambda để xử lý các khía cạnh khác nhau của pipeline xử lý hóa đơn:

- **Database Scanner**: Truy xuất và quản lý dữ liệu từ DynamoDB
- **Image Upload Handler**: Xử lý việc tải file lên S3
- **Textract Integration**: Trích xuất dữ liệu từ tài liệu hóa đơn
- **Bedrock Integration**: Cung cấp phân tích và hiểu biết sâu sắc được hỗ trợ bởi AI

## Kiến Trúc Hàm

Mỗi hàm Lambda được thiết kế với các trách nhiệm cụ thể để duy trì sự tách biệt các mối quan tâm và tối ưu hóa hiệu suất. Các hàm hoạt động cùng nhau để tạo ra một pipeline xử lý serverless hoàn chỉnh có thể tự động mở rộng dựa trên nhu cầu.

---

## Tiếp tục

[7. API Gateway](../7-api-gateway/)

---

## Tài Liệu Tham Khảo

- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
- [Serverless Architecture Patterns](https://aws.amazon.com/serverless/patterns/)
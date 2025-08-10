+++
title = "Cấu Hình API Gateway"
date = 2020-05-14T00:38:32+07:00
weight = 7
chapter = false
pre = "<b>7. </b>"
+++

Phần này bao gồm việc thiết lập API Gateway để tạo các REST API an toàn, có thể mở rộng kết nối ứng dụng frontend với các hàm Lambda backend.

## Tổng Quan API Gateway

### Chức Năng Cốt Lõi

**1. Quản Lý Yêu Cầu**
- Đóng vai trò là điểm vào duy nhất cho tất cả các yêu cầu của client
- Quản lý giao tiếp giữa frontend và các dịch vụ backend
- Cung cấp xử lý yêu cầu/phản hồi tập trung

**2. Định Tuyến Yêu Cầu**
- Định tuyến các yêu cầu HTTP/HTTPS đến các dịch vụ backend phù hợp
- Chỉ đạo yêu cầu đến các hàm Lambda cụ thể dựa trên endpoints
- Hỗ trợ nhiều loại tích hợp (Lambda, HTTP, dịch vụ AWS)

**3. Tích Hợp Bảo Mật**
- Tích hợp với Amazon Cognito để xác thực
- Hỗ trợ OAuth2 và ủy quyền tùy chỉnh
- Cung cấp quản lý API key và throttling

### Vai Trò Kiến Trúc

Trong kiến trúc serverless của chúng ta, API Gateway đóng vai trò là lớp điều phối:
- Nhận yêu cầu từ ứng dụng frontend
- Định tuyến yêu cầu quét dữ liệu đến hàm **Database Scanner**
- Chỉ đạo yêu cầu upload đến hàm **Image Upload Handler**
- Kết nối với hàm **Textract Integration** để xử lý tài liệu
- Liên kết với hàm **Bedrock Integration** để phân tích AI
- Quản lý xác thực thông qua tích hợp Cognito

## Cấu Hình API

### API Lưu Trữ và Xử Lý Hóa Đơn

#### Bước 1: Tạo REST API

1. Điều hướng đến [Amazon API Gateway Console](https://ap-southeast-1.console.aws.amazon.com/apigateway/main/welcome?api=unselected&region=ap-southeast-1)

   ![api1](/images/7/api1.png?width=90pc)

2. Tạo API mới
   - Chọn **REST API**

   ![api2](/images/7/api2.png?width=90pc)
   - Nhập **tên API** và **Tạo**
   ![api3](/images/7/api3.png?width=90pc)

#### Bước 2: Tạo Upload Resource

1. Tạo **resource** mới
   - **Tên resource**: Nhập tên mô tả
   - **Bật CORS**: Chọn tùy chọn này

   ![api4](/images/7/api4.png?width=90pc)
   ![api5](/images/7/api5.png?width=90pc)

#### Bước 3: Tạo Dynamic Path Resource

1. Tạo **child resource**
   - **Tên resource**: `{filename}`
   - **Bật CORS**: Chọn tùy chọn này

   ![api6](/images/7/api6.png?width=90pc)

#### Bước 4: Cấu Hình POST Method

1. Tạo method để upload file

   ![api7](/images/7/api7.png?width=90pc)
   - **Loại method**: POST
   - **Lambda Proxy Integration**: Bật
   - **Hàm Lambda**: Chọn hàm xử lý upload S3
  
   ![api8](/images/7/api8.png?width=90pc)

#### Bước 5: Cấu Hình Response Headers

1. Thiết lập cấu hình response
   - **Response headers**: `Access-Control-Allow-Origin`
   - **Response body**: `application/json`

   ![api9](/images/7/api9.png?width=90pc)

#### Bước 6: Cấu Hình Media Types

1. Truy cập **cài đặt API**

   ![api10](/images/7/api10.png?width=90pc)
2. Thêm **media type** cho upload file
   ![api11](/images/7/api11.png?width=90pc)

### API Truy Xuất Dữ Liệu

#### Bước 1: Tạo View Resource

1. Tạo resource mới để truy xuất dữ liệu

   ![api12](/images/7/api12.png?width=90pc)
   - **Tên resource**: `view-all`
   - **Bật CORS**: Chọn tùy chọn này
   - **Tạo**
   ![api13](/images/7/api13.png?width=90pc)

#### Bước 2: Cấu Hình GET Method

1. Tạo method để truy xuất dữ liệu

   ![api14](/images/7/api14.png?width=90pc)
   - **Loại method**: GET
   - **Lambda Proxy Integration**: Bật
   - **Hàm Lambda**: Chọn hàm scanner DynamoDB
  
   ![api15](/images/7/api15.png?width=90pc)

#### Bước 3: Deploy API

1. Deploy API để có thể truy cập được

   ![api16](/images/7/api16.png?width=90pc)
2. **Quan trọng**: Lưu URL deployment để tích hợp frontend
   ![api17](/images/7/api17.png?width=90pc)

## Thực Hành Tốt Nhất

### Bảo Mật
- Luôn bật CORS cho các yêu cầu cross-origin
- Triển khai xác thực và ủy quyền phù hợp
- Sử dụng API keys để kiểm soát truy cập bổ sung

### Hiệu Suất
- Bật caching cho các endpoints được truy cập thường xuyên
- Cấu hình giới hạn throttling phù hợp
- Giám sát việc sử dụng API và các số liệu hiệu suất

### Giám Sát
- Thiết lập CloudWatch logging để debug
- Cấu hình cảnh báo cho tỷ lệ lỗi và độ trễ
- Sử dụng AWS X-Ray để tracing phân tán

---

## Tiếp tục

[8. Kiểm Thử](../8-testing/)
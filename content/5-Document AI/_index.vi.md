+++
title = "Document AI"
date = 2024-05-14T00:38:32+07:00
weight = 5
chapter = false
pre = "<b>5. </b>"
+++

Trong phần này, chúng ta sẽ khám phá vai trò của Amazon Textract và Amazon Bedrock trong hệ thống xử lý hóa đơn serverless, cùng với cách Guardrails bảo vệ thông tin nhạy cảm.

## Tổng Quan Kiến Trúc

Hệ thống Document AI bao gồm các thành phần chính sau:
- **Amazon S3**: Lưu trữ hóa đơn đầu vào và kết quả xử lý
- **AWS Lambda**: Điều phối quy trình xử lý serverless
- **Amazon Textract**: Trích xuất dữ liệu từ hóa đơn
- **Amazon Bedrock**: Phân tích thông minh và xử lý thông tin

## Vai Trò của Amazon Textract

### Chức Năng Cốt Lõi
Amazon Textract là dịch vụ machine learning được quản lý hoàn toàn chuyên dụng cho:

**1. Trích Xuất Văn Bản và Dữ Liệu Có Cấu Trúc**
- Nhận dạng và trích xuất văn bản từ hình ảnh và PDF
- Phát hiện các trường dữ liệu có cấu trúc như bảng và biểu mẫu
- Duy trì định dạng và bố cục của tài liệu gốc

**2. Phân Tích Hóa Đơn và Biên Lai (Analyze Expense)**
- Tự động xác định các trường chính:
  - Tên Nhà Cung Cấp
  - Ngày Hóa Đơn
  - Tổng Số Tiền
  - Số Tiền Thuế
  - Chi tiết các mục hàng
- Trích xuất thông tin với điểm tin cậy cao
- Hỗ trợ nhiều định dạng hóa đơn khác nhau

**3. Xử Lý Theo Lô và Thời Gian Thực**
- Xử lý đồng bộ cho tài liệu nhỏ (< 5MB)
- Xử lý bất đồng bộ cho tài liệu lớn và xử lý theo lô
- Tích hợp trực tiếp với S3 để xử lý tự động

### Lợi Ích Trong Hệ Thống
- **Độ Chính Xác Cao**: Sử dụng mô hình deep learning được huấn luyện trên hàng triệu tài liệu
- **Không Cần Huấn Luyện**: Mô hình được huấn luyện sẵn và sẵn sàng sử dụng
- **Có Thể Mở Rộng**: Tự động mở rộng theo khối lượng công việc
- **Tiết Kiệm Chi Phí**: Chỉ trả tiền cho những gì bạn sử dụng

## Vai Trò của Amazon Bedrock

### Chức Năng Cốt Lõi
Amazon Bedrock cung cấp nền tảng để truy cập các mô hình nền tảng thông qua API:

**1. Claude 3 Haiku - Mô Hình Được Chọn**
- **Tốc Độ Cao**: Thời gian phản hồi nhanh, phù hợp cho xử lý thời gian thực
- **Tiết Kiệm Chi Phí**: Chi phí thấp cho xử lý khối lượng lớn
- **Hiệu Quả**: Hiệu suất xuất sắc cho các tác vụ phân tích và tóm tắt
- **Đa Ngôn Ngữ**: Hỗ trợ tiếng Việt và nhiều ngôn ngữ khác

**2. Phân Tích Thông Minh**
- **Xác Minh Dữ Liệu**: Xác thực độ chính xác của các giá trị số
- **Phân Loại Tự Động**: Phân loại hóa đơn theo loại hàng hóa/dịch vụ
- **Phát Hiện Bất Thường**: Xác định các giá trị không hợp lý
- **Tóm Tắt Thông Tin**: Tạo tóm tắt có ý nghĩa từ dữ liệu thô

**3. Xử Lý Ngôn Ngữ Tự Nhiên**
- Hiểu ngữ cảnh và ý nghĩa của thông tin
- Trả lời câu hỏi về nội dung hóa đơn
- Tạo ra những hiểu biết sâu sắc và khuyến nghị
- Định dạng đầu ra theo yêu cầu (JSON, text, v.v.)

### Lợi Ích Trong Hệ Thống
- **Serverless**: Không cần quản lý cơ sở hạ tầng
- **Dịch Vụ Được Quản Lý**: AWS xử lý cập nhật và bảo trì mô hình
- **Tính Khả Dụng Cao**: SLA cao cho khối lượng công việc sản xuất
- **Tích Hợp**: Tích hợp dễ dàng với các dịch vụ AWS khác

### Ứng Dụng Trong Xử Lý Hóa Đơn
- **Bảo Vệ Thông Tin Tài Chính**: Ngăn chặn việc tiết lộ số tài khoản và thông tin thanh toán
- **Tuân Thủ Quy Định**: Đảm bảo tuân thủ các quy định
- **Bảo Mật Dữ Liệu**: Bảo vệ thông tin khách hàng và nhà cung cấp
- **Kiểm Soát Chất Lượng**: Đảm bảo chất lượng và đầu ra phù hợp

## Quy Trình Xử Lý Tổng Thể

### Bước 1: Thu Thập Tài Liệu
- Hóa đơn được tải lên S3
- Hàm Lambda được kích hoạt tự động
- Xác thực và tiền xử lý

### Bước 2: Trích Xuất Dữ Liệu (Textract)
- API analyze_expense của Textract được gọi
- Trích xuất dữ liệu có cấu trúc từ hóa đơn
- Điểm tin cậy cho từng trường

### Bước 3: Phân Tích Thông Minh (Bedrock)
- Dữ liệu từ Textract được gửi đến Claude 3 Haiku
- AI phân tích, xác minh và tạo ra những hiểu biết sâu sắc
- Guardrails đảm bảo đầu ra an toàn

### Bước 4: Lưu Trữ Kết Quả
- Kết quả được định dạng và lưu trữ
- Metadata và audit trail
- Tích hợp với các hệ thống downstream

## Lợi Ích của Kiến Trúc Serverless

**1. Khả Năng Mở Rộng**
- Tự động mở rộng theo nhu cầu
- Xử lý từ vài hóa đơn đến hàng nghìn mỗi giây
- Không cần lập kế hoạch dung lượng

**2. Tối Ưu Hóa Chi Phí**
- Mô hình trả theo sử dụng
- Không có tài nguyên nhàn rỗi
- Quản lý tài nguyên tự động

**3. Độ Tin Cậy**
- Khả năng chịu lỗi tích hợp
- Thử lại tự động và xử lý lỗi
- Triển khai đa AZ

**4. Bảo Trì**
- Chi phí vận hành tối thiểu
- Cập nhật và vá lỗi tự động
- Tập trung vào logic nghiệp vụ

## Tài Liệu Tham Khảo

- [Tài Liệu Amazon Textract](https://docs.aws.amazon.com/textract/)
- [Hướng Dẫn Sử Dụng Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/)
- [Hướng Dẫn Mô Hình Claude 3 Haiku](https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters-anthropic-claude-3.html)

---

## Tiếp tục

[6. Hàm Lambda](../6-lambda/)
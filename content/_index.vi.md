+++
title = "Hệ Thống Đọc và Lưu Trữ Hóa Đơn Serverless"
date = 2020-05-14T00:38:32+07:00
weight = 1
chapter = false
+++

# Hệ Thống Đọc và Lưu Trữ Hóa Đơn Serverless
## Tổng Quan

Hệ thống đại diện cho một kiến trúc hoàn toàn serverless và có khả năng mở rộng cao được xây dựng hoàn toàn trên các dịch vụ AWS cloud, được thiết kế để quản lý truy cập người dùng một cách an toàn, xử lý logic backend và lưu trữ dữ liệu hiệu quả. Tại điểm đầu vào, **Amazon Route 53** chịu trách nhiệm phân giải DNS, định hướng các yêu cầu của client đến endpoint phù hợp. Các yêu cầu này sau đó được chuyển đến **Amazon API Gateway**, đóng vai trò là giao diện tập trung cho tất cả các tương tác bên ngoài với backend. API Gateway không chỉ xử lý việc định tuyến yêu cầu mà còn thực thi bảo mật bằng cách tích hợp với **Amazon Cognito** để xác thực và ủy quyền người dùng.

Khi người dùng được xác thực, API Gateway chuyển tiếp yêu cầu đến các hàm AWS Lambda cụ thể chứa logic nghiệp vụ cốt lõi của ứng dụng. Ví dụ, hàm **scan_lambda** có thể chịu trách nhiệm xác thực, quét hoặc tiền xử lý đầu vào của người dùng, trong khi hàm **savePicture** xử lý dữ liệu phức tạp hơn và tải kết quả lên **Amazon S3**. Amazon S3 đóng vai trò là lớp lưu trữ bền vững của hệ thống, cung cấp độ bền cao, tính khả dụng và truy cập an toàn đến dữ liệu được lưu trữ. Toàn bộ hệ thống được điều khiển bởi sự kiện, tiết kiệm chi phí và có khả năng mở rộng tự động dựa trên nhu cầu, làm cho nó lý tưởng cho các ứng dụng hiện đại yêu cầu tính khả dụng cao, chi phí vận hành thấp và kiểm soát bảo mật mạnh mẽ. Ngoài ra, với giám sát, ghi log và số liệu tích hợp được cung cấp bởi các dịch vụ AWS như CloudWatch, hệ thống đảm bảo khả năng hiển thị và bảo trì trên tất cả các thành phần mà không cần quản lý máy chủ thủ công hoặc cung cấp cơ sở hạ tầng.

![architecture](/images/1/architecture.png?width=90pc)

## Mục Tiêu

- **Không cần quản lý máy chủ** – Hệ thống tự động mở rộng và được quản lý mà không cần duy trì máy chủ.

- **Bảo mật cao** – Đảm bảo chỉ những người dùng được ủy quyền mới có thể truy cập dịch vụ.

- **Tối ưu hóa chi phí** – Giá cả theo mức sử dụng, không có chi phí cơ sở hạ tầng cố định.

- **Hiệu suất cao** – Xử lý nhanh chóng và điều chỉnh tự động dựa trên lượng traffic.

- **Tích hợp dễ dàng** – Các dịch vụ AWS hoạt động liền mạch với nhau, đơn giản hóa việc phát triển và vận hành.

## Cấu Trúc Workshop

Workshop này được tổ chức thành các phần sau để hướng dẫn bạn xây dựng một hệ thống xử lý hóa đơn serverless hoàn chỉnh:

### [1. Giới Thiệu](1-introduction/)
Bắt đầu với tổng quan workshop, kết quả học tập và hiểu biết về kiến trúc.

### [2. Frontend](2-frontend/)
Cấu hình Amazon Route 53 để quản lý DNS và triển khai ứng dụng frontend bằng AWS Amplify.

### [3. Xác Thực](3-authentication/)
Triển khai xác thực và ủy quyền người dùng an toàn bằng Amazon Cognito.

### [4. Lưu Trữ & Cơ Sở Dữ Liệu](4-storage-db/)
Thiết lập các giải pháp lưu trữ dữ liệu bằng Amazon S3 và DynamoDB cho ứng dụng của bạn.

### [5. Document AI](5-document-ai/)
Tích hợp xử lý tài liệu được hỗ trợ bởi AI bằng Amazon Textract và Bedrock.

### [6. Hàm Lambda](6-lambda/)
Phát triển và triển khai các hàm serverless cho logic nghiệp vụ cốt lõi và xử lý dữ liệu.

### [7. API Gateway](7-api-gateway/)
Tạo và cấu hình RESTful API để kết nối frontend với các dịch vụ backend.

### [8. Kiểm Thử](8-testing/)
Kiểm thử ứng dụng serverless hoàn chỉnh và xác minh tất cả các thành phần hoạt động cùng nhau.

### [9. Xóa Nguồn](9-delete-source/)
Dọn dẹp các tài nguyên AWS để tránh chi phí không cần thiết sau khi hoàn thành workshop.

### [10. Kết Luận](10-conclusion/)
Tóm tắt những thành tựu đạt được và các bước tiếp theo cho hành trình serverless của bạn.

---

## Bắt Đầu

Để bắt đầu workshop này, nhấp vào **[Giới Thiệu](1-introduction/)** hoặc sử dụng menu điều hướng bên trái để tiến hành từng phần một cách tuần tự.

{{% notice tip %}}
Đảm bảo bạn có tài khoản AWS với quyền phù hợp trước khi bắt đầu workshop này.
{{% /notice %}}
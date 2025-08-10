+++
title = "Xác Thực"
date = 2020-05-14T00:38:32+07:00
weight = 3
chapter = false
pre = "<b>3. </b>"
+++

### Amazon Cognito là gì?

Amazon Cognito đóng vai trò là dịch vụ xác thực và quản lý người dùng trung tâm trong các hệ thống dựa trên AWS, đảm bảo kiểm soát truy cập an toàn đến các tài nguyên backend như hàm Lambda và lưu trữ S3.

### Cấu Hình Amazon Cognito

### Bước 1: Tạo User Pool

1. Điều hướng đến [Amazon Cognito Console](https://us-east-1.console.aws.amazon.com/cognito/v2/home?region=us-east-1)
2. Nhấp **Create User Pool**

### Bước 2: Cấu Hình Cài Đặt Ứng Dụng

   ![cog1](/images/3/cog1.png?width=90pc)
- **Loại ứng dụng**: Single-page application
- **Tên ứng dụng**: Nhập tên ứng dụng của bạn
- **Tùy chọn đăng nhập**: Username

   ![cog2](/images/3/cog2.png?width=90pc)
- **Return URL**: Nhập URL ứng dụng của bạn
- **Thuộc tính bắt buộc cho đăng ký**: email
   ![cog3](/images/3/cog3.png?width=90pc)

### Bước 3: Truy Cập Giao Diện Đăng Nhập

- Xem lại cấu hình trang đăng nhập được host
- Kiểm thử giao diện đăng nhập

   ![cog4](/images/3/cog4.png?width=90pc)

### Bước 4: Lưu Chi Tiết Cấu Hình

**Quan trọng**: Ghi lại các giá trị sau để tích hợp ứng dụng:
 - **User Pool ID**
   ![cog5](/images/3/cog5.png?width=90pc)
 - **Client ID**
   ![cog6](/images/3/cog6.png?width=90pc)

### Bước 5: Tạo Tài Khoản Người Dùng Thử Nghiệm

1. Tạo tài khoản người dùng mới để kiểm thử
2. Hoàn thành quy trình đăng ký

   ![cog7](/images/3/cog7.png?width=90pc)
   ![cog8](/images/3/cog8.png?width=90pc)

### Bước 6: Xác Minh Xác Thực

1. Đăng nhập bằng thông tin đăng nhập đã tạo
2. Xác minh xác thực thành công
- Nhập username và password bạn đã thiết lập trước đó.
   ![cog9](/images/3/cog9.png?width=90pc)
   ![cog10](/images/3/cog10.png?width=90pc)
- Thay đổi mật khẩu và xác nhận
   ![cog11](/images/3/cog11.png?width=90pc)

### Bước 7: Xác Nhận Trạng Thái Người Dùng

- Xác minh trạng thái người dùng hiển thị là **Confirmed**
- Người dùng hiện đã sẵn sàng để truy cập ứng dụng

   ![cog12](/images/3/cog12.png?width=90pc)

---

## Tiếp tục

[4. Lưu Trữ & Cơ Sở Dữ Liệu](../4-storage-db/)

---

## Tài Liệu Tham Khảo

- [Amazon Cognito Documentation](https://docs.aws.amazon.com/cognito/)
- [Cognito User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html)
- [Authentication Best Practices](https://docs.aws.amazon.com/cognito/latest/developerguide/security.html)
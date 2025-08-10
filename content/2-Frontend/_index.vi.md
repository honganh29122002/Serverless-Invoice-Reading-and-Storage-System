+++
title = "Frontend"
date = 2020-05-14T00:38:32+07:00
weight = 2
chapter = false
pre = "<b>2. </b>"
+++

Phần này bao gồm việc thiết lập frontend cho hệ thống xử lý hóa đơn serverless, sử dụng Amazon Route 53 để quản lý DNS và AWS Amplify để hosting ứng dụng web.

## Thiết Lập Amazon Route 53

### Bước 1: Tạo Hosted Zone

1. Điều hướng đến [Amazon Route 53 Console](https://us-east-1.console.aws.amazon.com/route53/v2/home?region=ap-southeast-1#Dashboard)

   ![route1](/images/2/route1.png?width=90pc)

2. Nhấp **Hosted zones** → **Create hosted zone**
   ![route2](/images/2/route2.png?width=90pc)


- **Tên domain**: Nhập tên domain đã đăng ký của bạn
- **Loại**: Chọn **Public hosted zone**

   ![route3](/images/2/route3.png?width=90pc)

- Xác nhận hosted zone được tạo thành công
  ![route4](/images/2/route4.png?width=90pc)

### Bước 2: Xác Minh Tạo Hosted Zone

- Ghi chú các bản ghi NS và SOA mặc định
- Sao chép các giá trị trong trường **Value/Route traffic to**
- Cập nhật name servers của domain registrar để trỏ đến AWS Route 53

   ![route5](/images/2/route5.png?width=90pc)

## Cấu Hình AWS Amplify

### Bước 1: Khởi Tạo Ứng Dụng Amplify

1. Điều hướng đến [Amazon Amplify Console](https://ap-southeast-1.console.aws.amazon.com/amplify/apps)
2. Nhấp **Deploy an app**

   ![fe1](/images/2/fe1.png?width=90pc)

### Bước 2: Chọn Phương Thức Triển Khai

- Chọn **Deploy without git**
- Nhấp **Next**

   ![fe2](/images/2/fe2.png?width=90pc)

### Bước 3: Upload File Ứng Dụng

- Nhập **tên ứng dụng**

   ![fe3](/images/2/fe3.png?width=90pc)
- Upload file [Frontend.zip](https://github.com/honganh29122002/Frontend.zip) từ máy local
   ![fe4](/images/2/fe4.png?width=90pc)


### Bước 4: Triển Khai Ứng Dụng

- Xem lại cài đặt cấu hình
- Nhấp **Save and deploy**

   ![fe5](/images/2/fe5.png?width=90pc)

### Bước 5: Cấu Hình Custom Domain

1. Điều hướng đến **Domain management**

   ![fe6](/images/2/fe6.png?width=90pc)
2. Nhấp **Add domain**
   ![fe7](/images/2/fe7.png?width=90pc)

### Bước 6: Cấu Hình Domain

- Nhập tên custom domain của bạn
- Nhấp **Configure domain**

   ![fe8](/images/2/fe8.png?width=90pc)
   ![fe9](/images/2/fe9.png?width=90pc)

### Bước 7: Xác Minh Triển Khai

- Đợi xác minh domain và cấp phát SSL certificate
- Xác nhận ứng dụng có thể truy cập được qua custom domain

   ![fe10](/images/2/fe10.png?width=90pc)

---

## Tiếp tục

[3. Xác Thực](../3-authentication/)

---

## Tài Liệu Tham Khảo

- [Amazon Route 53 Documentation](https://docs.aws.amazon.com/route53/)
- [AWS Amplify User Guide](https://docs.aws.amazon.com/amplify/)
- [Custom Domain Configuration](https://docs.aws.amazon.com/amplify/latest/userguide/custom-domains.html)
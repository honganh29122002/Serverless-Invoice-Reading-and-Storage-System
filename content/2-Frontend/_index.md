+++
title = "Frontend"
date = 2020-05-14T00:38:32+07:00
weight = 2
chapter = false
pre = "<b>2. </b>"
+++


## Amazon Route 53 Setup

### Step 1: Create Hosted Zone

1. Navigate to the [Amazon Route 53 Console](https://us-east-1.console.aws.amazon.com/route53/v2/home?region=ap-southeast-1#Dashboard)
2. Click **Hosted zones** → **Create hosted zone**

   ![route1](/images/2/route1.png?width=90pc)
   ![route2](/images/2/route2.png?width=90pc)

### Step 2: Configure Domain Settings

- **Domain name**: Enter your registered domain name
- **Type**: Select **Public hosted zone**

   ![route3](/images/2/route3.png?width=90pc)

### Step 3: Verify Hosted Zone Creation

- Confirm the hosted zone is created successfully
- Note the default NS and SOA records

   ![route4](/images/2/route4.png?width=90pc)

- Code **Frontend**
```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Invoice Uploader</title>
  <script src="https://cdn.jsdelivr.net/npm/amazon-cognito-identity-js@6.3.7/dist/amazon-cognito-identity.min.js"></script>
  <style>
    body { font-family: Arial, sans-serif; margin: 30px; }
    form, button { margin-top: 20px; }
    #upload-form, #view-all-btn { display: none; }
    #result { background: #f4f4f4; padding: 10px; border: 1px solid #ccc; white-space: pre-wrap; }
    #view-all-result { background: #f4f4f4; padding: 10px; border: 1px solid #ccc; white-space: pre-wrap; margin-top: 20px; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; }
    th, td { padding: 8px 12px; border: 1px solid #ddd; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

  <h2>Login</h2>
  <form id="login-form">
    <input type="text" id="username" placeholder="Username or Email" required />
    <input type="password" id="password" placeholder="Password" required />
    <button type="submit">Login</button>
  </form>
  <div id="login-message"></div>

  <h2>Upload Invoice</h2>
  <form id="upload-form">
    <input type="file" id="invoice-file" accept=".pdf,.jpg,.jpeg,.png,.txt" required />
    <button type="submit">Upload</button>
  </form>

  <h3>Result</h3>
  <pre id="result"></pre>

  <h3>View All Invoices</h3>
  <!-- Nút bấm để gọi API view-all và hiển thị dữ liệu -->
  <button id="view-all-btn">View All Invoices</button>
  <div id="view-all-result"></div>

  <script>
    const loginForm = document.getElementById("login-form");
    const uploadForm = document.getElementById("upload-form");
    const loginMessage = document.getElementById("login-message");
    const resultEl = document.getElementById("result");
    const viewAllBtn = document.getElementById("view-all-btn");
    const viewAllResultEl = document.getElementById("view-all-result");

    const API_GATEWAY_UPLOAD_URL =
      "https://fvfgkbr294.execute-api.ap-southeast-1.amazonaws.com/dev/invoicebuckett123/{filename}";
    const API_GATEWAY_VIEW_ALL_URL =
      "https://fvfgkbr294.execute-api.ap-southeast-1.amazonaws.com/dev/view-all"; // URL cho view-all API

    const poolData = {
      UserPoolId: "ap-southeast-1_noiKt1wrx",
      ClientId: "3rodaicnohm5pnh5q3105qccvd",
    };
    const userPool = new AmazonCognitoIdentity.CognitoUserPool(poolData);

    // Đăng nhập Cognito
    loginForm.addEventListener("submit", function (e) {
      e.preventDefault();
      const username = document.getElementById("username").value;
      const password = document.getElementById("password").value;

      console.log("Đăng nhập với:", { username });

      loginMessage.style.color = "blue";
      loginMessage.textContent = "Đang đăng nhập...";

      const authDetails = new AmazonCognitoIdentity.AuthenticationDetails({ Username: username, Password: password });
      const cognitoUser = new AmazonCognitoIdentity.CognitoUser({ Username: username, Pool: userPool });

      cognitoUser.authenticateUser(authDetails, {
        onSuccess: function (result) {
          const token = result.getIdToken().getJwtToken();
          console.log("Đăng nhập thành công - Token:", token);
          window.idToken = token;

          loginMessage.style.color = "green";
          loginMessage.textContent = "Đăng nhập thành công!";
          loginForm.style.display = "none";
          uploadForm.style.display = "block";
          viewAllBtn.style.display = "inline-block"; // Hiển thị nút View All
        },
        onFailure: function (err) {
          console.error("Lỗi đăng nhập:", err);
          loginMessage.style.color = "red";
          loginMessage.textContent = "Đăng nhập thất bại: " + err.message;
        }
      });
    });

    // Upload hóa đơn
    uploadForm.addEventListener("submit", async function (e) {
      e.preventDefault();
      const file = document.getElementById("invoice-file").files[0];
      if (!file) {
        console.warn("Không có file được chọn");
        resultEl.textContent = "Vui lòng chọn file để upload.";
        return;
      }

      const fileName = encodeURIComponent(file.name);
      const uploadUrl = API_GATEWAY_UPLOAD_URL.replace("{filename}", fileName);
      const idToken = window.idToken;

      if (!idToken) {
        console.error("Không tìm thấy ID token.");
        resultEl.textContent = "Bạn chưa đăng nhập hoặc phiên đăng nhập đã hết hạn.";
        return;
      }

      console.log("Chuẩn bị upload:", {
        fileName,
        uploadUrl,
        fileType: file.type,
        fileSize: file.size,
      });

      try {
        const arrayBuffer = await file.arrayBuffer();

        const response = await fetch(uploadUrl, {
          method: "POST",
          headers: {
            Authorization: idToken,
            "Content-Type": file.type || "application/octet-stream",
          },
          body: arrayBuffer,
        });

        console.log("Response status:", response.status);
        const resultText = await response.text();
        console.log("Phản hồi từ Lambda:", resultText);
        resultEl.textContent = resultText;
      } catch (error) {
        console.error("Lỗi upload:", error);
        resultEl.textContent = "Lỗi upload: " + error.message;
      }
    });

    // Gọi API View All Invoices
    viewAllBtn.addEventListener("click", async function () {
      const idToken = window.idToken;

      if (!idToken) {
        console.error("Không tìm thấy ID token.");
        viewAllResultEl.textContent = "Bạn chưa đăng nhập hoặc phiên đăng nhập đã hết hạn.";
        return;
      }

      console.log("Đang gọi API View All Invoices");

      try {
        const response = await fetch(API_GATEWAY_VIEW_ALL_URL, {
          method: "GET",
          headers: {
            Authorization: idToken,
          },
        });

        if (response.ok) {
          const data = await response.json();
          console.log("Dữ liệu hóa đơn:", data);
          // Hiển thị kết quả dưới dạng HTML được trả về từ Lambda
          viewAllResultEl.innerHTML = data.formatted_result; // Hiển thị kết quả dưới dạng HTML
        } else {
          console.error("Lỗi khi gọi API View All:", response.status);
          viewAllResultEl.textContent = "Lỗi khi gọi API View All.";
        }
      } catch (error) {
        console.error("Lỗi gọi API View All:", error);
        viewAllResultEl.textContent = "Lỗi kết nối với API View All: " + error.message;
      }
    });
  </script>

</body>
</html>
```

### Step 4: Update Domain Name Servers

- Copy the **Value/Route traffic to** field values
- Update your domain registrar's name servers to point to AWS Route 53

   ![route5](/images/2/route5.png?width=90pc)

## AWS Amplify Configuration

### Step 1: Initialize Amplify Application

1. Navigate to the [Amazon Amplify Console](https://ap-southeast-1.console.aws.amazon.com/amplify/apps)
2. Click **Deploy an app**

   ![fe1](/images/2/fe1.png?width=90pc)

### Step 2: Choose Deployment Method

- Select **Deploy without git**
- Click **Next**

   ![fe2](/images/2/fe2.png?width=90pc)

### Step 3: Upload Application Files

- Enter your **App name**
- Upload the application .zip file from your local machine

   ![fe3](/images/2/fe3.png?width=90pc)
   ![fe4](/images/2/fe4.png?width=90pc)

### Step 4: Deploy Application

- Review configuration settings
- Click **Save and deploy**

   ![fe5](/images/2/fe5.png?width=90pc)

### Step 5: Configure Custom Domain

1. Navigate to **Domain management**
2. Click **Add domain**

   ![fe6](/images/2/fe6.png?width=90pc)
   ![fe7](/images/2/fe7.png?width=90pc)

### Step 6: Domain Configuration

- Enter your custom domain name
- Click **Configure domain**

   ![fe8](/images/2/fe8.png?width=90pc)
   ![fe9](/images/2/fe9.png?width=90pc)

### Step 7: Verify Deployment

- Wait for domain verification and SSL certificate provisioning
- Confirm the application is accessible via your custom domain

   ![fe10](/images/2/fe10.png?width=90pc)
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

   ![route1](/images/2/route1.png?width=90pc)
2. Click **Hosted zones** → **Create hosted zone**
   ![route2](/images/2/route2.png?width=90pc)


- **Domain name**: Enter your registered domain name
- **Type**: Select **Public hosted zone**

   ![route3](/images/2/route3.png?width=90pc)

- Confirm the hosted zone is created successfully
  ![route4](/images/2/route4.png?width=90pc)

### Step 2: Verify Hosted Zone Creation

- Note the default NS and SOA records
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

   ![fe3](/images/2/fe3.png?width=90pc)
- Upload the [Frontend.zip](https://github.com/honganh29122002/Frontend.zip) file from your local machine
   ![fe4](/images/2/fe4.png?width=90pc)



  ### Step 4: Deploy Application

- Review configuration settings
- Click **Save and deploy**

   ![fe5](/images/2/fe5.png?width=90pc)

### Step 5: Configure Custom Domain

1. Navigate to **Domain management**

   ![fe6](/images/2/fe6.png?width=90pc)
2. Click **Add domain**
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

---

## Continue to

[3. Authentication](../3-authentication/)

---

## References

- [Amazon Route 53 Documentation](https://docs.aws.amazon.com/route53/)
- [AWS Amplify User Guide](https://docs.aws.amazon.com/amplify/)
- [Custom Domain Configuration](https://docs.aws.amazon.com/amplify/latest/userguide/custom-domains.html)
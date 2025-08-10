# Serverless Invoice Reading and Storage System

A comprehensive workshop demonstrating how to build a fully serverless invoice processing system using AWS services with AI-powered document analysis.

## 🏗️ Architecture Overview

This system implements a modern serverless architecture that automatically processes invoices using AI services while maintaining high security and scalability.

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   User/Client   │───▶│   Amazon Route   │───▶│  AWS Amplify    │
│                 │    │       53         │    │   (Frontend)    │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                         │
                                                         ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│  Amazon Cognito │◀───│   Amazon API     │◀───│   Web Client    │
│ (Authentication)│    │    Gateway       │    │                 │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                │
                                ▼
                    ┌──────────────────┐
                    │   AWS Lambda     │
                    │   Functions      │
                    └──────────────────┘
                                │
                ┌───────────────┼───────────────┐
                ▼               ▼               ▼
    ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
    │   Amazon S3     │ │   Amazon        │ │   Amazon        │
    │ (File Storage)  │ │   DynamoDB      │ │   Textract      │
    └─────────────────┘ └─────────────────┘ └─────────────────┘
                                                      │
                                                      ▼
                                          ┌─────────────────┐
                                          │   Amazon        │
                                          │   Bedrock       │
                                          │ (Claude 3 Haiku)│
                                          └─────────────────┘
```

## 🔄 Data Flow Diagram

```
1. User Authentication
   User → Cognito → JWT Token

2. File Upload Process
   Frontend → API Gateway → Lambda → S3
                         └─→ DynamoDB (metadata)

3. AI Processing Pipeline
   S3 Trigger → Lambda → Textract → Extract Data
                      └─→ Bedrock → AI Analysis
                               └─→ DynamoDB (results)

4. Data Retrieval
   Frontend → API Gateway → Lambda → DynamoDB → Display Results
```

## 🚀 Features

- **Serverless Architecture**: No server management required
- **AI-Powered Processing**: Automatic invoice data extraction using Amazon Textract
- **Intelligent Analysis**: AI insights powered by Amazon Bedrock (Claude 3 Haiku)
- **Secure Authentication**: User management with Amazon Cognito
- **Scalable Storage**: File storage with Amazon S3 and structured data with DynamoDB
- **RESTful APIs**: Secure API endpoints with Amazon API Gateway
- **Multi-language Support**: English and Vietnamese interface
- **Cost-Effective**: Pay-per-use pricing model

## 📋 Prerequisites

- AWS Account with appropriate permissions
- Basic understanding of AWS services
- Familiarity with web development concepts
- Text editor or IDE

## 🛠️ AWS Services Used

| Service | Purpose |
|---------|---------|
| **Amazon Route 53** | DNS management and domain routing |
| **AWS Amplify** | Frontend hosting and deployment |
| **Amazon Cognito** | User authentication and authorization |
| **Amazon API Gateway** | RESTful API management |
| **AWS Lambda** | Serverless compute functions |
| **Amazon S3** | File storage and static content |
| **Amazon DynamoDB** | NoSQL database for structured data |
| **Amazon Textract** | AI-powered document text extraction |
| **Amazon Bedrock** | AI foundation models (Claude 3 Haiku) |

## 📚 Workshop Structure

### [1. Introduction](content/1-introduction/)
- Workshop overview and learning objectives
- Architecture understanding
- Prerequisites and setup

### [2. Frontend Setup](content/2-frontend/)
- Amazon Route 53 configuration
- AWS Amplify deployment
- Custom domain setup

### [3. Authentication](content/3-authentication/)
- Amazon Cognito User Pool setup
- Authentication flow implementation
- Security configuration

### [4. Storage & Database](content/4-storage-db/)
- Amazon S3 bucket configuration
- DynamoDB table setup
- Access policies and permissions

### [5. Document AI](content/5-document-ai/)
- Amazon Textract integration
- Amazon Bedrock setup
- AI processing workflows

### [6. Lambda Functions](content/6-lambda/)
- Database scanner function
- Image upload handler
- Textract integration
- Bedrock AI processing

### [7. API Gateway](content/7-api-gateway/)
- REST API creation
- Endpoint configuration
- CORS and security setup

### [8. Testing](content/8-testing/)
- End-to-end testing procedures
- Authentication validation
- File processing verification

### [9. Cleanup](content/9-delete-source/)
- Resource cleanup procedures
- Cost optimization
- Best practices

### [10. Conclusion](content/10-conclusion/)
- Workshop summary
- Key achievements
- Next steps and recommendations

## 🚀 Quick Start

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Serverless-Invoice-Reading-and-Storage-System
   ```

2. **Install Hugo** (for documentation)
   ```bash
   # Windows (using Chocolatey)
   choco install hugo-extended
   
   # macOS (using Homebrew)
   brew install hugo
   
   # Linux (using Snap)
   snap install hugo
   ```

3. **Run the documentation locally**
   ```bash
   hugo server
   ```

4. **Access the workshop**
   Open your browser and navigate to `http://localhost:1313`

## 💰 Cost Considerations

This workshop uses AWS services that may incur charges. Most services offer free tier usage, but be aware of:

- **Lambda**: First 1M requests per month are free
- **API Gateway**: First 1M API calls per month are free
- **S3**: 5GB of standard storage free for 12 months
- **DynamoDB**: 25GB of storage free
- **Textract**: 1,000 pages per month free for 3 months
- **Bedrock**: Pay-per-token pricing

**Important**: Follow the cleanup procedures in Section 9 to avoid unnecessary charges.

## 🔒 Security Best Practices

- Use IAM roles with least privilege access
- Enable MFA for AWS accounts
- Implement proper CORS policies
- Use HTTPS for all communications
- Regularly rotate access keys
- Monitor CloudTrail logs

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

If you encounter any issues or have questions:

1. Check the troubleshooting section in each workshop module
2. Review AWS service documentation
3. Open an issue in this repository

## 🎯 Learning Outcomes

After completing this workshop, you will be able to:

- Design and implement serverless architectures
- Integrate multiple AWS services effectively
- Implement secure authentication and authorization
- Build AI-powered document processing systems
- Create scalable and cost-effective cloud solutions
- Apply best practices for serverless development

---

**Happy Learning!** 🎉
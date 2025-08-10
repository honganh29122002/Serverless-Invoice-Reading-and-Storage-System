+++
title = "Lambda Configuration"
date = 2020-05-14T00:38:32+07:00
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

This section covers the configuration and deployment of serverless functions that power the document processing workflow.

## Overview

The application utilizes multiple Lambda functions to handle different aspects of the invoice processing pipeline:

- **Database Scanner**: Retrieves and manages data from DynamoDB
- **Image Upload Handler**: Processes file uploads to S3
- **Textract Integration**: Extracts data from invoice documents
- **Bedrock Integration**: Provides AI-powered analysis and insights

## Function Architecture

Each Lambda function is designed with specific responsibilities to maintain separation of concerns and optimize performance. The functions work together to create a complete serverless processing pipeline that scales automatically based on demand.

---

## Continue to

[6.1 Get Data From DB](../6-Lambda/6.1-scanDB//)

---

## References

- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Lambda Best Practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
- [Serverless Architecture Patterns](https://aws.amazon.com/serverless/patterns/)

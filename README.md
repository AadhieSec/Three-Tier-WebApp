# AWS Three-Tier Web Application

A serverless three-tier web application deployed on AWS using
Amazon S3, Amazon CloudFront, Amazon API Gateway, AWS Lambda,
and Amazon DynamoDB.

The project demonstrates how a web application can separate its
presentation, application logic, and data layers while using
managed AWS services.

## Architecture

![AWS Three-Tier Architecture](architecture/aws-architecture.png)

### Architecture Overview

The application follows a serverless three-tier architecture:

- **Presentation Tier:** Amazon S3 + Amazon CloudFront
- **Application Tier:** Amazon API Gateway + AWS Lambda
- **Data Tier:** Amazon DynamoDB

The frontend is stored in Amazon S3 and delivered to users through
Amazon CloudFront. API requests from the frontend are sent to
Amazon API Gateway, which invokes an AWS Lambda function. The
Lambda function retrieves data from Amazon DynamoDB and returns
the response through the API.

---

## AWS Services

| Service | Purpose |
|---|---|
| **Amazon S3** | Stores the static website files such as HTML, CSS, and JavaScript |
| **Amazon CloudFront** | Delivers the frontend globally through a CDN and provides caching |
| **Origin Access Control (OAC)** | Allows CloudFront to securely access the S3 origin without exposing the bucket directly |
| **Amazon API Gateway** | Provides the REST API endpoint for the application |
| **AWS Lambda** | Runs the serverless application logic and retrieves data from DynamoDB |
| **Amazon DynamoDB** | Stores application/user data in a NoSQL database |
| **AWS IAM** | Controls permissions for AWS resources, including Lambda's access to DynamoDB |

---

## Architecture Flow

```text
                         USER / BROWSER
                              |
                              |
                         HTTPS Request
                              |
                              v
                    +-------------------+
                    |   Amazon          |
                    |   CloudFront      |
                    |      CDN          |
                    +---------+---------+
                              |
                              | OAC
                              v
                    +-------------------+
                    |   Amazon S3       |
                    |                   |
                    | index.html        |
                    | style.css         |
                    | script.js         |
                    +-------------------+


                         API REQUEST
                              |
                              | GET /users
                              v
                    +-------------------+
                    |  Amazon API       |
                    |    Gateway        |
                    |    REST API       |
                    +---------+---------+
                              |
                              | Invoke
                              v
                    +-------------------+
                    |    AWS Lambda     |
                    |                   |
                    | RetrieveUserData   |
                    +---------+---------+
                              |
                              | GetItem
                              v
                    +-------------------+
                    |   Amazon          |
                    |   DynamoDB        |
                    |                   |
                    |   UserData Table  |
                    +-------------------+

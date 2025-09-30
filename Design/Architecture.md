# System Architecture
<img width="706" height="366" alt="Screenshot 2025-09-30 113920" src="https://github.com/user-attachments/assets/f38fc509-e18a-4e98-beea-d452cb9d2d3f" />

## Static Site (CloudFront + S3)  
We have this as its own module because it is the website that users will interact with. It encapsulates everything the user will see and use directly.  

## API Gateway  
This is the interface through which the frontend communicates with core services and the backend. It is its own module because it is the single point of interaction between the frontend and backend.  

## EventBridge  
A cron-like scheduled job that runs once per day. Its tasks include:  
- Updating ELO for users  
- Tracking which predictions were correct or incorrect  

Since it is a single recurring job, it is represented as its own box in the diagram.  

## Core Services  
This represents the server-side logic. It functions primarily to serve the API but is a catch-all module for other backend logic as well.  

## Cognito  
Responsible for authenticating users. It is its own module because it has specific duties and responsibilities separate from other services.  

## SES (Simple Email Service)  
Handles email authentication setup (one-time configuration).  

## DynamoDB / S3  
Our planned storage solution:  
- **DynamoDB (or MongoDB alternative):** Structured, queryable data store  
- **S3:** Long-term object storage for bulk or static data  

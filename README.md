# digitalden.cloud - A Serverless Website Hosted on AWS

Website: https://digitalden.cloud

Website porfolio built using AWS resources. Github actions workflow is used to automatically provision all resources (CI/CD) for the website on AWS on a code change to the default branch on this respository.

AWS credentials are stored in Github Action Secrets" rather than in my code for security reasons.

# Architecture:
![Architecture Diagram](/Images/AWS-Architecture.png)


**Tech-stack**:

- S3
- AWS CloudFront
- Certificate Manager
- AWS Lambda
- Dynamo DB
- GitHub Actions

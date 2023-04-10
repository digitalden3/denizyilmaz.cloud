# digitalden.cloud - A Serverless Website Hosted on AWS

Website: https://digitalden.cloud

Website Porfolio built using AWS resources. Github actions workflow is used to automatically provision all resources for the website on AWS on a code change to the default branch on this respository.

# Architecture:
![Architecture Diagram](/Images/AWS-Architecture-2.png)

**Tech-Stack**:

- AWS S3
- AWS CloudFront
- Certificate Manager
- AWS Lambda
- Dynamo DB
- GitHub Actions

### 1. HTML/CSS 
Wrote my portfolio website as a HTML webpage and used CSS for styling.

### 2. Static S3 Website
Created a S3 bucket and enabled my bucket to host a static website. Uploaded my index.html (my porfolio HTML) and my CSS (referenced in my HTML) to the bucket.

### 3. HTTPS & DNS 
Registered my domain at digitalden.cloud. Configured Amazon Route 53 to route traffic to digitalden.cloud

Secured my website using HTTPS protocol. Requested Public Certificates from AWS Certificate Manager. Configured a CloudFront distribution for my root domain and subdomain. Updated A Records to route traffic to my CloudFront distribution.

### 4. Backend configuration
Backend consists of **API Gateway**, **Lambda** and **DynamoDB** to store and retrieve visitors count.

Created a table in DynamoDB to hold my visitor counter data. Named the table VisitorCounterTable, and created a Primary Key called visitor_id as a String Type. Changed the RCU and WCU to 1 for both to save on costs. Added visitor_counter to the table as a number type.

Created a **Lambda Function** using the Python 3.8 runtime, and allowed Lambda to create a new role with basic Lambda permissions. The execution role only gave Lambda access to write to CloudWatch logs. However,  Lambda now needs to write to DynamoDB too, so I added the AmazonDynamoDBFullAccess permission policy to the execution role.

Created an **API Gateway** and configured it to be a Trigger for my Lambda Function. Specifcally, created a REST API with a GET Method that points to my Lambda Function. Enabled Lambda Proxy Integration and CORS. Deployed the API to the Stage name of Prod.

### 5. Visitor Count
Wrote snippet of JavaScript and added visitors count to website. JavaScript on my website calls the API Gateway, the API will trigger the Lambda function which will update the count on DynamoDB and in return GET the visitors count and pass it to the webpage.

### 6. Source Control
Created a GitHub repository for my code.

### 7. CI/CD
 Implemented a CI/CD pipeline using GitHub Actions. Once I pushed my codes to GitHub repo, GitHub Actions will be triggered which will sync all my code to my S3 bucket. (Also added code that invalidates my CloudFront cache as well).
 
AWS credentials are stored in Github Action Secrets rather than in my code for security.
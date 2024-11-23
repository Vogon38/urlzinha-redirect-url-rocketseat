## **Project: URL Redirection** ##

### **Description** ###
This microservice handles requests to shortened URLs, redirecting the user to the original URL if it hasn't expired.

### **Key Features**
- **API Gateway**: Routes incoming GET requests to the Lambda function.
- Reads data from the S3 bucket based on the URL code.
- Validates if the URL has expired.
- Returns:
    - HTTP 302 with a `Location` header pointing to the original URL if valid.
    - HTTP 410 if the URL has expired.

### **Request Example** ###
```bash
GET /abcd1234
```

### **Response Examples** ###
**Valid URL**
```http
HTTP/1.1 302 Found
Location: https://example.com
```
Expired URL
```http
HTTP/1.1 410 Gone
Body: "This URL has expired"
```
### **API Gateway Configuration** ###
- **HTTP Method**: GET
- **Endpoint**: `/{code}` (path parameter for the URL code).

### ***Technologies*** ###
- AWS Lambda
- AWS S3
- API Gateway
- Java (AWS SDK v2, Jackson)

### **How to Deploy** ###
**Build the Projects**: Package the Java projects as JAR files.  
**Upload to AWS Lambda**: Deploy the JARs to two separate AWS Lambda functions:  
- **Project 1 (URL Generation)**  
- **Project 2 (URL Redirection)**  
- **Configure API Gateway**:  
    - Project 1: Create a POST endpoint `/generate` and integrate it with the URL Generation Lambda.  
    - Project 2: Create a GET endpoint `/{code}` and integrate it with the URL Redirection Lambda.  
- **Set Up S3 Bucket**: Create an S3 bucket and update the bucket name in the source code for both projects.  
- **Deploy API Gateway**: Publish your API Gateway configuration to a stage (e.g., `prod`).  

_Access the project to generate here: [GENERATE_URL](https://github.com/Vogon38/urlzinha-generate-url-rocketseat)_

### **Acknowledgments** ###
This project was developed as part of a course offered by [RocketSeat](https://www.rocketseat.com.br). 
It demonstrates the integration of AWS services with microservices architecture.

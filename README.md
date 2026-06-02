# FAQ Microservice with AWS Lambda & API Gateway

## 🚀 Project Overview

This project implements a simple **serverless FAQ microservice** that returns a random question‑answer pair in JSON format.  
The service is triggered via an **Amazon API Gateway REST endpoint**, which invokes an **AWS Lambda function** written in Node.js.  
The Lambda function selects a random FAQ from a static list and returns it through API Gateway to the client.

This lab is based on **AWS Lab SPL‑58 (Version 2.0.36)** and demonstrates core serverless concepts: event‑driven architecture, infrastructure abstraction, and integration of AWS managed services.

---

## 🏗️ Architecture

Client → HTTP GET → Amazon API Gateway → VPC Endpoint → AWS Lambda (Node.js)
← HTTP Response ← API Gateway ← VPC Endpoint ← JSON response ←


- **API Gateway**: Exposes a public REST endpoint, transforms HTTP requests to JSON, and handles responses.
- **Lambda**: Contains the business logic – selects a random FAQ and returns it.
- **CloudWatch**: Logs all invocations for debugging and monitoring.

---

## 🛠️ Technologies Used

- **AWS Lambda** (Node.js 22.x)
- **Amazon API Gateway** (REST API, Open security)
- **Amazon CloudWatch** (Logs & monitoring)
- **AWS IAM** (lambda-basic-execution role)
- **VPC & subnets** (to simulate a more secure, networked environment)

---

## 📁 Lambda Function Code

The function uses an embedded JSON array of FAQs and randomly picks one.

```
var json = {
  "service": "lambda",
  "reference": "https://aws.amazon.com/lambda/faqs/",
  "questions": [ ... ] // 20+ FAQ items
};

export const handler = function(event, context) {
    var rand = Math.floor(Math.random() * json.questions.length);
    console.log("Quote selected: ", rand);
    var response = { body: JSON.stringify(json.questions[rand]) };
    console.log(response);
    context.succeed(response);
};

```

---

## ✅ What I Accomplished
Created a custom AWS Lambda function from scratch (no blueprint).

Attached the Lambda to a VPC, subnets, and security group for network isolation.

Integrated the Lambda with API Gateway to trigger it via HTTP GET requests.

Deployed the API to a stage (myDeployment).

Tested the endpoint both via browser and directly inside the Lambda console.

Used CloudWatch Logs to verify function execution and debug.

---

## 🔬 Testing the Microservice
Via API Gateway endpoint
After creation, API Gateway provides a public URL like:

text
https://xxxxxxxxxx.execute-api.<region>.amazonaws.com/myDeployment
Visiting this URL in a browser returns a random FAQ:

json
{
  "q": "What languages does AWS Lambda support?",
  "a": "AWS Lambda supports code written in Node.js (JavaScript), Python, and Java..."
}
Via Lambda Console Test
Created a test event (BasicTest) with an empty JSON payload {}.

Invoked the function and verified the execution result and logs.

---

## 📊 Monitoring
All invocations are logged in Amazon CloudWatch under the Lambda’s log group.
Logs can be viewed directly from the Lambda console’s Monitor tab or via CloudWatch Logs Insights.

## 🧠 Key Learnings
How to build a serverless backend without managing servers.

API Gateway as a reverse proxy / REST API facade.

Lambda as a compute service triggered by HTTP events.

VPC attachment for Lambda functions (enhanced security).

CloudWatch integration for serverless debugging.

Stateless function design and random selection logic.

---

## 🚧 Possible Improvements
Add a database (DynamoDB) to store FAQs dynamically.

Implement API keys or IAM authentication.

Add caching with API Gateway or CloudFront.

Expand to support POST or query parameters (e.g., ?id=5).

Write unit tests for the Lambda function.


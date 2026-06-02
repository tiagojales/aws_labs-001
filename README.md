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

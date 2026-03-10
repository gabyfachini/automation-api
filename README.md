# Automation API Platform (n8n)

This project implements an automation API using n8n. 
The goal is to centralize multiple utility services into a single HTTP endpoint.

The client sends a request containing an `action` field, and the workflow routes the request to the corresponding service.

---

# Overview

The API acts as a simple service router.

Each request sent to the main endpoint contains an `action` field that determines which automation will be executed.

Available services:

| Service | Description |
|--------|------------|
| password-generator | Generates a secure random password |
| fake-data | Returns random user data |
| motivational-quotes | Returns a motivational quote |
| cpf-validator | Validates the basic CPF format |

---

# Workflow Architecture

Main workflow flow:

Webhook  
↓  
Router API (Switch Node)  
↓  
Service Logic  
↓  
Respond to Webhook  

Each service is implemented using:

- Function Node for logic
- Respond to Webhook for API response

---

# API Endpoint
POST /webhook/api

---

Example local URL:
http://localhost:5678/webhook/api

---

# API Usage

All requests must be sent using **POST** with JSON.

---
# Password Generator

Request:
```json
{
  "action": "password-generator"
}
```

Response:
```json
{
  "service": "password-generator",
  "password": "A8#sF2kLmP9!"
}
```
---
# Fake Data

Request:
```json
{
  "action": "fake-data"
}
```

Response:
```json
{
  "service": "fake-data",
  "nome": "Carlos",
  "cidade": "Rio",
  "idade": 34
}
```
---
# Motivational Quote

Request:
```json
{
  "action": "motivational-quotes"
}
```
Response:
```json
{
  "service": "motivational-quotes",
  "quote": "Done is better than perfect."
}
```
---
# CPF Validator

Request:
```json
{
  "action": "cpf-validator",
  "cpf": "12345678900"
}
```
Response:
```json
{
  "cpf": "12345678900",
  "valido": true
}
```
Note:
The current validation checks only the CPF format and length, not the official Brazilian CPF validation algorithm.

---
# Technologies
- n8n
- JavaScript
- HTTP Webhooks
- Workflow Automation

---
# Running the Project
- Open n8n
- Go to Workflows
- Click Import
- Paste the workflow JSON
- Activate the Workflow
- After importing: Activate Workflow 
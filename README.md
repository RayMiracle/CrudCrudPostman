# Postman CRUD API Automation Practice

This repository contains a Postman Collection and Environment designed for practicing and demonstrating automated Create, Read, Update, and Delete (CRUD) operations against a public API. It's an excellent resource for honing your Postman testing skills, including advanced scripting and validation techniques.

## 🚀 Project Aim

The primary goal of this collection is to provide a hands-on example of automating a complete CRUD workflow for a resource (a "unicorn" in this case), showcasing robust Postman testing features.

## ✨ Features

**Full CRUD Workflow:**  
Tests the creation, retrieval, updating, and deletion of a unicorn resource.

**Comprehensive Validations:**

- **Status Code Assertions:** Verifies expected HTTP status codes (e.g., 201 Created, 200 OK, 404 Not Found).
- **JSON Schema Validation (Ajv):** Ensures response bodies adhere to a predefined structure and data types using the powerful Ajv validator.
- **Full Response Body Comparison:** Confirms that updated data matches expectations by performing deep equality checks against saved responses.

**Intelligent Flow Control:**  
Uses `pm.execution.setNextRequest()` to dynamically control the collection run order, skipping redundant requests and adapting the test flow based on conditions (e.g., first vs. second GET call).

**Smart Variable Management:**

- Utilizes a `baseURL` environment variable for easy API endpoint configuration.
- Employs collection variables (`unicornId`, `fullApiResponse`, `getCallCount`, `deleteCallCount`) to pass data between requests, track execution counts, and maintain test state.

**Automated Cleanup:**  
Includes logic to clear all collection variables at the end of the test run, ensuring a clean slate for repeated executions.

## 🛠️ Prerequisites

To use this collection, you will need:

- **Postman Desktop App:**  
  Download and install Postman from [postman.com/downloads](https://www.postman.com/downloads).

- **A Free CRUD API:**  
  This collection is designed to work seamlessly with temporary endpoints from [CrudCrud.com](https://crudcrud.com). This service provides instant, temporary REST API endpoints for practicing CRUD operations without needing to set up a backend.

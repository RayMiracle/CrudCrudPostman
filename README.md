# 🦄 Postman CRUD API Automation Practice

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Postman](https://img.shields.io/badge/Postman-FF6C37?style=flat&logo=postman&logoColor=white)](https://www.postman.com/)
[![API](https://img.shields.io/badge/API-CRUD-blue)](https://crudcrud.com/)

This repository contains a comprehensive **Postman Collection** and **Environment** designed for practicing and demonstrating automated **Create, Read, Update, and Delete (CRUD)** operations against a public API. It's an excellent resource for honing your Postman testing skills, including advanced scripting and validation techniques.

## 🎯 Project Aim

The primary goal of this collection is to provide a **hands-on example** of automating a complete CRUD workflow for a resource (a "unicorn" in this case), showcasing robust Postman testing features.

## ✨ Features

### 🔄 Full CRUD Workflow
Tests the creation, retrieval, updating, and deletion of a unicorn resource.

### 🔍 Comprehensive Validations

- **Status Code Assertions**: Verifies expected HTTP status codes (e.g., `201 Created`, `200 OK`, `404 Not Found`)
- **JSON Schema Validation (Ajv)**: Ensures response bodies adhere to a predefined structure and data types using the powerful Ajv validator
- **Full Response Body Comparison**: Confirms that updated data matches expectations by performing deep equality checks against saved responses

### 🎛️ Intelligent Flow Control
Uses `pm.execution.setNextRequest()` to dynamically control the collection run order, skipping redundant requests and adapting the test flow based on conditions (e.g., first vs. second GET call).

### 🧠 Smart Variable Management

- Utilizes a `baseURL` environment variable for easy API endpoint configuration
- Employs collection variables (`unicornId`, `fullApiResponse`, `getCallCount`, `deleteCallCount`) to pass data between requests, track execution counts, and maintain test state

### 🧹 Automated Cleanup
Includes logic to clear all collection variables at the end of the test run, ensuring a clean slate for repeated executions.

## 🛠️ Prerequisites

To use this collection, you will need:

- **Postman Desktop App**: Download and install Postman from [postman.com/downloads](https://www.postman.com/downloads/)
- **A Free CRUD API**: This collection is designed to work seamlessly with temporary endpoints from [CrudCrud.com](https://crudcrud.com/). This service provides instant, temporary REST API endpoints for practicing CRUD operations without needing to set up a backend.

## 🚀 Getting Started

Follow these steps to set up and run the collection in Postman:

### 1. Clone the Repository

```bash
git clone https://github.com/RayMiracle/CrudCrudPostman.git
```

### 2. Import into Postman

1. Open Postman
2. Click on **File > Import** (or the **Import** button in the sidebar)
3. Select the **Files** tab and choose the `UnicornFarm.postman_collection.json` and `Test.postman_environment.json` files from the cloned repository
4. Click **Import**

### 3. Set up baseURL Environment Variable

1. In Postman, select the **Unicorn CRUD Environment** from the environment dropdown in the top-right corner
2. Go to the **Environments** tab in the left sidebar, select **Unicorn CRUD Environment**
3. Locate the `baseURL` variable
4. Generate a new endpoint from [CrudCrud.com](https://crudcrud.com/). Copy the base URL (e.g., `https://crudcrud.com/api/YOUR_UNIQUE_HASH`) and paste it into the **CURRENT VALUE** field for `baseURL`
5. Click **Save** (Ctrl/Cmd + S)

### 4. Initial Collection Variables (Optional)

While the scripts handle initialization, for a clean start, you can verify/set `getCallCount` and `deleteCallCount` to `0` in the **Unicorn CRUD Collection's Variables** tab.

## ▶️ How to Run the Collection

1. In Postman, navigate to the **UnicornFarm** in the left sidebar
2. Click the **Run** button (or **...** next to the collection name and select **Run collection**)
3. The Collection Runner will open. Ensure all requests are selected
4. Click **Run UnicornFarm**

### 📋 Expected Flow

The collection is designed to run through a specific sequence, demonstrating conditional logic:

1. **Create New Unicorn**: (e.g., `POST /unicorns`) - Creates a new resource
2. **Get New Unicorn (1st Call)**: (e.g., `GET /unicorns/{{unicornId}}`) - Retrieves the newly created unicorn, validates its data, and saves the full response
3. **Update Unicorn Data**: (e.g., `PUT /unicorns/{{unicornId}}`) - Modifies the unicorn's details
4. **Get New Unicorn (2nd Call)**: (e.g., `GET /unicorns/{{unicornId}}`) - Retrieves the updated unicorn, validates its new data (deep equality check), and then jumps directly to the Delete request
5. **Delete the New Unicorn (1st Call)**: (e.g., `DELETE /unicorns/{{unicornId}}`) - Deletes the unicorn, expecting a `200 OK` status
6. **Get New Unicorn (3rd Call)**: (e.g., `GET /unicorns/{{unicornId}}`) - Attempts to retrieve the deleted unicorn, expecting a `404 Not Found` status. This request then jumps back to the Delete request for a second attempt
7. **Delete the New Unicorn (2nd Call)**: (e.g., `DELETE /unicorns/{{unicornId}}`) - Attempts to delete the already-deleted unicorn, expecting a `404 Not Found` status. This is the final step, which also clears all collection variables and stops the collection run

> 📝 **Note**: Observe the "Test Results" and "Console" in Postman for detailed pass/fail information and logs.

## 🏃‍♀️ Ways to Execute Tests

This collection offers several ways to run your tests, catering to different needs:

### 1. 📊 Via Collection Runner (Recommended for full workflow)

As described in the "How to Run the Collection" section above, this is the primary method to execute the entire workflow sequentially, leveraging the `setNextRequest` logic.

### 2. 🔧 Manually Call Each Individual Request

You can open each request (`POST`, `GET`, `PUT`, `DELETE`) in Postman and click **Send** individually.

> ⚠️ **Important**: When running manually, the `setNextRequest` logic will not automatically jump to the next request. You will need to manually navigate to the next request in your desired sequence. Pay close attention to the `console.log` messages in the "Tests" tab for guidance on the expected flow and variable values.

### 3. ⏰ Via Schedule Run Feature in Postman (Postman Cloud)

Postman allows you to schedule collection runs at defined intervals in the Postman cloud.

1. Navigate to your collection, click **Run**, and then select the **Schedule runs** tab
2. Configure the frequency, environment, and notifications. This is ideal for continuous monitoring and regression testing.

### 4. 💻 Via the Postman CLI

For command-line execution and integration into CI/CD pipelines, you can use the Postman CLI.

#### Prerequisites:
- Install the Postman CLI (refer to [Postman documentation](https://learning.postman.com/docs/postman-cli/postman-cli-overview/) for installation instructions)

#### How to Generate and Run the CLI Command:

1. In Postman, open your collection and click the **Run** button
2. In the Collection Runner, select the **Automate runs via CLI** tab
3. Choose the environment you want to use (e.g., **Test**)
4. **Generate or Use an API Key**:
   - If you don't have an API Key, click **Generate API Key** and follow the prompts. Copy the generated key
   - If you have an existing API Key, select it from the dropdown
5. Postman will automatically generate the full `postman collection run` command for you, including your collection ID, environment ID, and API Key
6. Click the **Copy Command** button
7. Open your local terminal (Command Prompt, PowerShell, Git Bash, etc.) and paste the copied command
8. Press Enter to execute the collection run

### 5. 📡 Via Postman Monitor

Postman Monitors allow you to run your collections at scheduled intervals from different geographic locations to check API performance and uptime.

1. Navigate to your collection, click **Run**, and then select the **Monitors** tab
2. Create a new monitor, configure its frequency, regions, and alerts. This is excellent for ensuring your API is always available and performing well.

## 📄 Collection Structure (Example Requests)

```
📁 UnicornFarm Collection
├── 📝 POST   Create a new unicorn
├── 📖 GET    Get the new unicorn
├── ✏️ PUT    Update the new unicorn
└── 🗑️ DELETE Delete the new unicorn
```

## 🤝 Contributing

Feel free to fork this repository, experiment with the code, and suggest improvements!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

<div align="center">
  <strong>Happy Testing! 🚀</strong>
  <br>
  <em>Made with ❤️ for the Postman community</em>
</div>

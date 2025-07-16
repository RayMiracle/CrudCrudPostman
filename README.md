Postman CRUD API Automation Practice
This repository contains a Postman Collection and Environment designed for practicing and demonstrating automated Create, Read, Update, and Delete (CRUD) operations against a public API. It's an excellent resource for honing your Postman testing skills, including advanced scripting and validation techniques.

🚀 Project Aim
The primary goal of this collection is to provide a hands-on example of automating a complete CRUD workflow for a resource (a "unicorn" in this case), showcasing robust Postman testing features.

✨ Features
Full CRUD Workflow: Tests the creation, retrieval, updating, and deletion of a unicorn resource.

Comprehensive Validations:

Status Code Assertions: Verifies expected HTTP status codes (e.g., 201 Created, 200 OK, 404 Not Found).

JSON Schema Validation (Ajv): Ensures response bodies adhere to a predefined structure and data types using the powerful Ajv validator.

Full Response Body Comparison: Confirms that updated data matches expectations by performing deep equality checks against saved responses.

Intelligent Flow Control: Uses pm.execution.setNextRequest() to dynamically control the collection run order, skipping redundant requests and adapting the test flow based on conditions (e.g., first vs. second GET call).

Smart Variable Management:

Utilizes a baseURL environment variable for easy API endpoint configuration.

Employs collection variables (unicornId, fullApiResponse, getCallCount, deleteCallCount) to pass data between requests, track execution counts, and maintain test state.

Automated Cleanup: Includes logic to clear all collection variables at the end of the test run, ensuring a clean slate for repeated executions.

🛠️ Prerequisites
To use this collection, you will need:

Postman Desktop App: Download and install Postman from postman.com/downloads.

A Free CRUD API: This collection is designed to work seamlessly with temporary endpoints from CrudCrud.com. This service provides instant, temporary REST API endpoints for practicing CRUD operations without needing to set up a backend.

🚀 Getting Started
Follow these steps to set up and run the collection in Postman:

Clone the Repository:

git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
cd YOUR_REPOSITORY_NAME



(Replace YOUR_USERNAME and YOUR_REPOSITORY_NAME with your actual GitHub details.)

Import into Postman:

Open Postman.

Click on File > Import (or the Import button in the sidebar).

Select the Files tab and choose the Unicorn_CRUD_Collection.json and Unicorn_CRUD_Environment.json files from the cloned repository.

Click Import.

Set up baseURL Environment Variable:

In Postman, select the Unicorn CRUD Environment from the environment dropdown in the top-right corner.

Go to the Environments tab in the left sidebar, select Unicorn CRUD Environment.

Locate the baseURL variable.

Generate a new endpoint from CrudCrud.com. Copy the base URL (e.g., https://crudcrud.com/api/YOUR_UNIQUE_HASH) and paste it into the CURRENT VALUE field for baseURL.

Click Save (Ctrl/Cmd + S).

Initial Collection Variables (Optional):

While the scripts handle initialization, for a clean start, you can verify/set getCallCount and deleteCallCount to 0 in the Unicorn CRUD Collection's Variables tab.

▶️ How to Run the Collection
In Postman, navigate to the Unicorn CRUD Collection in the left sidebar.

Click the Run button (or ... next to the collection name and select Run collection).

The Collection Runner will open. Ensure all requests are selected.

Click Run Unicorn CRUD Collection.

Expected Flow:
The collection is designed to run through a specific sequence, demonstrating conditional logic:

Create New Unicorn: (e.g., POST /unicorns) - Creates a new resource.

Get New Unicorn (1st Call): (e.g., GET /unicorns/{{unicornId}}) - Retrieves the newly created unicorn, validates its data, and saves the full response.

Update Unicorn Data: (e.g., PUT /unicorns/{{unicornId}}) - Modifies the unicorn's details.

Get New Unicorn (2nd Call): (e.g., GET /unicorns/{{unicornId}}) - Retrieves the updated unicorn, validates its new data (deep equality check), and then jumps directly to the Delete request.

Delete the New Unicorn (1st Call): (e.g., DELETE /unicorns/{{unicornId}}) - Deletes the unicorn, expecting a 200 OK status.

Get New Unicorn (3rd Call): (e.g., GET /unicorns/{{unicornId}}) - Attempts to retrieve the deleted unicorn, expecting a 404 Not Found status. This request then jumps back to the Delete request for a second attempt.

Delete the New Unicorn (2nd Call): (e.g., DELETE /unicorns/{{unicornId}}) - Attempts to delete the already-deleted unicorn, expecting a 404 Not Found status. This is the final step, which also clears all collection variables and stops the collection run.

Observe the "Test Results" and "Console" in Postman for detailed pass/fail information and logs.

🏃‍♀️ Ways to Execute Tests
This collection offers several ways to run your tests, catering to different needs:

Via Collection Runner (Recommended for full workflow):

As described in the "How to Run the Collection" section above, this is the primary method to execute the entire workflow sequentially, leveraging the setNextRequest logic.

Manually Call Each Individual Request:

You can open each request (POST, GET, PUT, DELETE) in Postman and click Send individually.

Important: When running manually, the setNextRequest logic will not automatically jump to the next request. You will need to manually navigate to the next request in your desired sequence. Pay close attention to the console.log messages in the "Tests" tab for guidance on the expected flow and variable values.

Via Schedule Run Feature in Postman (Postman Cloud):

Postman allows you to schedule collection runs at defined intervals in the Postman cloud.

Navigate to your collection, click Run, and then select the Schedule runs tab.

Configure the frequency, environment, and notifications. This is ideal for continuous monitoring and regression testing.

Via the Postman CLI:

For command-line execution and integration into CI/CD pipelines, you can use the Postman CLI.

Prerequisites:

Install the Postman CLI (refer to Postman documentation for installation instructions).

How to Generate and Run the CLI Command:

In Postman, open your collection and click the Run button.

In the Collection Runner, select the Automate runs via CLI tab.

Choose the environment you want to use (e.g., Unicorn CRUD Environment).

Generate or Use an API Key:

If you don't have an API Key, click Generate API Key and follow the prompts. Copy the generated key.

If you have an existing API Key, select it from the dropdown.

Postman will automatically generate the full postman collection run command for you, including your collection ID, environment ID, and API Key.

Click the Copy Command button.

Open your local terminal (Command Prompt, PowerShell, Git Bash, etc.) and paste the copied command.

Press Enter to execute the collection run.

Via Postman Monitor:

Postman Monitors allow you to run your collections at scheduled intervals from different geographic locations to check API performance and uptime.

Navigate to your collection, click Run, and then select the Monitors tab.

Create a new monitor, configure its frequency, regions, and alerts. This is excellent for ensuring your API is always available and performing well.

📄 Collection Structure (Example Requests)
POST Create new unicorn

GET Get the new unicorn

PUT Update the new unicorn

DELETE Delete the new unicorn

(Note: Actual request names in the collection might vary slightly.)

🤝 Contributing
Feel free to fork this repository, experiment with the code, and suggest improvements!

📄 License
This project is open-source and available under the MIT License.

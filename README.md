# Lab 4: PhotoPipe — Event-Driven Image Processing
## CST8917 — Serverless Applications | Winter 2026

---

## Demo Video
**Watch the project demonstration here:** [(https://youtu.be/A8iloYj0Ea8)]

---

## Project Overview
**PhotoPipe** is a serverless, event-driven pipeline built on Microsoft Azure. It demonstrates how to decouple application logic using **Azure Event Grid** to handle file uploads and metadata generation.

### Key Features:
* **Automated Image Processing:** Uploading `.jpg` or `.png` files triggers a Python Azure Function to generate metadata (size, dimensions, timestamp).
* **Audit Logging:** Every upload to the system is logged to **Azure Table Storage**, regardless of file type.
* **Advanced Filtering:** Event Grid subscriptions are used to route events based on file extensions and container paths.
* **Web Dashboard:** A client interface for direct-to-blob uploads and real-time result polling.

---

## Architecture
1.  **Web Client:** Directly uploads images to Azure Blob Storage using a SAS Token.
2.  **Blob Storage:** Acts as the event source (`image-uploads` container).
3.  **Event Grid System Topic:** Captures `BlobCreated` events.
4.  **Azure Functions:**
    * `process-image`: Triggered only for image files via suffix filtering.
    * `audit-log`: Triggered for all uploads to maintain a history.
5.  **Data Storage:** * `image-results`: Stores metadata JSON files.
    * `processinglog`: Azure Table Storage for audit trails.

---

## Setup & Installation

### Prerequisites
* Azure Subscription
* Azure Functions Core Tools
* Python 3.12
* VS Code with Azure Functions Extension

### Configuration
1.  **Clone the Repository:**

2.  **Environment Variables:**
    Create a `local.settings.json` file based on the provided `local.settings.example.json` and add your **Storage Account Connection String**.

3.  **Deploy to Azure:**
    Deploy the Function App using VS Code or the Azure CLI.

4.  **Event Grid Setup:**
    Create a System Topic for your storage account and configure the two subscriptions (`process-image-sub` and `audit-log-sub`) as specified in the lab requirements.

5.  **CORS:**
    Ensure CORS is enabled for both the **Storage Account** and the **Function App** to allow requests from your local client origin.

---

## Files Included
* `function_app.py`: The Python logic for all five Azure Functions.
* `requirements.txt`: Python dependencies.
* `test-function.http`: Test requests for verifying the API.
* `client.html`: The frontend web application.
* `local.settings.example.json`: A template for local configuration.
* `README.md`: Project documentation.

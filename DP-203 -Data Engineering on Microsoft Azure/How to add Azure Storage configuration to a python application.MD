# Article 3 : How to add Azure Storage configuration to a python application? <a id="section_3"></a>
Here's a detailed step-by-step guide on how to add Azure Storage configuration to a Python application:

**1. Create a Virtual Environment (Optional but Recommended):**
   - Open a terminal or command prompt.
   - Create a new directory for your project (if not already created) and navigate to it using the `cd` command.
   - Create a virtual environment (replace `venv` with your desired name):
     ```bash
     python -m venv venv
     ```
   - Activate the virtual environment:
     - On Windows:
       ```bash
       venv\Scripts\activate
       ```
     - On macOS and Linux:
       ```bash
       source venv/bin/activate
       ```

**2. Install the Required Packages:**
   - While your virtual environment is active, install the `azure-storage-blob` package using `pip`:
     ```bash
     pip install azure-storage-blob
     ```

**3. Create an Azure Storage Account:**
   - If you haven't created an Azure Storage Account yet, you can do so through the Azure portal or the Azure CLI.

**4. Retrieve the Connection String:**
   - Once you have the storage account, obtain the connection string. You can find it in the Azure portal or use the following Azure CLI command (replace `<resource-group>` and `<storage-account-name>` with your actual values):
     ```bash
     az storage account show-connection-string --resource-group <resource-group> --name <storage-account-name> --query connectionString --output tsv
     ```
   - Copy the connection string.

**5. Create a Configuration File:**
   - In your project directory, create a `.env` file (you can use any name, but `.env` is commonly used).
   - Open the `.env` file in a text editor.

**6. Store the Connection String in the Configuration File:**
   - Add the following line to the `.env` file, replacing `<your-connection-string>` with the actual connection string:
     ```
     AZURE_STORAGE_CONNECTION_STRING=<your-connection-string>
     ```
   - Save the `.env` file.

**7. Read the Configuration in Your Python Application:**
   - In your Python application script, import the `os` module to access environment variables:
     ```python
     import os
     from azure.storage.blob import BlobServiceClient
     ```

   - Retrieve the connection string from the environment variable:
     ```python
     connection_string = os.environ.get("AZURE_STORAGE_CONNECTION_STRING")
     ```

   - Create a `BlobServiceClient` instance using the connection string:
     ```python
     blob_service_client = BlobServiceClient.from_connection_string(connection_string)
     ```

**8. Use the Azure Storage Client:**
   - You can now use the `blob_service_client` to work with your Azure Storage account, such as creating containers, uploading and downloading blobs, etc.

**9. Deactivate the Virtual Environment (When Done):**
   - When you're done working on your application, deactivate the virtual environment:
     ```bash
     deactivate
     ```

Remember that this guide provides a general overview. Depending on your application's structure and requirements, you might need to adjust certain steps. Additionally, ensure that you handle exceptions, error cases, and security considerations properly in your code.
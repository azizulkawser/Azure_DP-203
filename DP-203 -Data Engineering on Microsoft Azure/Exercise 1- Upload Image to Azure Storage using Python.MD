# Exercise 1: Upload Image to Azure Storage using Python <a id="section_4"></a>
In this exercise, you will create a Python application that uploads an image to an Azure Storage container. This exercise assumes you have an Azure Storage account and access to its connection string.

**Step 1: Set Up Your Environment**

1. Create a new directory for this exercise and navigate to it in your terminal or command prompt.
2. If you haven't already, install the Azure Storage Blob Client Library for Python using pip:
   ```bash
   pip install azure-storage-blob
   ```
3. Create a virtual environment (recommended) and activate it:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On macOS/Linux
   venv\Scripts\activate     # On Windows
   ```

**Step 2: Prepare the Image**

1. Download an image you'd like to upload to your Azure Storage account. Save it in the same directory as your Python application. Name it `image.jpg`.

**Step 3: Write the Python Application** (```Follow Article 3 on How to add Azure Storage configuration to a python application```)

Create a file named `upload_image.py` in your exercise directory and add the following code:

```python
import os
from azure.storage.blob import BlobServiceClient, BlobClient, ContainerClient

# Retrieve the Azure Storage connection string from environment variables
connection_string = os.environ.get("AZURE_STORAGE_CONNECTION_STRING")

# Create a BlobServiceClient using the connection string
blob_service_client = BlobServiceClient.from_connection_string(connection_string)

def upload_image(container_name, image_path):
    # Get a reference to the container
    container_client = blob_service_client.get_container_client(container_name)
    
    # Create the container if it doesn't exist
    container_client.create_container()

    # Upload the image
    image_name = os.path.basename(image_path)
    blob_client = container_client.get_blob_client(image_name)
    with open(image_path, "rb") as image_file:
        blob_client.upload_blob(image_file)

if __name__ == "__main__":
    container_name = "images"
    image_path = "image.jpg"
    
    try:
        upload_image(container_name, image_path)
        print("Image uploaded successfully.")
    except Exception as e:
        print("An error occurred:", str(e))
```

**Step 4: Configure Environment Variables**

1. Obtain your Azure Storage connection string from the Azure portal.
2. Set the connection string as an environment variable. In your terminal or command prompt, run (replace `<your-connection-string>` with the actual connection string):
   - On macOS/Linux:
     ```bash
     export AZURE_STORAGE_CONNECTION_STRING="<your-connection-string>"
     ```
   - On Windows:
     ```bash
     setx AZURE_STORAGE_CONNECTION_STRING "<your-connection-string>"
     ```

**Step 5: Run the Application**

1. Make sure you're in the same directory as your `upload_image.py` and `image.jpg` files.
2. Run the Python application:
   ```bash
   python upload_image.py
   ```

This exercise guides you through creating a Python application that uploads an image to an Azure Storage container. It's important to understand the steps and code you're adding to your application, as it helps you learn how to interact with Azure Storage using the Azure SDK for Python.
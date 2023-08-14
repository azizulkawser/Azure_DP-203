# Exercise 2 : Upload a Video to Azure Storage using Python <a id="section_5"></a>
In this exercise, you will create a Python application that uploads a video to an Azure Storage container. The steps include setting up the environment, creating an Azure Storage account, obtaining the connection string, creating a container, uploading the video, and verifying the upload.

**Prerequisites:**

1. **Create an Azure Storage Account:** (```OR You can follow the steps described in Article 1``` )
   - If you don't have an Azure account, sign up for a free account at https://azure.com/free.
   - Log in to the Azure portal (https://portal.azure.com).
   - Click "Create a resource" > "Storage account."
   - Choose your subscription, resource group, storage account name, and region.
   - Choose a performance option (e.g., "Standard" or "Premium") and replication option (e.g., "Locally redundant storage" or "Geo-redundant storage").
   - Click "Review + Create" and then "Create."

2. **Obtain Azure Storage Connection String:**
   - After the storage account is created, navigate to the storage account in the Azure portal.
   - In the left menu, click "Access keys."
   - Copy either of the two connection strings (Key1 or Key2) displayed.

**Steps**

1. **Set Up Your Environment:**
   - Create a new directory for this exercise and navigate to it in your terminal or command prompt.

2. **Install Required Packages:**
   - Install the Azure SDK for Python using pip:
     ```bash
     pip install azure-storage-blob
     ```

3. **Write the Python Code:** ( ```Follow Article 3 on How to add Azure Storage configuration to a python application```)

   Create a Python file named `upload_video.py` and add the following code:

   ```python
   import os
   from azure.storage.blob import BlobServiceClient, BlobClient, ContainerClient

   # Follow Article 3 on How to add Azure Storage configuration to a python application
   # Retrieve the Azure Storage connection string from environment variables
   connection_string = os.environ.get("AZURE_STORAGE_CONNECTION_STRING")
   # Create a BlobServiceClient using the connection string
   blob_service_client = BlobServiceClient.from_connection_string(connection_string)

   def upload_image(container_name, video_path):
      # Get a reference to the container
      container_client = blob_service_client.get_container_client(container_name)
      
      # Create the container if it doesn't exist
      container_client.create_container()

      # Upload the image
      video_name = os.path.basename(video_path)
      blob_client = container_client.get_blob_client(video_name)

      with open(video_path, "rb") as video_file:
         blob_client.upload_blob(video_file)
      
      return f"Uploaded {video_name} to {container_name}"


   if __name__ == "__main__":
      container_name = "videos"
      video_path = "path_to_your_video.mp4"
      
      try:
         upload_video(container_name, image_path)
         print("Image uploaded successfully.")
      except Exception as e:
         print("An error occurred:", str(e))
   ```

   Update `video_path` with the path to the video file you want to upload.

4. **Run the Python Script:**
   - Open a terminal in the project directory.
   - Run the script:
     ```bash
     python upload_video.py
     ```

   The script will create a container named "videos," upload the video to it.

Congratulations! You've successfully completed the exercise by creating an Azure Storage account, obtaining the connection string, and using a Python application to upload a video to an Azure Storage container.
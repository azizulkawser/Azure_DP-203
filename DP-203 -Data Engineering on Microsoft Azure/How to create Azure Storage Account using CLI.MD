# Article 1. How to create Azure storage account using CLI? <a id="section_1"></a>
To create an Azure Storage Account using the Azure Command-Line Interface (CLI), you can follow these steps:

1. **Install Azure CLI:** If you haven't already, you need to install the Azure CLI on your machine. You can download and install it from the official website: https://docs.microsoft.com/en-us/cli/azure/install-azure-cli

2. **Login:** Open a terminal or command prompt and log in to your Azure account using the following command:
   
   ```bash
   az login
   ```

   Follow the prompts to complete the authentication process.

3. **Create Storage Account:** Once you're logged in, you can create a new Azure Storage Account using the `az storage account create` command. Here's the basic syntax:

   ```bash
   az storage account create --name <storage-account-name> --resource-group <resource-group-name> --location <location> --sku <sku-name>
   ```

   Replace the placeholders:
   - `<storage-account-name>` with your desired name for the storage account.
   - `<resource-group-name>` with the name of the resource group where you want to create the storage account.
   - `<location>` with the Azure region where you want to create the storage account (e.g., "eastus", "westus", etc.).
   - `<sku-name>` with the desired SKU (service level). Common SKUs are "Standard_LRS" (Locally Redundant Storage) and "Premium_LRS" (Premium Locally Redundant Storage).

   Here's an example command:

   ```bash
   az storage account create --name mystorageaccount --resource-group myresourcegroup --location eastus --sku Standard_LRS
   ```

4. **Access Keys:** After creating the storage account, you might need the access keys to connect to it programmatically. You can retrieve the access keys using the following command:

   ```bash
   az storage account keys list --resource-group <resource-group-name> --account-name <storage-account-name>
   ```

5. **Additional Configuration:** You can add more configurations during the creation process, such as setting the default access tier, enabling hierarchical namespace, and more. Check the official Azure CLI documentation for more options and details.

When creating an Azure Storage Account using the Azure CLI, there are several additional configurations you can specify to customize the behavior and features of the storage account. Here are some of the commonly used additional configurations:

   1. **Access Tier (Default):** You can set the default access tier for the storage account. This determines the initial storage performance and cost. Options are "Hot" (frequent access) or "Cool" (infrequent access). The default is "Hot."

      ```bash
      --default-access-tier {Cool,Hot}
      ```

   2. **Hierarchical Namespace:** Enabling the hierarchical namespace allows you to work with data using a file system-like structure in Azure Blob Storage.

      ```bash
      --enable-hierarchical-namespace {true,false}
      ```

   3. **Encryption Settings:** You can configure encryption settings for your storage account. Encryption can be enabled at rest using service-managed keys or customer-managed keys.

      ```bash
      --encryption-services {blob,file,queue,table}
      --encryption-key-source {Microsoft.Storage,Microsoft.Keyvault}
      --encryption-keyvault {keyvault-name}
      ```

   4. **Network Rules:** You can configure network rules to restrict access to your storage account based on IP addresses or ranges.

      ```bash
      --allow-blob-public-access {Container,Blob,Disabled}
      --ip-address-range <range>
      --virtual-network <vnet-name>
      ```

   5. **Custom Domain:** You can configure a custom domain (e.g., using your own domain name) for the storage account.

      ```bash
      --custom-domain <custom-domain-name>
      --use-subdomain {true,false}
      ```

   6. **Tags:** You can assign metadata tags to your storage account for better organization and management.

      ```bash
      --tags <key1=value1 key2=value2 ...>
      ```

   7. **Data Lake Storage Gen2 Configuration:** If using Data Lake Storage Gen2, you can specify the filesystem, hierarchical namespace, and authentication settings.

      ```bash
      --filesystem <filesystem-name>
      --namespace-enabled {true,false}
      --account-kind StorageV2
      ```

   8. **Access Control:** Configure access control settings for the storage account. This includes setting up role-based access control (RBAC) and shared access signatures (SAS).

These are just a few examples of the additional configurations you can set when creating an Azure Storage Account using the Azure CLI. The available options might change over time, so it's recommended to refer to the latest Azure CLI documentation or use the `--help` flag with the `az storage account create` command to see the most up-to-date options and explanations.
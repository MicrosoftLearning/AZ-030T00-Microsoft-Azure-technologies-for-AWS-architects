# Mini-lab: Create a storage account in the portal

Every storage account must belong to an Azure resource group. A resource group is a logical container for grouping your Azure services. When you create a storage account, you have the option to either create a new resource group, or use an existing resource group. This article shows how to create a new resource group.

A general-purpose v2 storage account provides access to all of the Azure Storage services: blobs, files, queues, tables, and disks. The steps outlined here create a general-purpose v2 storage account, but the steps to create any type of storage account are similar.

To create a general-purpose v2 storage account in the Azure portal, follow these steps:

1. On the Azure portal menu, select **All services**. In the list of resources, type **Storage Accounts**. As you begin typing, the list filters based on your input. Select **Storage Accounts**.

1. On the **Storage Accounts** window that appears, choose **Add**.

1. Select the subscription in which to create the storage account.

1. Under the **Resource group** field, select **Create new**. Enter a name for your new resource group, as shown in the following image.

    ![Screenshot showing how to create a resource group in the portal](../../Linked_Image_Files/create-resource-group-for-storage.png)

1. Next, enter a name for your storage account. The name you choose must be unique across Azure. The name also must be between 3 and 24 characters in length, and can include numbers and lowercase letters only.

1. Select a location for your storage account, or use the default location.

1. Leave these fields set to their default values:

    | Field| Value|
    | :--- | :--- |
    | Deployment model| Resource Manager|
    | Performance| Standard|
    | Account kind| StorageV2 (general-purpose v2)|
    | Replication| Read-access geo-redundant storage (RA-GRS)|
    | Access tier| Hot|

1. Select **Review + Create** to review your storage account settings and create the account.

1. Select **Create**.

>:heavy_check_mark: **Note:** We will use the storage account created during this demo later in this module, in other demos/walkthroughs.
# Mini-lab: Create ARM templates by using the Azure Portal

In this mini-lab you will learn how to create, edit, and deploy an Azure Resource Manager template by using the Azure portal. This mini-lab shows you how to create an Azure Storage account, but you can use the same process to create other Azure resources.

## Generate a template using the portal

Using the Azure portal, you can configure a resource, for example, an Azure Storage account. Before you deploy the resource, you can export your configuration into a Resource Manager template. You can save the template and reuse it in the future.

1. Sign into the Azure portal: https://portal.azure.com/.

1. Select **Create a resource**

1. In **Search the Marketplace**, write ***Storage account*** and select the option it displays

1. Once in the *Storage account* view, click **Create**

1. Enter the following information:

    * **Resource group:** Select **Create new** and specify a resource group name of your choice. 
    * **Storage account name:** Give your storage account a unique name. The storage account name must be unique across all of Azure. If you get an error message saying, "The storage account name is already taken", try using **\<your name\>storage\<Today's date in MMDD\>**, for example, *jackstorage1016*.
    
    * You can use the default values for the rest of the properties.
    > **Note:** Some of the exported templates require some edits before you can deploy them.

1. Click **Review + create** at the bottom left of the screen.

    ❗️ **Note:**  Do ***not*** select **Create** in the next step.

1. Select **Download a template for automation** at the bottom right of the screen. The portal shows the generated template:

    * The main pane shows the template. It is a JSON file with six top-level elements: `schema`, `contentVersion`, `parameters`, `variables`, `resources`, and `output`.

    * There are six **parameters** defined. One of them is called **storageAccountName**. 
        > In the next section, edit the template to use a generated name for the storage account.

    * In the template, one Azure **resource** is defined. The type is `Microsoft.Storage/storageAccounts`. Note how the resource is defined and the definition structure.
    
1. Select **Download** from the top of the screen (under "Template"). 

1. Open the downloaded zip file, there are 2 files (**parameters.JSON** and **template.JSON**). Save both files to your computer. 
    > In the next section, use a template deployment tool to edit the template.

1. Select the **Parameters** tab to see the values you provided for the parameters. Write down these values. You will need them in the next section when you deploy the template.
    * Example:

        ![Parameters Template](../../Linked_Image_Files/template-parameters.png)

1. Go back to the home view pressing the **Microsoft Azure** label on the top left of the window
 
## Edit and deploy the template

The Azure portal can be used to perform some basic template editing by using a portal tool called *Template Deployment*. To edit a more complex template, consider using Visual Studio Code which provides richer editing functionality.

> **Tip:** Azure requires that each Azure service has a unique name. The deployment fails if you enter a storage account name that already exists. To avoid this issue, you can use the template function `uniquestring()` to generate a unique storage account name.

1. In the Azure portal, select **Create a resource**.

1. In **Search the Marketplace**, type **template deployment**, and select the option it displays.
(**Template deployment (deploy using custom templates)**).

1. Select **Create**.

1. Select **Build your own template in the editor** to open the editor.

1. Select **Load file** from the menu below *Edit template*, and then select the *template.json* file you downloaded in the last section.

1. Make the following three changes to the template:

    * Remove the **storageAccountName** parameter from the `parameters` element. 
    * Add one variable called **storageAccountName** as shown below to the `variables` element. The example below will generate a unique Storage Account name:
        ```JSON
        "storageAccountName": "[concat(uniqueString(subscription().subscriptionId), 'storage')]"
        ```
    * Update the name element of the `resources` (where the **Microsoft.Storage/storageAccounts** is located) to use the newly defined variable instead of the parameter:
       ```json
       "name": "[variables('storageAccountName')]",
       ```   

1. Select **Save**.

1. A form will appear

1. In the **BASICS** section of the form that appears, select the resource group you created in the last section.

1. In the **SETTINGS** section of the form, enter the values from the parameters you wrote down in Step 8 of the previous section. Here is a screenshot of a sample deployment:

    ![Azure Resource Manager templates deployment with the fields filled in using sample information.](../../Linked_Image_Files/1f-azure-resource-manager-template-tutorial-deploy.png)

1. Accept the terms and conditions and then select **Purchase**.

1. Select the bell icon (notifications) from the top of the screen to see the deployment status.
    > Wait until the deployment is completed.

1. Once the deployment is complete, select **Go to resource group** from the notification pane. You can see the deployment status was successful, and there is only one storage account in the resource group. The storage account name is a unique string generated by the template. 

## Clean up resources

When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.

1. From the options on top, click **Delete resource group**

    ![Options bar on top of resource goup](../../Linked_Image_Files/delete-resource-group-option.png)

1. You'll be asked to **TYPE THE RESOURCE GROUP NAME** to confirm the action (it's the name right under `Home` on the top left of the window)

    ![Delete confirmation window](../../Linked_Image_Files/delete-confirmation.png)

1. Now you'll be able to click the button **Delete** on the bottom of the window

1. Wait for the notifications pane to indicate that the resource has been deleted

1. We are done!

# Mini-lab: Enable system-assigned managed identity on an existing VM

## Enable managed identity

To enable system-assigned managed identity on a VM that was originally provisioned without it, your account needs the [Virtual Machine Contributor](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) role assignment. No additional Azure AD directory role assignments are required.

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/) using an account associated with the Azure subscription that contains the VM.

2. Navigate to the desired Virtual Machine and select **Identity**.

3. Under **System assigned**, **Status**, select **On** and then click **Save**.

   ![Configuration page screenshot](../../Linked_Image_Files/create-windows-vm-portal-configuration-blade.png)  

## Sign in to Azure VM using managed identity (PowerShell)

Traditionally, in order to access secured resources under its own identity, a script client would need to:

- Be registered and consented with Azure AD as a confidential/web client application.

- Sign in under its service principal using the app's credentials (which are likely embedded in the script).

With managed identities for Azure resources, your script client no longer needs to do either, as it can sign in under the managed identities for Azure resources service principal.

The following script demonstrates how to:

1. Sign in to Azure AD under the VM's managed identity for Azure resources service principal.  

2. Call an Azure Resource Manager cmdlet to get information about the VM. PowerShell takes care of managing token use for you automatically.  

   ```azurepowershell
   Add-AzAccount -identity

   # Call Azure Resource Manager to get the service principal ID for the VM's managed identity for Azure resources. 
   $vmInfoPs = Get-AzVM -ResourceGroupName <RESOURCE-GROUP> -Name <VM-NAME>
   $spID = $vmInfoPs.Identity.PrincipalId
   echo "The managed identity for Azure resources service principal ID is $spID"
   ```

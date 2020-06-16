# Mini-lab: Create VMs inside an availability set

## Prerequisites

Ensure that the following prerequisites are in place prior to this demonstration:

- Set environment variable before hand: **AdminPassword="myStr0ngPW%%"**

## Create an availability set

1. Launch Cloud Shell from the top navigation of the Azure portal.

    ![Azure portal top navigation, with Cloud Shell icon highlighted](../../Linked_Image_Files/launch_Cloud_Shell.png)

1. Check that the environment drop-down from the left-hand side of shell window says **Bash**.

    ![Environment drop-down, displaying Bash.](../../Linked_Image_Files/select_Bash_environment.png)

1. Create a resource group by running the following command: `az group create --name myResourceGroup --location westus`

1. Create a managed availability set by running the following command: `az vm availability-set create --resource-group myResourceGroup --name myAvailabilitySet --platform-fault-domain-count 2 --platform-update-domain-count 2`

## Create VMs inside an availability set

VMs must be created within the availability set to make sure they're correctly distributed across the hardware. You can't add an existing VM to an availability set after it's created.
When you create a VM with az vm create you use the --availability-set parameter to specify the name of the availability set.

1. Create two virtual machines by running the following command:

    ```
    for i in `seq 1 2`; do
    az vm create \
        --resource-group myResourceGroup \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --vnet-name MyVnet --subnet subnet1 \
        --image debian \
        --admin-password $AdminPassword \
        --admin-username azureuser \
        --no-wait
    done
    ```

1. It takes a few minutes to create and configure both VMs. When it finishes, you will have two virtual machines distributed across the underlying hardware.

1. In the Azure portal, navigate to **Resource Groups** > **myResourceGroupAvailability** > **myAvailabilitySet** and look at the availability set. You should see how the VMs are distributed across the two fault and update domains.

    ![Azure portal UI, showing the new availability set.](../../Linked_Image_Files/myResourceGroups_myAvailabilitySet.png)

## Clean up deployment

1. Run the following command to remove the resource group, VM, and all related resources: `az group delete --name myResourceGroup --yes`
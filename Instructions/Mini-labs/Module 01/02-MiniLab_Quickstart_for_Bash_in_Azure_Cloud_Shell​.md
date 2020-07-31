# Mini-lab: Quickstart for Bash in Azure Cloud Shell

This document details how to use Bash in Azure Cloud Shell in the Azure portal.

## Start Cloud Shell

1. Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

1. Launch **Cloud Shell** from the top navigation of the Azure portal.

    ![Cloud Shell icon](../../Linked_Image_Files/shell-icon.png)
    
    * If the Shell icon is not displaying, use the **ellipses icon**
        ![Ellipses icon](../../Linked_Image_Files/three-points.png)

1. If you are prompted with a message that says **"You have no storage mounted"**:

    1. Select a subscription to create a storage account and Microsoft Azure Files share.

    1. Select **Create storage**.

>:pencil: **Tip:** You are automatically authenticated for Azure CLI in every session.

## Select the Bash environment

Check that the environment drop-down from the left-hand side of shell window says **Bash**.

![Environment selector showing Bash](../../Linked_Image_Files/env-selector.png)

## Set your subscription

1. List subscriptions you have access to.

    ```
    az account list
    ```
    * Note the 'name' of the subscription 

1. Set your preferred subscription:

    ```
    az account set --subscription 'my-subscription-name'
    ```
    * Replace 'my-subscription-name' with the name of a subscription you like
    * This will change the subscription that you are working on. If you want to undo this change, simply write the following command and replace 'old-subscription-name' with the name of the subscription you want to keep using

        ```
        az account set --subscription 'old-subscription-name'
        ```

>:pencil: **Tip:** Your subscription will be remembered for future sessions in `/home/<user>/.azure/azureProfile.json`.

## Create a resource group

1. Create a new resource group in EastUS named "MyRG".

    ```
    az group create --location eastus --name MyRG
    ```

## Create a Linux VM

1. Create an Ubuntu VM in your new resource group. The Azure CLI will create SSH keys and set up the VM with them.

    ```
        az vm create -n myVM -g MyRG --image UbuntuLTS --generate-ssh-keys
    ```

2. Wait until the CLI finishes

>:heavy_check_mark: **Note:** Using `--generate-ssh-keys` instructs Azure CLI to create and set up public and private keys in your VM and `$Home` directory. By default keys are placed in Cloud Shell at `/home/<user>/.ssh/id_rsa` and `/home/<user>/.ssh/id_rsa.pub`. Your `.ssh` folder is persisted in your attached file share's 5-GB image used to persist `$Home`.

Your username on this VM will be your username used in Cloud Shell ($User@Azure:).

## SSH into your Linux VM

1. Search for your VM name in the Azure portal search bar.

1. Click on the VM named **myVM**

1. Click **Connect** to get your VM name and public IP address.

    ![Connect option](../../Linked_Image_Files/sshcmd-copy.png)

1. Under the **Connect via SSH with client**, select **"Run the example command below to connect to your VM"**

1. Notice the command:

    ```
    ssh -i <private key path> <username>@<ipaddress>
    ```

1. Run the following command with that **username** and **ipaddress**:

    ```
    ssh <username>@<ipaddress>
    ```

1. The CLI will ask you `Are you sure you want to continue connecting (yes/no)?` Type **yes** and press return

1. Upon establishing the SSH connection, the Ubuntu welcome prompt should open.

    ![Ubuntu welcome prompt](../../Linked_Image_Files/ubuntu-welcome.png)

## Cleaning up

1. To exit your ssh session, type:

    ```
    exit
    ```

1. Close the CLI window by clicking **Quit**

1. Reopen the CLI using the right top button
    ![Cloud Shell icon](../../Linked_Image_Files/shell-icon.png)

1. Delete your resource group and any resources within it.

    ```
    az group delete -n MyRG
    ```
1. When asked: `Are you sure you want to perform this operation?` Type **yes** and press return

1. Wait until the CLI finishes *(this may take a few minutes)*

1. We are done!
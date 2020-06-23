# Mini-lab: Quickstart for Bash in Azure Cloud Shell

This document details how to use Bash in Azure Cloud Shell in the Azure portal.

## Start Cloud Shell

1. Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

1. Launch **Cloud Shell** from the top navigation of the Azure portal.

![Cloud Shell icon](../../Linked_Image_Files/shell-icon.png)

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

1. Set your preferred subscription:

    ```
    az account set --subscription 'my-subscription-name'
    ```
>:pencil: **Tip:** Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.

## Create a resource group

Create a new resource group in WestUS named "MyRG".

```
az group create --location westus --name MyRG
```

## Create a Linux VM

Create an Ubuntu VM in your new resource group. The Azure CLI will create SSH keys and set up the VM with them.

```
az vm create -n myVM -g MyRG --image UbuntuLTS --generate-ssh-keys
```

>:heavy_check_mark: **Note:** Using `--generate-ssh-keys` instructs Azure CLI to create and set up public and private keys in your VM and `$Home` directory. By default keys are placed in Cloud Shell at `/home/<user>/.ssh/id_rsa` and `/home/<user>/.ssh/id_rsa.pub`. Your `.ssh` folder is persisted in your attached file share's 5-GB image used to persist `$Home`.

Your username on this VM will be your username used in Cloud Shell ($User@Azure:).

## SSH into your Linux VM

1. Search for your VM name in the Azure portal search bar.

1. Click **Connect** to get your VM name and public IP address.

    ![Connect option](../../Linked_Image_Files/sshcmd-copy.png)

1. SSH into your VM with the ssh cmd.

    ```
    ssh username@ipaddress
    ```

Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.

![Ubuntu welcome prompt](../../Linked_Image_Files/ubuntu-welcome.png)

## Cleaning up

1. Exit your ssh session.

    ```
    exit
    ```

1. Delete your resource group and any resources within it.

    ```
    az group delete -n MyRG
    ```

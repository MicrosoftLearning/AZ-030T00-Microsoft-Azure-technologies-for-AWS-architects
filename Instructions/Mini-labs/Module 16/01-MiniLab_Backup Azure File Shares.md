# Mini-lab: Back up Azure file shares

In this mini-lab, we will explore backing up a file share in the Azure portal.

## Configure a storage account with file share

**Note:** If you already have a storage account and file share, you can skip this step.

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/) and search for **Storage Accounts**.

2. **Add** a new storage account.

3. Provide the storage account information (your choice).

4. Select **Review + create** and then **Create**.

5. Access your storage account, and select **Files**.

6. Select **+ File share** and give your new file share a **Name** and a **Quota**.

7. After your file share is created **Upload a file**.

## Create a Recovery Services vault

1. In the Azure portal, type Recovery Services and select **Recovery Services vaults**.

2. Select **Add**.

3. Provide a **Name**, **Subscription**, **Resource group**, and **Location**. 

4. Your new vault should be in the same location as the file share. 

5. Select **Create**. It can take several minutes for the Recovery Services vault to be created. Monitor the status notifications in the upper right-hand area of the portal. Once your vault is created, it appears in the list of Recovery Services vaults.

6. If after several minutes the vault is not added, select **Refresh**.

## Configure file share backup

1. Open your recovery services vault.

2. Select **Backup** and create a new backup instance. 

3. From the **Where is your workload running?** drop-down menu, select **Azure**.

4. From the **What do you want to backup?** menu, select **Azure FileShare**.

5. Select **Backup**.

6. From the list of Storage accounts, **select a storage account**, and select **OK**. Azure searches the storage account for files shares that can be backed up. If you recently added your file shares, allow a little time for the file shares to appear.

7. From the File Shares list, **select one or more of the file shares** you want to backup, and select **OK.**

8. On the Backup Policy page, choose **Create New backup policy** and provide Name, Schedule, and Retention information. Select **OK**.

9. When you are finished configuring the backup select **Enable backup**. 

## Verify the file share backup

1. Explore the **Backup items** blade. There is information on backed up items and replicated items.

2. Explore the **Backup policies** blade. You can add or delete backup policies. 

3. Explore the **Backup jobs** blade. Here you can review the status of your backup jobs.

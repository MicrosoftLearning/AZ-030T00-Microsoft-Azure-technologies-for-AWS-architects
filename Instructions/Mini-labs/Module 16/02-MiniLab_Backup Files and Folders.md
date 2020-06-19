# Mini-lab: Back up files and folders

In this demonstration, we will step through the process to backup and restore files and folders from Windows to Azure.

> **Note:** This demonstration assumes you have not used the Azure Backup Agent before and need a complete installation. 

## Create a Recovery Services vault

1. In the Azure portal, type Recovery Services and click **Recovery Services vaults**.

2. Click **Add**.

3. Provide a **Name**, **Subscription**, **Resource group**, and **Location**. 

4. Click **Create**. It can take several minutes for the Recovery Services vault to be created. Monitor the status notifications in the upper right-hand area of the portal. Once your vault is created, it appears in the list of Recovery Services vaults. 

5. If after several minutes you don't observe your vault, click **Refresh**.

## Configure the vault

1. For your recovery services vault, click **Backup**.

2. From the **Where is your workload running?** drop-down menu, select **On-premises**.

3. From the **What do you want to backup?** menu, select **Files and folders**. Notice your other choices.

4. Click **Prepare infrastructure**. 

5. Click **Download Agent for Windows Server or Windows Client**. A pop-up menu prompts you to run or **save** MARSAgentInstaller.exe.

6. By default, the MARSagentinstaller.exe file is saved to your **Downloads** folder. When the installer completes, a pop-up asking if you want to run the installer, or open the folder. You **don't need** to install the agent yet. You can install the agent after you have downloaded the vault credentials.

7. Return to your recovery services vault, check the box **Already downloaded or using the latest recovery services agent**.

8. Click **Download**. After the vault credentials finish downloading, a pop-up asking if you want to open or **save** the credentials. Click **Save**. If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail. You cannot open the vault credentials. Proceed to the next step. The vault credentials are in the **Downloads** folder.

> **Note**: You must have the latest version of the MARS agent. Versions of the agent below 2.0.9083.0 must be upgraded by uninstalling and reinstalling the agent. 

## Install and register the agent
1. Locate and double-click the **MARSagentinstaller.exe** from the **Downloads** folder (or other saved location). The 
installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.
2. To complete the wizard, you need to:

   * Choose a location for the installation and cache folder.

   * Provide your proxy server info if you use a proxy server to connect to the internet.

   * Provide your user name and password details if you use an authenticated proxy.

   * If prompted, install any missing software.  

   * Provide the downloaded vault credentials

   * Enter and save the encryption passphrase in a secure location.

3. Wait for the server registration to complete. This could take a couple of minutes. 

4. The agent is now installed and your machine is registered to the vault. You're ready to configure and schedule your backup.

## Create the backup policy

1. Open the **Microsoft Azure Recovery Services** agent. You can find it by searching your machine for Microsoft Azure Recovery Services. 

2. If this is the first time you are using the agent there will be a **Warning** to create a backup policy. The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained. 

3. Click **Schedule Backup** to launch the Schedule Backup Wizard.

    * Read the **Getting Started** page.

    * **Add items** to include files and folders that you want to protect. Select just a few sample files. Note you can exclude files from the backup. 

    * Specify the **backup schedule**. You can schedule daily (at a maximum rate of three times per day) or weekly backups.

    * Select your **retention policy** settings. The retention policy specifies the duration for which the backup is stored. Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs. You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.

    * Choose your **initial backup type page** as **Automatically**. Notice there is a choice for offline backup.

    * **Confirm** your choices and **Finish** the wizard.

## Backup files and folders

1. Click **Back Up Now** to complete the initial sending over the network.

2. In the wizard, confirm your settings, and then click **Back Up**.

3. You may **Close** the wizard. It will continue to run in the background. 

4. The **Status** of your backup will show on the first page of the agent. 

5. You can **View Details** for more information.

## Explore the recover settings

1. Click **Recover data**.

2. Walkthrough the wizard making selections based on your backup settings. 

3. Notice your choices to restore from the current server or another server. 

4. Notice you can backup individual files and folders or an entire volume.

5. Select a volume and **Mount** the drive. This can take a couple of minutes.

6. Verify the mounted volume can be accessed in **File Explorer** and that your backup files are available.

7. **Unmount** the drive. 

## Explore the backup properties

1. Click **Change Properties**.

2. Explore the different tabs.

3. On the **Encryption** tab you can change the passphrase.

4. On the **Proxy Configuration** tab you can add proxy information.

5. On the **Throttling** tab you can enable internet bandwidth usage throttling. Throttling controls how network bandwidth is used during data transfer. This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic. Throttling applies to back up and restore activities.

## Delete your backup schedule

1. Click **Schedule Backup**.

2. In the wizard, select **Stop using this backup schedule and delete all the stored backups**.

3. Verify your choices and click **Finish**.

4. You will be prompted for a recovery services vault security pin.

5. In the Azure portal locate your recovery services vault.

6. Select **Properties** and then Security PIN **Generate**.

7. Copy the PIN into the Backup agent to finish deleting the schedule.
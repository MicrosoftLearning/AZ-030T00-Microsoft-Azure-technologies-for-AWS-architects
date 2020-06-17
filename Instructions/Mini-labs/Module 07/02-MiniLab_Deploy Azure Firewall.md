# Mini-lab: Deploy Azure Firewall

One way to control outbound network access from an Azure subnet is with Azure Firewall. With Azure Firewall, you can configure:

* Application rules that define fully qualified domain names (FQDNs) that can be accessed from a subnet.

* Network rules that define source address, protocol, destination port, and destination address.

For this demonstration, you create a simplified single VNet with three subnets for easy deployment. For production deployments, a hub and spoke model is recommended. The firewall is in its own VNet. The workload servers are in peered VNets in the same region with one or more subnets.

* **AzureFirewallSubnet** - the firewall is in this subnet.

* **Workload-SN** - the workload server is in this subnet. This subnet's network traffic goes through the firewall.

* **Jump-SN** - The "jump" server is in this subnet. The jump server has a public IP address that you can connect to using Remote Desktop. From there, you can then connect to (using another Remote Desktop) the workload server.

![Tutorial network infrastructure](../../Linked_Image_Files/deploy_azure_firewall_image1.png)

In this mini-lab, you learn how to:

* Set up a test network environment

* Deploy a firewall

 

## Set up the network

First, create a resource group to contain the resources needed to deploy the firewall. 

**Create a resource group**

The resource group contains all the resources for the demonstration.

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/).

2. On the Azure portal menu, select **Resource groups** or search for and select Resource groups from any page. Then select **Add**.

3. For **Resource group name**, enter *Test-FW-RG*.

4. For Subscription, select your subscription.

5. For **Resource group location**, select a location. All other resources that you create must be in the same location.

6. Select **Create**.

**Create a VNet**

This VNet will contain three subnets.

1. On the Azure portal menu or from the **Home** page, select **Create a resource**.

2. Select **Networking > Virtual network**, then **Create**

3. For **Subscription**, select your subscription.

4. For **Resource group**, select the previously created **Test-FW-RG**.

5. Under **Instance Details**, for Name, type *Test-FW-VN*.

6. For **Location**, select the same location that you used previously.

7. For **Address space**, type **10.0.0.0/16**.

8. Under **Subnet**, select **+ Add subnet**

9. For  **Subnet name** type *AzureFirewallSubnet*. The firewall will be in this subnet, and the subnet name must be AzureFirewallSubnet.

9. For **Subnet Address range**, type *10.0.1.0/26*, then **add**.

10. Accept the other default settings, and then select **Create**.

**Create additional subnets**

Next, create subnets for the jump server, and a subnet for the workload servers.

1. On the Azure portal menu, select **Resource groups** or search for and select Resource groups from any page. Then select **Test-FW-RG**.

2. Select the **Test-FW-VN** virtual network.

3. Select **Subnets** > **+Subnet**.

4. For **Name**, type *Workload-SN*.

5. For **Address range**, type *10.0.2.0/2*4.

6. Select **OK**.

Create another subnet named Jump-SN, address range *10.0.3.0/24*.

**Create virtual machines**

Now create the jump and workload virtual machines and place them in the appropriate subnets.

1. On the Azure portal menu or from the **Home** page, select **Create a resource**.

2. Select **Compute** and then select **Windows Server 2016 Datacenter** in the Featured list.

3. Enter these values for the virtual machine:

| Setting | Value |
|-------------------------|------------------|
| Resource group | **Test-FW-RG** |
| Virtual machine name | **Srv-Jump** |
| Region | Same as previous |
| Administrator user name | **azureuser** |
| Password | **Azure123456**! |


4. Under **Inbound port rules**, for **Public inbound ports**, select **Allow selected ports**.

5. For **Select inbound ports**, select **RDP (3389)**.

6. Accept the other defaults and select **Next: Disks**.

7. Accept the disk defaults and select **Next: Networking**.

8. Make sure that **Test-FW-VN** is selected for the virtual network and the subnet is **Jump-SN**.

9. For **Public IP**, accept the default new public ip address name (Srv-Jump-ip).

10. Accept the other defaults and select **Next: Management**.

11. Select **Off** to disable boot diagnostics. Accept the other defaults and select **Review + create**.

12. Review the settings on the summary page, and then select **Create**.

Use the information in the following table to configure another virtual machine named **Srv-Work**. The rest of the configuration is the same as the Srv-Jump virtual machine.

| Setting | Value |
|----------------------|-------------|
| Subnet | **Workload-SN** |
| Public IP | **None** |
| Public inbound ports | **None** |


## Deploy the firewall

Deploy the firewall into the VNet.

1. On the Azure portal menu or from the **Home** page, select **Create a resource**.

2. Type *firewall* in the search box and press **Enter**.

3. Select **Firewall** and then select **Create**.

4. On the **Create a Firewall page**, use the following table to configure the firewall:

| Setting | Value |
|--------------------------|---------------------------------------------------------------|
| Subscription | your subscription |
| Resource group | **Test-FW-RG** |
| Name | **Test-FW01** |
| Location | Select the same location that you used previously |
| Choose a virtual network | **Use existing: Test-FW-VN **|
| Public IP address | **Add new**. The Public IP address must be the Standard SKU type. | |


5. Select **Review + create.**

6. Review the summary, and then select **Create** to create the firewall.

This will take a few minutes to deploy.

7. After deployment completes, go to the **Test-FW-RG** resource group, and select the **Test-FW01 firewall**.


 

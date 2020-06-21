# Mini-lab: VNet Peering

**Note**: For this mini-lab you will need two virtual networks. 

**Configure VNet peering on the first virtual network**

1. In the **Azure portal**, select the first virtual network.

2. Under **SETTINGS**, select **Peerings**.

3. Select **+ Add**.

    + Provide a **name** for the first virtual network peering. For example, VNet1toVNet2. 

    + In the **Virtual network** drop-down, select the second virtual network you would like to peer with. 

    + Note the region, this will be needed when you configure the VPN gateway. 

    + Provide a name for the second virtual network peering. For example, VNet2toVNet1. 

    + Use the informational icons to review the network access, forwarded traffic, and gateway transit settings.

    + Check the box for **Allow gateway transit**. Note the error that the virtual network does not have a gateway. 

    + Make sure the **Allow gateway transit** check box is not selected.

    + Click **OK** to save your settings.

**Configure a VPN gateway**

1. In the **Azure portal**, search for **virtual network gateways**.

2. Select **+ Add**.

    + Provide a **name** for your virtual network gateway. For example, VNet1Gateway.

    + Ensure the gateway is in the same region as the first virtual network.

    + In the **virtual network** drop-down select the first virtual network.

    + In the **Public IP address** area, **Create new** and give the IP address a name.

    + Click **Create and review**. Address any validation errors.

    + Click **Create**. 

3. Monitor the notifications to ensure the gateway is successfully created.

**Allow gateway transit**

1. In the **Azure portal**, return to your first virtual network. 

2. On the **Overview** blade, notice the new **Connected device** for your VPN gateway.

3. Select the gateway and notice you can perform a health check and review access statistics. 

4. Return to the previous page and under **SETTINGS**, select **Peerings**.

    + Select the peering and enable **Allow gateway transit**. Notice the previous error has been resolved. 

    + Notice after making this selection, **Use remote gateways** is disabled. 

5. **Save** your changes. 

**Confirm VNet peering on the second virtual network**

1. In the **Azure portal**, select the second virtual network. 

2. Under **SETTINGS**, select **Peerings**.

3. Notice that a peering has automatically been created. The name is what you provided when the first virtual network peering was configured. 

4. Notice that the **Peering Status** is **Connected**.

5. Click the peering.

    + Notice that **Allow gateway transit** cannot be selected.

    + Use the informational icon to review the **Use remote gateways** setting.

6. **Discard** your changes. 

 

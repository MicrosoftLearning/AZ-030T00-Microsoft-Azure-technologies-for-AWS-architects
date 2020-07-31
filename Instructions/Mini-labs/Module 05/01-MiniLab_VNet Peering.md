# Mini-lab: VNet Peering

> **Note**: For this mini-lab you will need two virtual networks.

## Create virtual networks
1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/)

1. Search "Virtual network" on the searchbox on top of the page anc click on the resource of that name. A new view will appear

1. On this new view, click the `+ Add` button

1. Select your subscription and the resource group on wich you'd like your virtual networks to reside
    * If you don't have a resource group, click on "Create new" and give it any mane you like

1. Give your virtual network a name (for example: "`virtualnetwork1`"), and select any region you like

1. Click on `Review + Create`

1. Wait a few seconds

1. Click on `Create`

1. Repeat this process for `virtualnetwork2` in order to have 2 virtual networks available


## Configure VNet peering on the first virtual network

1. Select the first virtual network. A right pane will appear

1. On these right pane, on the search bar right under the virtual network's name, write "**Peerings**" and click on the option that appears.

1. Select **+ Add**. This will take you to a new view

    + Provide a **name** for the first virtual network peering. For example, VNet1toVNet2. 

    + In the **Virtual network** drop-down, select the second virtual network you would like to peer with. 

    + Note the region, this will be needed when you configure the VPN gateway. 

    + Provide a name for the second virtual network peering. For example, VNet2toVNet1. 

    + Use the informational icons to review the network access, forwarded traffic, and gateway transit settings.

    + Check the box for **Allow gateway transit**. Note the error that the virtual network does not have a gateway. 

    + Make sure the **Allow gateway transit** check box is not selected.

    + Click **OK** to save your settings.

## Configure a VPN gateway

1. In the **Azure portal**, search for **virtual network gateways**.

1. Select **+ Add**.

    + Provide a **name** for your virtual network gateway. For example, VNet1Gateway.

    + Ensure the gateway is in the same region as the first virtual network.

    + In the **virtual network** drop-down select the first virtual network.

    + In the **Public IP address** area, **Create new** and give the IP address a name.

    + Click **Create and review**. Address any validation errors.

    + Click **Create**. 

1. Wait a few moments until the gateway is successfully created (you'll see a notification when this happens)

### Allow gateway transit

1. In the **Azure portal**, return to your first virtual network. 

1. On the **Overview** blade, notice the new **Connected device** for your VPN gateway.

1. Select the gateway and notice you can perform a health check and review access statistics. 

1. Return to the previous page (clickng on the `X` on the top right) and on the search bar right under the virtual network's name, write "**Peerings**" again and click on the option that appears.

    + Select the peering 
    
    + Enable **Allow gateway transit**. Notice the previous error has been resolved. 

    + Notice after making this selection, **Use remote gateways** is disabled. 

1. **Save** your changes (with "enable gateway transit" checkbox checked)

## Confirm VNet peering on the second virtual network

1. In the **Azure portal**, select the second virtual network. 

1. On the search bar right under the virtual network's name, write "**Peerings**" and click on the option that appears.

1. Notice that a peering has automatically been created. The name is what you provided when the first virtual network peering was configured. 

1. Notice that the **Peering Status** is **Connected**.

1. Click the peering.

    + Notice that **use remote gateways ** cannot be selected.

    + Use the informational icon to review the **Use remote gateways** setting.

1. **Discard** your changes. 

 

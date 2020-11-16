# Mini-lab: Azure Security Center

Azure Security Center provides unified security management and threat protection across your hybrid cloud workloads.

## Prerequisites
To get started with Security Center, you must have a subscription to Microsoft Azure. If you do not have a subscription, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).

## Enable Security Center on your Azure subscription

1. Sign into the [Azure portal](https://azure.microsoft.com/features/azure-portal/).

1. From the portal's menu, select **Security Center**. 

    Security Center's overview page opens.

    ![Security Center's overview dashboard](../../Linked_Image_Files/overview.png)

**Security Center – Overview** provides a unified view into the security posture of your hybrid cloud workloads, enabling you to discover and assess the security of your workloads and to identify and mitigate risk. Security Center automatically, at no cost, enables any of your Azure subscriptions not previously onboarded by you or another subscription user.

You can view and filter the list of subscriptions by selecting the **Subscriptions** menu item. Security Center will adjust the display to reflect the security posture of the selected subscriptions. 

Within minutes of launching Security Center the first time, you may see:

- **Recommendations** for ways to improve the security of your connected resources.
- An inventory of your resources that are now being assessed by Security Center, along with the security posture of each.

To take full advantage of Security Center, you need to complete the steps below to enable Azure Defender and install the Log Analytics agent.

> **Tip:** To enable Security Center on all subscriptions within a management group, see [Enable Security Center on multiple Azure subscriptions](https://docs.microsoft.com/en-us/azure/security-center/onboard-management-group).

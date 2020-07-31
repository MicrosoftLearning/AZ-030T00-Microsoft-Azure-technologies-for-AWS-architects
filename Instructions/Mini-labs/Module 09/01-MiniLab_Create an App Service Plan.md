# Mini-lab: Create an App Service Plan

In this demonstration, we will create and work with Azure App Service plans.

**Create an App Service Plan**

1. Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com/). 

2. Search for and select **App Service Plans**.

3. Click **+ Add** to create a new App Service plan.

    | Setting | Value |
    | -- | -- |
    | Subscription | **Choose your subscription** |
    | Resource Group | **myRGAppServices** (create new) |
    | Name | **AppServicePlan1** |
    | Operating System | **Windows** |
    | Region | **East US** |

4. Click **Review + Create** and then **Create**.

5. Wait for your new App Service plan to deploy.

**Review Pricing Tiers**

1. Locate your new App Service plan.

2. Under **Settings**, click **Scale up (App Service Plan)**.

3. Notice there are three tiers: **Dev/Test**, **Production**, and **Isolated**.

4. Click each tier and review the included features and included hardware.

5. How do the tiers compare? 

**Review autoscaling**

1. Under **Settings** click **Scale out (App Service Plan)**.

2. Notice the default is **Manual scale**.

3. Notice you can specify an **instance count** depending on your App Service plan selection.

4. Click **Custom autoscale**.

5. Notice two scale modes: **Scale based on a metric** and **Scale to a specific instance count**.

6. Click **Add a rule**. 

>**Note**: This rule will add an instance when the CPU percentages is greater than 80% for 10 minutes.

| Setting | Value |
| - | - |
| Time aggregation | **Average** |
| Metric name | **CPU percentage** |
| Operator | **Greater than** |
| Threshold | **80** |
| Duration | **10 minutes** |
| Operation | **Increase count by** |
| Instance count | **1** |
| Cool down | **5 minutes** |

7. **Add** your rule changes.

8. Review the **Instance limits**: **Minimum**, **Maximum**, and **Default**.

9. Notice that you can add a **Schedule** and **Specify start/end dates** and **Repeat specific days**.

10. Observe how you can create different App Service plans for your apps.

## Clean up resources

When the Azure resources are no longer needed, clean up the resources you deployed. You may want to save environment for the demo in the next lesson (Deploy staging slots).

# Mini-lab: Register an app with the Microsoft Identity platform

In this demo you'll learn how to perform the following actions:

* Register an application with the Microsoft identity platform

## Prerequisites

This demo is performed in the Azure Portal.

### Login to the Azure Portal

1.  Login to the portal: [https://portal.azure.com](https://portal.azure.com) 


## Register a new application

1. Search for and select **Azure Active Directory**. On the **Active Directory** page, select **App registrations** and then select **New registration**.

2. When the **Register an application** page appears, enter your application's registration information:

    <table>
    <thead>
    <tr>
    <th>Field</th>
    <th>Value</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><p><strong>Name</strong></p></td>
    <td><p><code>az204appregdemo</code></p></td>
    </tr>
    <tr>
    <td><p><strong>Supported account types</strong></p></td>
    <td><p>Select <strong>Accounts in this organizational directory</strong></p></td>
    </tr>
    <tr>
    <td><p><strong>Redirect URI (optional)</strong></p></td>
    <td><p>Select <strong>Public client/native (mobile &amp; desktop)</strong> and enter <code>http://localhost</code> in the box to the right.</p></td>
    </tr>
    </tbody>
    </table>

    <!--
    Field | Value 
    - | - 
    **Name** | `az204appregdemo` | Enter a meaningful application name that will be displayed to users of the app.
    **Supported account types** | Select **Accounts in this organizational directory** 
    **Redirect URI (optional)** | Select **Public client/native (mobile & desktop)** and enter `http://localhost` in the box to the right.
    -->

    Below are more details on the **Supported account types**.

    Account type | Scope
    - | -
    **Accounts in this organizational directory only** | This option maps to Azure AD only single-tenant (only people in your Azure AD directory).
    **Accounts in any organizational directory** | This option maps to an Azure AD only multi-tenant. Select this option if you would like to target anyone from any Azure AD directory.
    **Accounts in any organizational directory and personal Microsoft accounts** | This option maps to Azure AD multi-tenant and personal Microsoft accounts. 

3. Select **Register**.

    ![Shows the screen to register a new application in the Azure portal](../../linked_image_files/new-app-registration-expanded.png)

Azure AD assigns a unique application (client) ID to your app, and you're taken to your application's **Overview** page. 
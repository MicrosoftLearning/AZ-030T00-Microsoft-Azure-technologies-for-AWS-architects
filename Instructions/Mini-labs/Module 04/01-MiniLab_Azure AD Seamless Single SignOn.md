# Mini-lab: Azure Active Directory Seamless Single Sign-On

 


Azure Active Directory (Azure AD) Seamless Single Sign-On (Seamless SSO) automatically signs in users when they are on their corporate desktops that are connected to your corporate network. Seamless SSO provides your users with easy access to your cloud-based applications without needing any additional on-premises components.


## Prerequisites

Ensure that the following prerequisites are in place prior to this mini-lab:

* **Set up your Azure AD Connect server**: If you use Pass-through Authentication as your sign-in method, no additional prerequisite check is required. If you use password hash synchronization as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:

	* You use version 1.1.644.0 or later of Azure AD Connect.
	
	* If your firewall or proxy allows DNS whitelisting, whitelist the connections to the *.msappproxy.net URLs over port 443. 


* **Set up domain administrator credentials**: You need to have domain administrator credentials for each Active Directory forest that:

	* You synchronize to Azure AD through Azure AD Connect.
	
	* Contains users you want to enable for Seamless SSO.

## Enable Azure AD Connect

1. Enable Seamless SSO through [Azure AD Connect](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/whatis-hybrid-identity).

	* If you're doing a fresh installation of Azure AD Connect, choose the [custom installation path](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-install-custom). On the **User sign-in** page, check the **Enable single sign on option**.

		![Azure AD Connect: User sign-in](../../Linked_Image_Files/SSO_demo_image1.png)

	* If you already have an installation of Azure AD Connect, select the **Change user sign-in** page in Azure AD Connect, and then select **Next**.

		![Azure AD Connect: Change the user sign-in](../../Linked_Image_Files/SSO_demo_image2.png)

1. Continue through the wizard until you get to the **Enable single sign on** page. Provide domain administrator credentials for each Active Directory forest that:

	* You synchronize to Azure AD through Azure AD Connect.

	* Contains users you want to enable for Seamless SSO.

1. After completion of the wizard, Seamless SSO is enabled on your tenant.

## Verify Seamless SSO is enabled

Follow procedure below to verify that you have enabled Seamless SSO correctly:

1.Sign in to the [Azure Active Directory administrative center](https://aad.portal.azure.com/) with the global administrator credentials for your tenant.

1. Select **Azure Active Directory** in the left pane.

1. Select **Azure AD Connect**.

1. Verify that the Seamless single sign-on feature appears as *Enabled*.

	![Azure portal: Azure AD Connect pane](../../Linked_Image_Files/SSO_demo_image3.png)

>Important

Seamless SSO creates a computer account named AZUREADSSOACC in your on-premises Active Directory (AD) in each AD forest. The AZUREADSSOACC computer account needs to be strongly protected for security reasons. Only Domain Admins should be able to manage the computer account. Ensure that Kerberos delegation on the computer account is disabled and that no other account in Active Directory has delegation permissions on the AZUREADSSOACC computer account. Store the computer account in an Organization Unit (OU) where they are safe from accidental deletions and where only Domain Admins have access.

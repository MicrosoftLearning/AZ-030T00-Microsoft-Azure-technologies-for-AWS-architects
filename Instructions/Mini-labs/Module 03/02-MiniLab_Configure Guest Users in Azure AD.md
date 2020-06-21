# Mini-lab: Add Guest users to Azure AD in the Azure Portal

You can invite anyone to collaborate with your organization by adding them to your directory as a guest user. Then you can either send an invitation email that contains a redemption link or send a direct link to an app you want to share. 

Guest users can sign in with their own work, school, or social identities.

In this mini-lab, you'll add a new guest user to Azure AD and send an invitation.

## Prerequisites

To complete the scenario in this mini-lab you need:

* A role that allows you to create users in your tenant directory, like the Global Administrator role or any of the limited administrator directory roles.

* A valid email account that you can add to your tenant directory, and that you can use to receive the test invitation email.

## Add Guest users to Azure AD

1. Sign in to the [Azure portal](https://portal.azure.com/) as an Azure AD administrator.

2. In the left pane, select **Azure Active Directory**.

3. Under **Manage**, select **Users**.

    ![Screenshot showing where to select the Users option](../../Linked_Image_Files/guest_user_image1.png)

4. Select **New guest user**.

    ![Screenshot showing where to select the New guest user option](../../Linked_Image_Files/guest_user_image2.png)

5. On the **New user** page, select **Invite user** and  add the guest user's information.

    ![Screenshot showing where to select the New guest user option](../../Linked_Image_Files/guest_user_image3.png)

    - **Name** The first and last name of the guest user.

    - **Email address (required)** The email address of the guest user.

    - **Personal message (optional)** Include a personal welcome message to the guest user.

    - **Groups** You can add the guest user to one or more existing groups, or you can do it later.

    - **Directory role** If you require Azure AD administrative permissions for the user, you can add them to an Azure AD role.

6. Select **Invite** to automatically send the invitation to the guest user. A notification appears in the upper right with the message Successfully invited user.

7. After you send the invitation, the user account is automatically added to the directory as a guest.

## Assign an App to a Guest user

Add the *Active Directory for GitHub Enterprise* app to your test tenant and assign the test guest user to the app.

1. Sign in to the Azure portal as an Azure AD administrator.

2. In the left pane, select **Enterprise applications**.

3. Select **New application**.

    ![Screenshot showing the Add from the gallery search box](../../Linked_Image_Files/guest_user_image4.png)

4. Under **Add from the gallery**, search for **GitHub**, and then select **Active Directory for GitHub Enterprise**.

    ![Screenshot showing the Add from the gallery search box](../../Linked_Image_Files/guest_user_image6.png)

5. Select **Add**.

6. Under Manage, select Single **sign-on**, and under **Single Sign-on Mode**, select **Password-based Sign-on**, and click **Add**.

    ![Screenshot showing the Add from the gallery search box](../../Linked_Image_Files/guest_user_image7.png)

7. Under **Manage**, select **Users and groups > Add user > Users and groups**, click **Select**.

    ![Screenshot showing Add user to group.](../../Linked_Image_Files/guest_user_image9.png)

8. Select **Assign**.

## Accept the Guest user invite

Now sign in to the guest user email account to view the invitation.

1. Sign in to your test guest user's email account.

2. In the inbox, find the "*You're invited*" email.

3. In the email body, select Get Started. A Review permissions page opens in the browser.

4. Select **Accept Invitation**. The Access Panel opens, which lists the applications the guest user can access.

    ![Screenshot showing the Review permissions page](../../Linked_Image_Files/guest_user_image5.png)

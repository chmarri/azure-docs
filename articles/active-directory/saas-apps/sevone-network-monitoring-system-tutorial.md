---
title: 'Tutorial: Azure AD SSO integration with SevOne Network Monitoring System (NMS)'
description: Learn how to configure single sign-on between Azure Active Directory and SevOne Network Monitoring System (NMS).
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 11/21/2022
ms.author: jeedes

---

# Tutorial: Azure AD SSO integration with SevOne Network Monitoring System (NMS)

In this tutorial, you'll learn how to integrate SevOne Network Monitoring System (NMS) with Azure Active Directory (Azure AD). When you integrate SevOne Network Monitoring System (NMS) with Azure AD, you can:

* Control in Azure AD who has access to SevOne Network Monitoring System (NMS).
* Enable your users to be automatically signed-in to SevOne Network Monitoring System (NMS) with their Azure AD accounts.
* Manage your accounts in one central location - the Azure portal.

## Prerequisites

To get started, you need the following items:

* An Azure AD subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/free/).
* SevOne Network Monitoring System (NMS) single sign-on (SSO) enabled subscription.
* Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Azure AD.
For more information, see [Azure built-in roles](../roles/permissions-reference.md).

## Scenario description

In this tutorial, you configure and test Azure AD SSO in a test environment.

* SevOne Network Monitoring System (NMS) supports **SP** initiated SSO.

> [!NOTE]
> Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add SevOne Network Monitoring System (NMS) from the gallery

To configure the integration of SevOne Network Monitoring System (NMS) into Azure AD, you need to add SevOne Network Monitoring System (NMS) from the gallery to your list of managed SaaS apps.

1. Sign in to the Azure portal using either a work or school account, or a personal Microsoft account.
1. On the left navigation pane, select the **Azure Active Directory** service.
1. Navigate to **Enterprise Applications** and then select **All Applications**.
1. To add new application, select **New application**.
1. In the **Add from the gallery** section, type **SevOne Network Monitoring System (NMS)** in the search box.
1. Select **SevOne Network Monitoring System (NMS)** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

 Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, as well as walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Azure AD SSO for SevOne Network Monitoring System (NMS)

Configure and test Azure AD SSO with SevOne Network Monitoring System (NMS) using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between an Azure AD user and the related user at SevOne Network Monitoring System (NMS).

To configure and test Azure AD SSO with SevOne Network Monitoring System (NMS), perform the following steps:

1. **[Configure Azure AD SSO](#configure-azure-ad-sso)** - to enable your users to use this feature.
    1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with B.Simon.
    1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable B.Simon to use Azure AD single sign-on.
1. **[Configure SevOne Network Monitoring System (NMS) SSO](#configure-sevone-network-monitoring-system-nms-sso)** - to configure the single sign-on settings on application side.
    1. **[Create SevOne Network Monitoring System (NMS) test user](#create-sevone-network-monitoring-system-nms-test-user)** - to have a counterpart of B.Simon in SevOne Network Monitoring System (NMS) that is linked to the Azure AD representation of user.
1. **[Test SSO](#test-sso)** - to verify whether the configuration works.

## Configure Azure AD SSO

Follow these steps to enable Azure AD SSO in the Azure portal.

1. In the Azure portal, on the **SevOne Network Monitoring System (NMS)** application integration page, find the **Manage** section and select **single sign-on**.
1. On the **Select a single sign-on method** page, select **SAML**.
1. On the **Set up single sign-on with SAML** page, click the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png "Basic Configuration")

1. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type the URL:
    `https://azwcusehnmspas01.corp.microsoft.com/sso/callback`

    b. In the **Reply URL** textbox, type a URL using the following pattern:
    `https://azwcusehnmspas01.corp.microsoft.com/sso/callback`

    c. In the **Sign on URL** text box, type the URL:
    `https://azwcusehnmspas01.corp.microsoft.com/sso/callback`

    d. In the **Relay State** text box, type the value:
    `sevonenms`

1. SevOne Network Monitoring System (NMS) application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attribute mappings.](common/default-attributes.png "Attributes")

1. In addition to above, SevOne Network Monitoring System (NMS) application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute|
    | ------------ | --------- |
    | displayname | user.displayname |   

1. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section,  find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png "Certificate")

1. On the **Set up SevOne Network Monitoring System (NMS)** section, copy the appropriate URL(s) based on your requirement.

	![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png "Metadata")  

### Create an Azure AD test user

In this section, you'll create a test user in the Azure portal called B.Simon.

1. From the left pane in the Azure portal, select **Azure Active Directory**, select **Users**, and then select **All users**.
1. Select **New user** at the top of the screen.
1. In the **User** properties, follow these steps:
   1. In the **Name** field, enter `B.Simon`.  
   1. In the **User name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
   1. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
   1. Click **Create**.

### Assign the Azure AD test user

In this section, you'll enable B.Simon to use Azure single sign-on by granting access to SevOne Network Monitoring System (NMS).

1. In the Azure portal, select **Enterprise Applications**, and then select **All applications**.
1. In the applications list, select **SevOne Network Monitoring System (NMS)**.
1. In the app's overview page, find the **Manage** section and select **Users and groups**.
1. Select **Add user**, then select **Users and groups** in the **Add Assignment** dialog.
1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then click the **Select** button at the bottom of the screen.
1. If you are expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
1. In the **Add Assignment** dialog, click the **Assign** button.

## Configure SevOne Network Monitoring System (NMS) SSO

To configure single sign-on on **SevOne Network Monitoring System (NMS)** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from Azure portal to [SevOne Network Monitoring System (NMS) support team](mailto:support@sevone.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create SevOne Network Monitoring System (NMS) test user

In this section, you create a user called Britta Simon at SevOne Network Monitoring System (NMS). Work with [SevOne Network Monitoring System (NMS) support team](mailto:support@sevone.com) to add the users in the SevOne Network Monitoring System (NMS) platform. Users must be created and activated before you use single sign-on.

## Test SSO 

In this section, you test your Azure AD single sign-on configuration with following options. 

* Click on **Test this application** in Azure portal. This will redirect to SevOne Network Monitoring System (NMS) Sign-On URL where you can initiate the login flow. 

* Go to SevOne Network Monitoring System (NMS) Sign-On URL directly and initiate the login flow from there.

* You can use Microsoft My Apps. When you click the SevOne Network Monitoring System (NMS) tile in the My Apps, this will redirect to SevOne Network Monitoring System (NMS) Sign-On URL. For more information about the My Apps, see [Introduction to the My Apps](../user-help/my-apps-portal-end-user-access.md).

## Next steps

Once you configure SevOne Network Monitoring System (NMS) you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-aad).
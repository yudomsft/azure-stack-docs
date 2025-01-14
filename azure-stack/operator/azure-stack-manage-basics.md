---
title: Azure Stack administration basics | Microsoft Docs
description: Learn the basics of Azure Stack administration.
services: azure-stack
documentationcenter: ''
author: justinha
manager: femila
editor: ''

ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2019
ms.author: justinha
ms.lastreviewed: 05/29/2019

---
# Azure Stack administration basics

If you're new to Azure Stack administration, there are several things you need to know. This article provides an overview of your role as an Azure Stack operator, and what you need to tell your users to help them become productive.

## Understand the builds

### Integrated systems

If you're using an Azure Stack integrated system, update packages distribute updated versions of Azure Stack. You can import these packages and apply them by using the **Updates** tile in the administrator portal.
 
### Development kit

If you're using the Azure Stack Development Kit (ASDK), review [What is Azure Stack?](../asdk/asdk-what-is.md) to learn the purpose and limitations of the ASDK. You can use the ASDK as a *sandbox*, where you can evaluate Azure Stack and develop and test your apps in a non-production environment. For deployment information, see [Azure Stack Development Kit deployment](../asdk/asdk-install.md).

Like Azure, we innovate rapidly. We'll regularly release new builds. If you're running the ASDK and you want to move to the latest build, you must [redeploy Azure Stack](../asdk/asdk-redeploy.md). You can't apply update packages. This process takes time, but the benefit is that you can try out the latest features. The ASDK documentation on our website reflects the latest release build.

## Learn about available services

You'll need an awareness of which services you can make available to your users. Azure Stack supports a subset of Azure services. The list of supported services will continue to evolve.

**Foundational services**

By default, Azure Stack includes the following "foundational services" when you deploy Azure Stack:

- Compute
- Storage
- Networking
- Key Vault

With these foundational services, you can offer Infrastructure-as-a-Service (IaaS) to your users with minimal configuration.

**Additional services**

Currently, we support the following additional Platform-as-a-Service (PaaS) services:

- App Service
- Azure Functions
- SQL and MySQL databases
- Kubernetes (in preview)

These services require additional configuration before you can make them available to your users. For more information, see the "Tutorials" and the "How-to guides\Offer services" sections of our Azure Stack operator documentation.

**Service roadmap**

Azure Stack will continue to add support for Azure services. For the projected roadmap, see the [Azure Stack: An extension of Azure](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409) whitepaper. You can also monitor the [Azure Stack blog posts](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview) for new announcements.

## What account should I use?
There are a few account considerations to be aware of when managing Azure Stack. Especially in deployments using Windows Server Active Directory Federation Services (AD FS) as the identity provider instead of Azure Active Directory (Azure AD). The following account considerations apply to both Azure Stack integrated systems and ASDK deployments:


|Account|Azure AD|AD FS|
|-----|-----|-----|
|Local Administrator (.\Administrator)|ASDK host administrator.|ASDK host administrator.|
|AzureStack\AzureStackAdmin|ASDK host administrator.<br><br>Can be used to sign in to the Azure Stack administrator portal.<br><br>Access to view and administer Service Fabric rings.|ASDK host administrator.<br><br>No access to the Azure Stack administrator portal.<br><br>Access to view and administer Service Fabric rings.<br><br>No longer owner of the Default Provider Subscription (DPS).|
|AzureStack\CloudAdmin|Can access and run permitted commands within the privileged endpoint.|Can access and run permitted commands within the privileged endpoint.<br><br>Can't sign in to the ASDK host.<br><br>Owner of the Default Provider Subscription (DPS).|
|Azure AD Global Administrator|Used during installation.<br><br>Owner of the Default Provider Subscription (DPS).|Not applicable.|
|

## What tools do I use to manage?
 
You can use the [administrator portal](azure-stack-manage-portals.md) or PowerShell to manage Azure Stack. The easiest way to learn the basic concepts is through the portal. If you want to use PowerShell, there are preparation steps. Before you get started, you might want to get familiar with how PowerShell is used on Azure Stack. For more information, see [Get started with PowerShell on Azure Stack](../user/azure-stack-powershell-overview.md).

Azure Stack uses Azure Resource Manager as its underlying deployment, management, and organization mechanism. If you're going to manage Azure Stack and help support users, you can learn about Resource Manager. See the [Getting Started with Azure Resource Manager](https://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) whitepaper.

## Your typical responsibilities

Your users want to use services. From their perspective, your main role is to make these services available to them. Decide which services to offer, and make those services available by creating plans, offers, and quotas. For more information, see [Overview of offering services in Azure Stack](azure-stack-offer-services-overview.md). 

You'll also need to add items to [Azure Stack Marketplace](azure-stack-marketplace.md). The easiest way is to [download marketplace items from Azure to Azure Stack](azure-stack-download-azure-marketplace-item.md).

> [!NOTE]
> If you want to test your plans, offers, and services, you can use the [user portal](azure-stack-manage-portals.md); not the administrator portal.

In addition to providing services, you must do the regular duties of an operator to keep Azure Stack up and running. These duties include the following tasks:

- Add user accounts (for [Azure AD](azure-stack-add-new-user-aad.md) deployment or for [AD FS](azure-stack-add-users-adfs.md) deployment).
- [Assign role-based access control (RBAC) roles](azure-stack-manage-permissions.md) (This task isn't restricted to admins.)
- [Monitor infrastructure health](azure-stack-monitor-health.md).
- Manage [network](azure-stack-viewing-public-ip-address-consumption.md) and [storage](azure-stack-manage-storage-accounts.md) resources.
- Replace bad hardware. For example, [replace a failed disk](azure-stack-replace-disk.md).

## What to tell your users

You'll need to let your users know how to work with services in Azure Stack, how to connect to the environment, and how to subscribe to offers. Besides any custom documentation that you may want to provide your users, you can direct users to [Azure Stack User Documentation](https://docs.microsoft.com/en-us/azure-stack/user/).

**Understand how to work with services in Azure Stack**

There's information your users must understand before they use services and build apps in Azure Stack. For example, there are specific PowerShell and API version requirements. Also, there are some feature deltas between a service in Azure and the equivalent service in Azure Stack. Make sure that your users review the following articles:

- [Key considerations: Using services or building apps for Azure Stack](../user/azure-stack-considerations.md)
- [Considerations for Virtual Machines in Azure Stack](../user/azure-stack-vm-considerations.md)
- [Storage: differences and considerations](../user/azure-stack-acs-differences.md)

The information in these articles summarizes the differences between a service in Azure and Azure Stack. It supplements the information that's available for an Azure service in the global Azure documentation.

**Connect to Azure Stack as a user**

In an ASDK environment, if a user doesn't use Remote Desktop to connect to the ASDK host, they can configure a virtual private network (VPN) connection to connect to Azure Stack. See [Connect to Azure Stack](../asdk/asdk-connect.md).

Your users will want to know how to [access the user portal](../user/azure-stack-use-portal.md) or how to connect through PowerShell. In an integrated systems environment, the user portal address varies per deployment. You'll need to provide your users with the correct URL.

If using PowerShell, users may have to register resource providers before they can use services. A resource provider manages a service. For example, the networking resource provider manages resources like virtual networks, network interfaces, and load balancers. They must [install](azure-stack-powershell-install.md) PowerShell, [download](azure-stack-powershell-download.md) additional modules, and [configure](../user/azure-stack-powershell-configure-user.md) PowerShell (which includes resource provider registration).

**Subscribe to an offer**

Before a user can use services, they must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that you've created as an operator.

## Where to get support

> [!Note]  
> To find support information for earlier releases of Azure Stack (pre-1905), see [Help and Support for earlier releases Azure Stack (pre-1905)](azure-stack-servicing-policy.md).

### Integrated systems

For an integrated system, there's a coordinated escalation and resolution process between Microsoft and our original equipment manufacturer (OEM) hardware partners.

If there's a cloud services issue, support is offered through Microsoft Customer Support Services (CSS). To open a support request, select the Help and support icon (question mark) in the upper-right corner of the administrator portal, select **Help + support**, and then select **New support request** under the **Support** section.

If there's an issue with deployment, patch and update, hardware (including field replaceable units), or any hardware-branded software, like software running on the hardware lifecycle host, contact your OEM hardware vendor first.

For anything else, contact Microsoft CSS.

### Azure Stack Development Kit (ASDK)

For the ASDK, you can ask support-related questions in the [Microsoft forums](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). To get to the forums, select the Help and support icon (question mark) in the upper-right corner of the administrator portal, then select **Help + support**, and then select **MSDN Forums** under the **Support** section. These forums are regularly monitored. Because the ASDK is an evaluation environment, there's no official support offered through Microsoft CSS.

## Next steps

[Region management in Azure Stack](azure-stack-region-management.md)
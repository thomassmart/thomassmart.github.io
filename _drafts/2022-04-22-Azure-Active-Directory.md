---
layout: post
title:  Azure Active Directory
date:   2022-04-22
tags: azure 100-days-of-azure AzureAD
---

# Who are you?

If you've been reading along the past few posts, you should be familiar with Azure, and it's global reach. You may also recall the terminology around Azure Tenancies. Each tenant, in reality they are instances of Azure AD. Cool, so it's used. A lot. But what is it?

Azure Active Directory (Azure AD) is a service that provides identity and access in the cloud. This platform allows staff to access external resources such as Microsoft 365, the Azure portal, and hundreds of other SaaS apps. They may also use Azure Active Directory to access internal resources, such as apps on a company intranet network and any cloud apps the the organisation has built.

![Azure Ad](/assets/img/100daysofazure/AzureAD.png)

# How's this different to AD?

Although Azure AD and Active Directory are connected, there are several fundamental differences between them. 

In Windows 2000, Microsoft launched Active Directory, which enabled organisations to manage multiple on-premises infrastructure systems and components using a single user profile. 
Active Directory on Windows Server provides a self-managed identity and access management solution for on-premises environments. Microsoft's Azure AD identity and access management solution is hosted in the cloud. You manage the identity accounts using Azure AD, but Microsoft assures that the service is available globally. Azure AD will be intuitive to anyone who's ever dealt with Active Directory.

Microsoft does not track sign-in attempts when you use Active Directory to safeguard identities on-premises. When you link Active Directory to Azure AD, Microsoft can help secure the organisation for no additional cost by identifying questionable sign-in attempts. Sign-in attempts from unusual places or unrecognised devices, for example, can be detected by Azure AD.

Here's what Azure AD doesn't do when compared to AD:

* It does not allow you to connect a server to it.
* It does not have Group Policy. For device management, investigate InTune.
* LDAP, NTLM, and Kerberos are not supported.
* There are no OUs or Forests within the directory structure.

# Licensing
Like many services within Azure, a number of features are offered for free. Enough to enable you to consume other products within Azure, or to entice you to upgrade to gain access to additional features.

There are 4 main licenses for Azure AD:

1. **Azure Active Directory Free**
User and group administration, synchronisation with on-premises directories, basic reporting, self-service password change for cloud users, and single sign-on across Azure, Microsoft 365, and many popular SaaS apps are all available.

2. **Azure Active Directory Premium P1**
In addition to the Free features, P1 also lets your hybrid users access both on-premises and cloud resources. It also supports advanced administration, such as dynamic groups, self-service group management, Microsoft Identity Manager, and cloud write-back capabilities, which allow self-service password reset for your on-premises users.

3. **Azure Active Directory Premium P2**
In addition to the Free and P1 features, P2 also offers Azure Active Directory Identity Protection to help provide risk-based Conditional Access to your apps and critical company data and Privileged Identity Management to help discover, restrict, and monitor administrators and their access to resources and to provide just-in-time access when needed.

4. **Pay as you go" feature licenses**
You can also get additional feature licenses, such as Azure Active Directory Business-to-Customer (B2C). B2C can help you provide identity and access management solutions for your customer-facing apps.

# Features

Azure AD does a lot, to summarise though:

1. **Authentication**
This includes confirming a user's identification in order to have access to apps and resources. Self-service password reset, multifactor authentication (MFA), a customizable list of prohibited passwords, and smart lockout services are among the features available.

2. **Single Sign-On (SSO)**
SSO allows you to access various applications with just one login and password. The security approach is simplified by the use of a single identity for each user. When users change positions or depart an organisation, access adjustments are associated to that identity, which considerably lowers the work required to alter or delete accounts.

3. **Application Management**
Azure AD may be used to manage both cloud and on-premises applications. User experience is improved through features such as Application Proxy, SaaS apps, the My Apps site (also known as the access panel), and single sign-on. Users can be internal or external, and be allowed to self service access, or be assigned based on various signals.

4. **Device Management**
Azure AD offers the registration of devices in addition to individual user accounts. Devices that have been registered may be handled using technologies like Microsoft Intune. It also enables device-based Conditional Access settings to limit access attempts to recognised devices exclusively, independent of the requesting user account.

They'll be topics on different aspects of Azure AD in coming posts. Promise.

# Additional Resources

| Style | Link |
| --- | --- |
| Visual Learner | [John Savill -  Azure AD Overview](https://www.youtube.com/watch?v=EUVKEhiHYG0) |
| Auditory Learner | [365 Days of Cloud Podcast](https://podcasts.apple.com/au/podcast/azure-active-directory/id1528148762?i=1000507165417) |
| Physical Learner | [Sign up for M365 dev account]() |
| Solitary Learner | [Microsoft Learn Module](https://docs.microsoft.com/en-au/learn/modules/secure-access-azure-identity-services/3-what-is-azure-active-directory) |


>Day 6 of 💯. Who are you, where are the others?

<sup>94 (minus weekends) to go 💪</sup>

![Azure has regions](https://media.giphy.com/media/l36kU80xPf0ojG0Erg/giphy.gif)
---
title: Use Software Restriction Policies and AppLocker policies (Windows)
description: This topic for the IT professional describes how to use Software Restriction Policies (SRP) and AppLocker policies in the same Windows deployment.
ms.assetid: c3366be7-e632-4add-bd10-9df088f74c6d
ms.reviewer: 
ms.author: macapara
ms.prod: m365-security
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: mjcaparas
manager: dansimp
audience: ITPro
ms.collection: M365-security-compliance
ms.topic: conceptual
ms.date: 09/21/2017
ms.technology: windows-sec
---

# Use Software Restriction Policies and AppLocker policies

**Applies to**

- Windows 10
- Windows 11
- Windows Server 2016 and above

>[!NOTE]
>Some capabilities of Windows Defender Application Control are only available on specific Windows versions. Learn more about the [Windows Defender Application Control feature availability](/windows/security/threat-protection/windows-defender-application-control/feature-availability).

This topic for the IT professional describes how to use Software Restriction Policies (SRP) and AppLocker policies in the same Windows deployment.

## Understand the difference between SRP and AppLocker

You might want to deploy application control policies in Windows operating systems earlier than Windows Server 2008 R2 or Windows 7. You can use AppLocker policies only on the supported versions and editions of Windows as listed in [Requirements to use AppLocker](requirements-to-use-applocker.md). However, you can use SRP on those supported editions of Windows plus Windows Server 2003 and Windows XP. To compare features and functions in SRP and AppLocker so that you can determine when to use each technology to meet your application control objectives, see [Determine your application control objectives](determine-your-application-control-objectives.md).

## Use SRP and AppLocker in the same domain

SRP and AppLocker use Group Policy for domain management. However, when policies are generated by SRP and AppLocker exist in the same domain, and they are applied through Group Policy, AppLocker policies take precedence over policies generated by SRP on computers that are running an operating system that supports AppLocker. For info about how inheritance in Group Policy applies to AppLocker policies and policies generated by SRP, see [Understand AppLocker rules and enforcement setting inheritance in Group Policy](understand-applocker-rules-and-enforcement-setting-inheritance-in-group-policy.md).

>**Important:**  As a best practice, use separate Group Policy Objects to implement your SRP and AppLocker policies. To reduce troubleshooting issues, do not combine them in the same GPO.
 
The following scenario provides an example of how each type of policy would affect a bank teller software app, where the app is deployed on different Windows desktop operating systems and managed by the Tellers GPO.

| Operating system | Tellers GPO with AppLocker policy | Tellers GPO with SRP | Tellers GPO with AppLocker policy and SRP |
| - | - | - | - |
| Windows 10, Windows 8.1, Windows 8,and Windows 7 | AppLocker policies in the GPO are applied, and they supersede any local AppLocker policies.| Local AppLocker policies supersede policies generated by SRP that are applied through the GPO. | AppLocker policies in the GPO are applied, and they supersede the policies generated by SRP in the GPO and local AppLocker policies or policies generated by SRP.| 
| Windows Vista| AppLocker policies are not applied.| Policies generated by SRP in the GPO are applied, and they supersede local policies generated by SRP.AppLocker policies are not applied.| Policies generated by SRP in the GPO are applied, and they supersede local policies generated by SRP. AppLocker policies not applied.| 
| Windows XP| AppLocker policies are not applied.| Policies generated by SRP in the GPO are applied, and they supersede local policies generated by SRP. AppLocker policies are not applied.| Policies generated by SRP in the GPO are applied, and they supersede local policies generated by SRP. AppLocker policies not applied.| 
 
>**Note:**  For info about supported versions and editions of the Windows operating system, see [Requirements to use AppLocker](requirements-to-use-applocker.md).
 
## Test and validate SRPs and AppLocker policies that are deployed in the same environment

Because SRPs and AppLocker policies function differently, they should not be implemented in the same GPO. This makes testing the result of the policy straightforward, which is critical to successfully controlling application usage in the organization. Configuring a testing and policy distribution system can help you understand the result of a policy. The effects of policies generated by SRP and AppLocker policies need to be tested separately and by using different tools.

### Step 1: Test the effect of SRPs

You can use the Group Policy Management Console (GPMC) or the Resultant Set of Policy (RSoP) snap-in to determine the effect of applying SRPs by using GPOs.

### Step 2: Test the effect of AppLocker policies

You can test AppLocker policies by using Windows PowerShell cmdlets. For info about investigating the result of a policy, see:

-   [Test an AppLocker policy by using Test-AppLockerPolicy](test-an-applocker-policy-by-using-test-applockerpolicy.md)
-   [Monitor app usage with AppLocker](monitor-application-usage-with-applocker.md)

Another method to use when determining the result of a policy is to set the enforcement mode to **Audit only**. When the policy is deployed, events will be written to the AppLocker logs as if the policy was enforced. For info about using the **Audit only** mode, see:

- [Understand AppLocker enforcement settings](understand-applocker-enforcement-settings.md)
- [Configure an AppLocker policy for audit only](configure-an-applocker-policy-for-audit-only.md)

## See also

- [AppLocker deployment guide](applocker-policies-deployment-guide.md)

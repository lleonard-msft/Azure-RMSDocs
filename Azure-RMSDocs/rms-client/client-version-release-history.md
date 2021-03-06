---
# required metadata

title: Azure Information Protection client&colon; Version release history and support policy
description: See what's new or changed in a release of the Azure Information Protection client for Windows, and understand the lifecycle policy for support. 
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/22/2017
ms.topic: article
ms.prod:
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid:  6ebd0ca3-1864-4b3d-bb3e-a168eee5eb1d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Information Protection client: Version release history and support policy

>*Applies to: Azure Information Protection*

The Azure Information Protection team regularly updates the Azure Information Protection client for fixes and new functionality. 

You can download the latest GA release version and the current preview version from the [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=53018). These versions are also included in the Microsoft Update Catalog (category: **Azure Information Protection**), so that you can deploy the client by using WSUS or Configuration Manager, or other software deployment mechanisms that use Microsoft Update.

### Servicing information and timelines

Each general availability (GA) version of the Azure Information Protection client is supported for up to six months after the release of the subsequent GA version. Unsupported versions of the client are not included on this page. Fixes and new functionality are always applied to the latest GA version and will not be applied to older GA versions.

Preview versions should not be deployed for end users on production networks. Instead, use the latest preview version to see and try new functionality or fixes that are coming in the next GA version. Preview versions that are not current are not supported.

### Release history

Use the following information to see what’s new or changed for a supported release of the Azure Information Protection client for Windows. The most current release is listed first. 

> [!NOTE]
> Minor fixes are not listed so if you experience a problem with the Azure Information Protection client, we recommend that you check whether it is fixed with the latest GA release. If the problem remains, check the current preview version.
>  
> For technical support, see the [Support options and community resources](../get-started/information-support.md#support-options-and-community-resources) information. We also invite you to engage with the Azure Information Protection team, on their [Yammer site](https://www.yammer.com/askipteam/).

## Versions later than 1.10.56.0

If you have a version of the client that is later than 1.10.56.0, it is a preview build for testing and evaluation purposes. 

For what's new or changed in the current preview version since the last GA version of the client, see the **Details** section on the [download page](https://www.microsoft.com/en-us/download/details.aspx?id=53018). 

## Version 1.10.56.0

**Released**: 09/18/2017

This version includes the MSIPC version 1.0.3219.0619 of the RMS client.

**New features**:

- Support for the new Office 365 DLP conditions that you can configure for a label. For more information, see [Configure conditions for an Azure Information Protection label](../deploy-use/configure-policy-classification.md).

- Support for labels that are configured for user-defined actions. For Outlook, this label automatically applies the Outlook Do Not Forward option. For Word, Excel, PowerPoint, and File Explorer, this label prompts the user to specify custom permissions. For more information, see [Configure an Azure Information Protection label for protection](../deploy-use/configure-policy-protection.md).

- Labels support multiple languages. Beginning with August 30, 2017, the [default policy](../deploy-use/configure-policy-default.md) includes support for multiple languages that this version of the client displays to users. For users to see labels in their preferred language from a default policy before this date, and for labels that you configure, see [How to configure labels for different languages in Azure Information Protection](../deploy-use/configure-policy-languages.md).

- Labels are displayed from the **Protect** button on the Office ribbon, in addition to displaying on the Information Protection bar. 

- Native protection for the following Visio file types: .vsdm, .vsdx, .vssm, .vssx, .vstm, .vstx

- Support for advanced client configurations that you configure in the Azure portal. These configurations include the following:
    
    - [Hide or show the Do Not Forward button in Outlook](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)
    
    - [Make the custom permissions options available or unavailable to users](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)
    
    - [Permanently hide the Azure Information Protection bar](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)
    
    - [Enable recommended classification in Outlook](../rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)

- For PowerShell, support to label files non-interactively by using the new PowerShell cmdlets, [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) and [Clear-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication). For more information how to use these cmdlets, see the [PowerShell section](../rms-client/client-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection) of the admin guide.

- For the PowerShell cmdlets, [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) and [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification), there are new parameters: **Owner** and **PreserveFileDetails**. These parameters let you specify an email address for the Owner custom property, and leave the date unchanged for documents that you label.

**Fixes**:

Fixes for stability and for specific scenarios that include:

- Support for generically protecting large files that previously could cause corruption if larger than 1 GB. Now, the file size is limited only by available hard disk space and available memory. For more information about file size limitations, see [File sizes supported for protection](client-admin-guide-file-types.md#file-sizes-supported-for-protection) from the admin guide.

- The Azure Information Protection client viewer opens protected PDF (.ppdf) files as view-only.

- Support for labeling and protection of files stored on SharePoint Server.

- Watermarks now support multiple lines. In addition, visual markings are now applied to a document on the [first save only](../deploy-use/configure-policy-markings.md#when-visual-markings-are-applied) rather than every time a document is saved.

- The **Run Diagnostics** option in the **Help and Feedback** dialog box is replaced with **Reset Settings**. The behavior for this action has changed to include signing out the user and deleting the Azure Information Protection policy. For more information, see [More information about the Reset Settings option](..\rms-client\client-admin-guide.md#more-information-about-the-reset-settings-option) from the admin guide.

- Support for proxy authentication.

Fixes for a better user experience, that include:

- Email validation when users specify custom permissions. Also, multiple email addresses can now be specified by pressing Enter.

- The parent label is not displayed when all its sublabels are configured for protection and the client does not have an edition of Office that supports protection. 

## Version 1.7.210.0

**Released**: 06/06/2017

This version includes the MSIPC version 1.0.2217.1 of the RMS client.

**New features**:

- New PowerShell cmdlet, [Set-AIPFileClassification](/powershell/module/azureinformationprotection/Set-AIPFileClassification). When you run this cmdlet, it inspects the file contents and automatically applies labels to unlabeled files, according to the conditions that you specify in the Azure Information Protection policy.

**Fixes**:

- All labeling and classification cmdlets are now supported on computers that are not connected to the Internet but have a valid Azure Information Protection policy.

- For consistency, an output parameter from the [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) cmdlet is changed from British English (**IsLabelled**) to American English (**IsLabeled**). If you have scripts or automated processes that look for this parameter, update the spelling for this parameter.

- General fixes for stability that include:

    - For Outlook: Fixes for crashes, high memory consumption, and display issues for menus.
    
    - For Word, Excel, and PowerPoint: Fixes for high CPU usage, display issues when saving large Excel files, or the application stops responding. 
    
    Also for these applications, to improve performance for Office 2016 with SharePoint Online and OneDrive for Business, automatic and recommended labeling is applied when the file closes rather than when the file saves (automatically saves or the user chooses to save). Similarly, if the setting **All documents and email must have a label** is enabled, users are not prompted to select a label until the file closes. The exception is for Word 2016 and Excel 2016 and the user selects the **Save As** option. Then, this action triggers these labeling behaviors if they are configured. 

## Next steps

For more information about installing and using the client: 

- For users: [Download and install the client](install-client-app.md)

- For admins: [Azure Information Protection client administrator guide](client-admin-guide.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

---
# required metadata

title: Configuring servers for the Azure Rights Management connector | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configuring servers for the Azure Rights Management connector

Use the following information to help you configure your on-premises servers that will use the Azure Rights Management (RMS) connector. These procedures cover step 5 from [Deploying the Azure Rights Management connector](deploying-the-azure-rights-management-connector.md).

Before you begin, make sure that you have installed and configured the RMS connector and you have checked any [prerequisites](deploying-the-azure-rights-management-connector.md#prerequisites-for-the-rms-connector) that are applicable for the servers that will use the connector.


## Configuring servers to use the RMS connector
After you have installed and configured the RMS connector, you are ready to configure your on-premises servers that will use Rights Management and connect to Azure RMS by using the connector. This means configuring the following servers:

-   **For Exchange 2016 and Exchange 2013**: Client access servers and mailbox servers

-   **For Exchange 2010**: Client access servers and hub transport servers

-   **For SharePoint**: Front-end SharePoint webservers, including those hosting the Central Administration server

-   **For File Classification Infrastructure**: Windows Server computers that have installed File Resource Manager

This configuration requires registry settings. To do this, you have two options: Automatically by using the server configuration tool for Microsoft RMS connector, or manually by editing the registry.

---

**Automatically by using the server configuration tool for Microsoft RMS connector:**

- Advantages:

	- No direct editing of the registry. This is automated for you by using a script.

	- No need to run a Windows PowerShell cmdlet to obtain your Microsoft RMS URL.

	- The prerequisites are automatically checked for you (but not automatically remediated) if you run it locally.

Disadvantages:

- When you run the tool, you must make a connection to a server that is already running the RMS connector.

---

**Manually by editing the registry:**

- Advantages:

	- No connectivity to a server running the RMS connector is required.

- Disadvantages:

	- More administrative overheads that are error-prone.

	- You must obtain your Microsoft RMS URL, which requires you to run a Windows PowerShell command.

	- You must always make all the prerequisites checks yourself.


---

> [!IMPORTANT]
> In both cases, you must manually install any prerequisites and configure Exchange, SharePoint, and File Classification Infrastructure to use Rights Management.

For most organizations, automatic configuration by using the server configuration tool for Microsoft RMS connector will be the better option, because it provides greater efficiency and reliability than manual configuration.

After making the configuration changes on these servers, you must restart them if they are running Exchange or SharePoint and previously configured to use AD RMS. There is no need to restart these servers if you are configuring them for Rights Management for the first time. You must always restart the file server that is configured to use File Classification Infrastructure after you make these configuration changes.

### How to use the server configuration tool for Microsoft RMS connector

1.  If you haven’t already downloaded the script for the server configuration tool for Microsoft RMS connector (GenConnectorConfig.ps1), download it from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=314106).

2.  Save the GenConnectorConfig.ps1 file on the computer where you will run the tool. If you will run the tool locally, this must be the server that you want to configure to communicate with the RMS connector. Otherwise, you can save it on any computer.

3.  Decide how to run the tool:

    -   **Locally**: You can run the tool interactively, from the server to be configured to communicate with the RMS connector. This is useful for a one-off configuration, such as a testing environment.

    -   **Software deployment**: You can run the tool to produce registry files that you then deploy to one or more relevant servers by using a systems management application that supports software deployment, such as System Center Configuration Manager.

    -   **Group Policy**: You can run the tool to produce a script that you give to an administrator who can create Group Policy objects for the servers to be configured. This script creates one Group Policy object for each server type to be configured, which the administrator can then assign to the relevant servers.

    > [!NOTE]
    > This tool configures the servers that will communicate with the RMS connector and that are listed at the beginning of this section. Do not run this tool on the servers that run the RMS connector.

4.  Start Windows PowerShell with the **Run as an administrator** option, and use the Get-help command to read instructions how to the use the tool for your chosen configuration method:

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

To run the script, you must enter the URL of the RMS connector for your organization. Enter the protocol prefix (HTTP:// or HTTPS://) and the name of the connector that you defined in DNS for the load balanced address of your connector. For example, https://connector.contoso.com. The tool then uses that URL to contact the servers running the RMS connector and obtain other parameters that are used to create the required configurations.

> [!IMPORTANT]
> When you run this tool, make sure that you specify the name of the load-balanced RMS connector for your organization and not the name of a single server that runs the RMS connector service.

Use the following sections for specific information for each service type:

-   [Configuring an Exchange server to use the connector](#configuring-an-exchange-server-to-use-the-connector)

-   [Configuring a SharePoint server to use the connector](#configuring-a-sharepoint-server-to-use-the-connector)

-   [Configuring a file server for File Classification Infrastructure to use the connector](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> After these servers are configured to use the connector, client applications that are installed locally on these servers might not work with RMS. When this happens, it is because the applications try to use the connector rather than use RMS directly, which is not supported.
>
> In addition, if Office 2010 is installed locally on an Exchange server, the client app’s IRM features might work from that computer after the server is configured to use the connector, but this is not supported.
>
> In both scenarios, you must install the client applications on separate computers that are not configured to use the connector. They will then correctly use RMS directly.

## Configuring an Exchange server to use the connector
The following Exchange roles communicate with the RMS connector:

-   For Exchange 2016 and Exchange 2013: Client access server and mailbox server

-   For Exchange 2010: Client access server and hub transport server

To use the RMS connector, these servers running Exchange must be running one of the following software versions:

-   Exchange Server 2016

-   Exchange Server 2013 with Exchange 2013 Cumulative Update 3

-   Exchange Server 2010 with Exchange 2010 Service Pack 3 Rollup Update 6

You will also need to install on these servers, a version of the RMS client that includes support for RMS Cryptographic Mode 2. The minimum version that is supported in Windows Server 2008 is included in the hotfix that you can download from [RSA key length is increased to 2048 bits for AD RMS in Windows Server 2008 R2 and in Windows Server 2008](http://support.microsoft.com/kb/2627272). The minimum version for Windows Server 2008 R2 can be downloaded from [RSA key length is increased to 2048 bits for AD RMS in Windows 7 or in Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Windows Server 2012 and Windows Server 2012 R2 natively support Cryptographic Mode 2.

> [!IMPORTANT]
> If these versions or later versions of Exchange and the RMS client are not installed, you will not be able to configure Exchange to use the connector. Check that these versions are installed before you continue.

### To configure Exchange servers to use the connector

1. Make sure that the Exchange servers are authorized to use the RMS connector, by using the RMS connector administration tool and the information from the [Authorizing servers to use the RMS connector](install-and-configure-the-rms-connector.md#authorizing-servers-to-use-the-rms-connector) section. This configuration is required so that Exchange can use the RMS connector.

2.  On the Exchange server roles that communicate with the RMS connector, do one of the following:

    -   Run the server configuration tool for Microsoft RMS connector. For more information, see [How to use the server configuration tool for Microsoft RMS connector](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) in this article.

        For example, to run the tool locally to configure a server running Exchange 2016 or Exchange 2013:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
        ```

    -   Make manual registry edits by using the information in [Registry settings for the RMS connector](registry-settings-rms-connector.md) to manually add registry settings on the servers. 

3.  Enable IRM functionality in Exchange. For more information, see [Information Rights Management Procedures](https://technet.microsoft.com/library/dd351212%28v=exchg.150%29.aspx) in the Exchange library.

## Configuring a SharePoint server to use the connector
The following SharePoint roles communicate with the RMS connector:

-   Front-end SharePoint webservers, including those hosting the Central Administration server

To use the RMS connector, these servers running SharePoint must be running one of the following software versions:

-   SharePoint Server 2013

-   SharePoint Server 2010

A SharePoint 2013 server must also be running a version of the MSIPC client 2.1 that is supported with the RMS connector. To make sure that you have a supported version, download the latest client from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=38396).

> [!WARNING]
> There are multiple versions of the MSIPC 2.1 client, so make sure that you have version 1.0.2004.0 or later.
>
> You can verify the client version by checking the version number of MSIPC.dll, which is located in **\Program Files\Active Directory Rights Management Services Client 2.1**. The properties dialog box  shows the version number of the MSIPC 2.1 client.

These servers running SharePoint 2010 must have installed a version of the MSDRM client that includes support for RMS Cryptographic Mode 2. The minimum version that is supported in Windows Server 2008 is included in the hotfix that you can download from [RSA key length is increased to 2048 bits for AD RMS in Windows Server 2008 R2 and in Windows Server 2008](http://support.microsoft.com/kb/2627272), and the minimum version for Windows Server 2008 R2 can be downloaded from [RSA key length is increased to 2048 bits for AD RMS in Windows 7 or in Windows Server 2008 R2](http://support.microsoft.com/kb/2627273). Windows Server 2012 and Windows Server 2012 R2 natively support Cryptographic Mode 2.

### To configure SharePoint servers to use the connector

1. Make sure that the SharePoint servers are authorized to use the RMS connector, by using the RMS connector administration tool and the information from the [Authorizing servers to use the RMS connector](install-and-configure-the-rms-connector.md#authorizing-servers-to-use-the-rms-connector) section. This configuration is required so that Exchange can use the RMS connector.

2.  On the SharePoint servers that communicate with the RMS connector, do one of the following:

    -   Run the server configuration tool for Microsoft RMS connector. For more information, see [How to use the server configuration tool for Microsoft RMS connector](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) in this article.

        For example, to run the tool locally to configure a server running SharePoint 2013:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   If you are using SharePoint 2013, make manual registry edits by using the information in [Registry settings for the RMS connector](registry-settings-rms-connector.md) to manually add registry settings on the servers. 

3.  Enable IRM in SharePoint. For more information, see [Configure Information Rights Management (SharePoint Server 2010)](https://technet.microsoft.com/library/hh545607%28v=office.14%29.aspx) in the SharePoint library.

    When you follow these instructions, you must configure SharePoint to use the connector by specifying **Use this RMS server**, and then enter the load-balancing connector URL that you configured. Enter the protocol prefix (HTTP:// or HTTPS://) and the name of the connector that you defined in DNS for the load balanced address of your connector. For example, if your connector name is  https://connector.contoso.com, your configuration will look like the following picture:

    ![](../media/AzRMS_SharePointConnector.png)

    After IRM is enabled on a SharePoint farm, you can enable IRM on individual libraries by using the **Information Rights Management** option on the **Library Settings** page for each of the libraries.


## Configuring a file server for File Classification Infrastructure to use the connector
To use the RMS connector and File Classification Infrastructure to protect Office documents, the file server must be running one of the following operating systems:

-   Windows Server 2012 R2

-   Windows Server 2012

### To configure file servers to use the connector

1.  Make sure that the file servers are authorized to use the RMS connector, by using the RMS connector administration tool and the information from the [Authorizing servers to use the RMS connector](install-and-configure-the-rms-connector.md#authorizing-servers-to-use-the-rms-connector) section. This configuration is required so that Exchange can use the RMS connector.

2.  On the file servers configured for File Classification Infrastructure and that will communicate with the RMS connector, do one of the following:

    -   Run the server configuration tool for Microsoft RMS connector. For more information, see [How to use the server configuration tool for Microsoft RMS connector](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector) in this article.

        For example, to run the tool locally to configure a file server running FCI:

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - Make manual registry edits by using the information in [Registry settings for the RMS connector](registry-settings-rms-connector.md) to manually add registry settings on the servers. 

3.  Create classification rules and file management tasks to protect documents with RMS Encryption, and then specify an RMS template to automatically apply RMS policies. For more information, see [File Server Resource Manager Overview](http://technet.microsoft.com/library/hh831701.aspx) in the Windows Server documentation library.

## Next steps
Now that the RMS connector is installed and configured, and your servers are configured to use it, IT administrators and users can protect and consume email message and documents by using Azure RMS. To make this easy for users, deploy the RMS sharing application, which installs an add-on for Office and adds new right-click options to File Explorer. For more information, see the [Rights Management sharing application administrator guide](../rms-client/rights-management-sharing-application-administrator-guide.md).

In addition, you might consider the following to help you monitor the RMS connector and your organization’s usage of Azure RMS:

-   The built-in **Microsoft Rights Management connector** performance counters.

-   The [RMS Analyzer tool](https://www.microsoft.com/en-us/download/details.aspx?id=46437), using the RMS connector option to help you monitor the health of the connector and identify any configuration issues.

-   [Logging and analyzing Azure Rights Management usage](logging-and-analyzing-azure-rights-management-usage.md)

You can use the [Azure Rights Management deployment roadmap](azure-rights-management-deployment-roadmap.md) to check whether there are other configuration steps that you might want to do before you roll out [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] to users and administrators. 
---
title: "Manage Online Backup in Windows Server Essentials"
description: Learn how to use the Online Backup management page in the Windows Server Essentials Dashboard to perform common administrative tasks.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 95a9f593-fad7-4335-bd4d-c7bb8c033efb
author: nnamuhcs
ms.author: wscontent
manager: mtillman
---

# Manage Online Backup in Windows Server Essentials

>Applies To: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 After you integrate with  Microsoft Azure Backup, the **Online Backup** management page appears in the Windows Server Essentials Dashboard. The **Online Backup** page makes it possible to perform common administrative tasks. The features on the Online Backup page include:

- The following sub-section pages:

  -   **Online Backup** After you register the server for online backup, this section displays the current backup status, storage status, and account information.

  -   **Protected Folders** This section lists all shared folders and all File History folders on the server, and any other folders that you have chosen to back up in  Azure. The list includes the folder name, folder path, and status for each shared folder.

  -   **Backup History** This section displays a list of recent online backups. The list includes the type of operation, and the time and status for each backup.

- A details pane with additional information about a selected backup job or restore job.

- A tasks pane that includes a set of administrative tasks that you can perform.

  As a best practice, you should back up the most important business and user data. For example, you should back up server folders that contain critical data files. You should also back up the File History for network computers that contain critical information.

  When deciding which data to back up online, consider the backup frequency and retention policy that you want to implement. Then review your budget and determine the amount of storage space you can afford. Balance the cost and volume of storage against your needs, and then configure online backup to protect as much of your important data as possible. For pricing information, see [pricing details for Azure Backup](https://azure.microsoft.com/pricing/details/backup/).

  The following sections describe various online backup tasks that can appear in the Windows Server Essentials Dashboard.

## Online backup tasks in the Dashboard

-   [Upload a certificate to the Azure Backup vault](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)

-   [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)

-   [Start an online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_3)

-   [Restore files and folders from an online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_4)

-   [Register this server for backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)

-   [Unregister server](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6)

###  <a name="BKMK_1"></a> Upload a certificate to the Azure Backup vault
 Before you can use  Azure Backup for online backups in Windows Server Essentials, you must upload a public certificate to register with the backup vault. The certificate is used to authenticate the  Azure Backup deployment (the agent), acting on behalf of the Microsoft Online Services subscription owner to manage resources associated with the subscription.

> [!NOTE]
>  Before you upload the certificate, you must complete the procedures in [Sign up for Azure Backup Service](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16).

##### To upload a certificate to use with the Azure Backup Service

1. Log on to the Windows Server Essentials Dashboard with an administrator account.

2. On the Dashboard **Home** page, click **ONLINE BACKUP**.

3. In the **ONLINE BACKUP** area, click **Upload certificate to Azure Backup vault**.

    That opens **Recovery Services** in the  Azure Management Portal. If you aren't already signed in to  Azure, you'll need to sign in using your Microsoft account.

4. Click the name of the backup vault you'll use for online backups to open the **Quick Start** page for the backup vault.

5. Click **Manage Certificate**.

6. In the **Manage Certificate** dialog box, paste the path of the public certificate generated by Windows Server Essentials. To obtain the path of the public certificate, do the following:

   1.  On the Windows Server Essentials Dashboard, click the **Online Backup** tab.

   2.  On the **Online Backup** page, copy the path of the generated certificate.

   3.  Switch to the  Azure Management Portal, and then in the **Manage Certificate** dialog box, paste the path to upload the generated public certificate.

   > [!NOTE]
   >  You can also use your own public certificate. To know what certificate is required, on the **Quick Start** page, click the **Acquire Certificate** link.

   > [!NOTE]
   >   Azure requires an x.509 v2 certificate with a public key. For more information, see [Manage vault certificates](/previous-versions/azure/dn169036(v=azure.100)).

7. After you select the certificate, click **OK** (check mark).

8. You are returned to the **Quick Start** page. Click **Dashboard**, and verify that the certificate was uploaded successfully. After the certificate is uploaded successfully, the dashboard displays the certificate thumbprint and expiration date.

   After completing this procedure, do the following:

9. Register the server with the  Azure Backup Service. For more information, see [Register this server for backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).

10. Configure online backup of the server. For more information, see [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).

###  <a name="BKMK_2"></a> Configure online backup
 After you register the server with  Azure Backup, you can configure the online backup settings in Windows Server Essentials.

##### To configure online backup

1.  Either from the Register Your Server Wizard or from the **Online Backup** page of the Windows Server Essentials Dashboard, click **Configure online backup**. The Configure Online Backup Wizard appears.

2.  On the **Configure Online Backup** page of the wizard, select the check box for each server folder that you want to back up to  Azure Backup. Clear the check box for each server folder that you do not want to include in the backup. To add folders that are not shown in the list, click **Add Folders**. When you finish your selection, click **Next**.

    > [!NOTE]
    >  You cannot select a folder that is not located on the local server, or a folder that is on a drive that is formatted as ReFS.

3.  On the **Add File History Backups** page of the wizard, you can select to include File History Backups for network computers that support the File History feature. Then click **Next** to continue.

4.  On the **Specify the Backup Schedule** page of the wizard, configure the following and then click **Next** to continue:

    -   Select or accept the time of day when you want the online backup to run. The default time is 10:00 PM. You may also specify a time to run a second backup.

    -   Select or accept the days when you want the online backup to run. By default, online backup runs on Monday through Friday.

5.  On the **Specify the Backup Retention Policy** page of the wizard, select the number of days that you want to keep online backups, and then click **Next**. The default is 7 days. You can also choose to keep online backups for 15 or 30 days.

    > [!NOTE]
    >   Azure Backup always retains your most recent backup. If the backup destination does not have sufficient space available to store the backup, the backup process will not succeed. To avoid this situation, either purchase additional storage space, or shorten the data retention period. For pricing information, see [Pricing Details](https://azure.microsoft.com/pricing/details/backup/) for  Microsoft Azure Backup.

6.  On the **Choose your bandwidth usage** page of the wizard, if you want to restrict the amount of Internet bandwidth that is allocated to online backup, select **Enable Internet bandwidth usage**. Use the options on the page to specify how much Internet bandwidth to allow your online backup to use during work hours and during non-work hours. Then define your business hours and business days.

    > [!NOTE]
    >   Azure Backup allows you to customize how the integration software utilizes the network bandwidth when backing up or restoring information. Using a technique commonly known as throttling, you can control the amount of network bandwidth that is available for use by the backup and restore processes during specific day and time intervals. After selecting the **Enable Internet bandwidth usage** check box in the Configure Online Backup wizard, you can specify the workdays and work hours during which to apply the work-hours bandwidth limit. The non-work-hours limit is used at all other times. Valid bandwidth ranges are from 256 Kbps to Unlimited for both limits.

7.  When the online backup configuration completes, click **Close**.

    > [!TIP]
    >  After a successful backup configuration, the **Online Backup** page shows the status of the most recent online backup and the amount of storage space used by the backup vault. To see the status of previous backups, click **Backup History**.

###  <a name="BKMK_3"></a> Start an online backup

> [!NOTE]
>  Before you can start an online backup, you must first [Register this server for backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5), and then [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).

##### To start an online backup immediately

1.  Log on to the Dashboard as an administrator.

2.  On the navigation bar, click **ONLINE BACKUP**.

3.  In the **Online Backup Tasks** pane, click **Start backup now**.

###  <a name="BKMK_4"></a> Restore files and folders from an online backup
 The Restore Files and Folders Wizard guides you through the process of locating, selecting, and restoring files and folders that are backed up online. As you advance through the wizard, you will perform the following tasks:

1.  **Choose an online backup from which to restore files and folders**

     When you run the Restore Files and Folders Wizard, the first thing that you must do is specify if you want to restore files from an online backup of the server that you are currently logged on to, or from a backup of a different server.

2.  **Choose a server from which to restore files and folders**

     If you chose to restore files and folders from a different server, select the server you want to restore from in the list of available servers, and then click **Next**.

3.  **Choose a volume that contains the files and folders to be restored**

     Online backups contain volumes that correspond to the volumes on the backup source server. After you select the volume, select the date and time of the backup from which to restore, and then click **Next**.

4.  **Select files and folders to restore**

     On the **Select Items To Restore** page of the wizard, you can open the various folder locations and select the check box for each file or folder that you want to restore. When you are finished selecting files, click **Next**.

5.  **Specify the destination location for restored files and folders**

     The **Specify Restore Options** page of the wizard allows you to specify where to restore files and folders. There are two options:

    -   **Restore to the original location**. Select this option to restore files and folders to the exact location from which the backup originated.

    -   **Restore to a different location**.  Choose this option to specify a different location on the server in which to restore the files.

         In the default installation, if a file with the same name as a restore file already exists at the destination location, the wizard creates a copy of the original file. Additionally, the Access Control List (ACL) is updated to reflect current file permissions. You can click **Advanced** to customize the default settings.

6.  **Confirm the restoration information**

     The **Confirm Your Restoration Information** page provides a summary of the restore instructions that you have specified. To proceed with file restore, you must type the correct passphrase for your online backup account.

###  <a name="BKMK_5"></a> Register this server for backup
 To back up or restore files, folders, and file history on your Windows Server Essentials server to  Azure Backup, you must first register your server with the  Microsoft Azure Backup Service.

> [!NOTE]
>  Before you register your server, you must upload a certificate to use with the backup vault that will store the online backups. For more information, see [Upload a certificate to the Azure Backup vault](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).

##### To register your server with Azure Backup

1.  Log on to the server as an administrator, and open the Dashboard.

2.  On the navigation bar, click **ONLINE BACKUP**.

3.  In the **Online Backup** subsection, click **Register**.

4.  Choose the certificate that you want to use with the backup vault for your online backups. The default certificate is selected by default; if you want to choose a different certificate, use **Browse**. Then click **Next**.

5.  Follow the instructions in the wizard to create a passphrase and then complete the registration.

###  <a name="BKMK_6"></a> Unregister server

> [!CAUTION]
>  If you unregister your Windows Server Essentials server from the  Microsoft Azure Backup Service,  Azure Backup can no longer back up the server. Additionally, server data that was previously uploaded will be erased. To resume online backups, you must register the server again.

##### To unregister your server with Azure Backup

1.  Sign in to the [Azure Management Portal](https://portal.azure.com).

2.  Click **Recovery Services**.

3.  In **Recovery Services**, click the name of the backup vault.

4.  From the **Quick Start** page for the vault, click **Servers**.

5.  Select the server, click **Delete**, and then click **Yes** at the confirmation prompt.

## Related tasks

-   [Change the online backup policy](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_7)

-   [View online backup storage usage](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_8)

-   [Include a new folder in online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_9)

-   [Remove or exclude file history backups from the online backup policy](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_10)

-   [Disable or re-enable online server backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_11)

-   [Stop an online server backup in progress](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_12)

-   [View online backup status](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_13)

-   [View and manage online backup alerts](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_14)

-   [Reset online backup to default settings](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_15)

-   [Sign up for Azure Backup Service](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16)

-   [Integrate Azure Backup with Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_17)

-   [Protect folders for online backup in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_18)

-   [Online backup history in Windows Server Essentials](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_19)

###  <a name="BKMK_7"></a> Change the online backup policy
 It is easy to make changes to the online backup policy by using the Windows Server Essentials Dashboard.

##### To change the online backup policy

1. Log on to the Dashboard as an administrator.

2. On the navigation bar, click **Online Backup**.

3. In the **Online Backup Tasks** pane, click **Configure online backup**.

4. Follow the instructions in the wizard to customize the online backup policy.

   For more detailed information about the settings that you can customize, see [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).

###  <a name="BKMK_8"></a> View online backup storage usage

##### To view the amount of storage space that Online Backup uses

1.  Log on to the Dashboard as an administrator.

2.  On the navigation bar, click **ONLINE BACKUP**.

3.  On the **Online Backup** tab, the **Storage Status** appears in the information pane.

###  <a name="BKMK_9"></a> Include a new folder in online backup

##### To include a new folder in the online backup policy

1. Log on to the Dashboard as an administrator.

2. On the navigation bar, click **Online Backup**.

3. In the **Online Backup Tasks** pane, click **Configure online backup**.

4. On the **Change or Remove the Backup Policy** page, click **Customize the Online Backup Policy**.

5. On the **Configure Online Backup** page, if the folder you want to include does not appear in the list, click **Add folders**.

6. In the **Add folders** window, browse to and select the folder you want to include in online backup, and then click **OK**.

7. On the **Configure Online Backup** page, select other folders to include as desired, and then click **Next**.

8. Follow the instructions in the wizard to finish customizing the online backup policy.

   For more detailed information about other settings that you can customize, see [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).

###  <a name="BKMK_10"></a> Remove or exclude file history backups from the online backup policy

##### To remove or exclude a folder from the online backup policy

1.  Log on to the Dashboard as an administrator.

2.  On the navigation bar, click **Online Backup**.

3.  Click the **Protected Folders** tab. The details pane, displays a list of folders with their online backup status.

4.  Select the folder that you want to exclude from the online backup policy, and then in the task pane, click **Remove the folder from online backup**.

###  <a name="BKMK_11"></a> Disable or re-enable online server backup
 For instructions about how to use  Azure Backup to back up or restore server data, see [Register this server for backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).

 For instructions about how to stop using  Azure Backup to back up or restore server data, see [Unregister server](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_6).

###  <a name="BKMK_12"></a> Stop an online server backup in progress

##### To stop an online server backup in progress

1.  Log on to the Dashboard as an administrator.

2.  On the navigation bar, click **ONLINE BACKUP**.

3.  In the **Online Backup Tasks** pane, click **Stop the backup**.

     After you stop the backup, a status of **Canceled** appears for the backup in the **Backup History** list.

###  <a name="BKMK_13"></a> View online backup status

##### To view the backup status

1.  Log on to the Dashboard as an administrator.

2.  On the navigation bar, click **ONLINE BACKUP**.

3.  Click the **Backup History** tab. The list view displays the status for each backup job. Select a backup job to view additional details about that job.

###  <a name="BKMK_14"></a> View and manage online backup alerts
 Like many other alerts, alerts for  Azure Backup are displayed in the Alert Viewer.

##### To view online backup alerts in the Alert Viewer

1. Open the Dashboard.

2. Do one of the following:

     Windows Server Essentials: On the navigation pane, click the alerts icon \(may be Critical, Warning, or Informational\). This opens the Alert Viewer.

     Windows Server Essentials: On the **Home** page, click the **Health Monitoring** tab.

3. Review the list of alerts for issues that are related to  Azure Backup.

   For more information about using the Alert Viewer or Health Monitoring tab to manage alerts, see [Manage System Health](Manage-System-Health-in-Windows-Server-Essentials.md).

###  <a name="BKMK_15"></a> Reset online backup to default settings
 Windows Server Essentials provides a wizard that helps you configure the settings for online backup. If you want to restore the default settings, run the **Configure online backup** task, and choose the **Remove the online backup policy** option. Then, run the **Configure online backup** task again. Your previously uploaded data remains unchanged.

###  <a name="BKMK_16"></a> Sign up for Azure Backup Service
 To prepare to integrate  Microsoft Azure Backup with Windows Server Essentials, you'll log on to the  Azure Management Portal with your Microsoft Online Services account, and then create a backup vault to store your online backups in  Azure. You'll then download the  Azure Backup Integration module, and use the downloaded file to install the  Azure Backup Add-In on your Windows Server Essentials server. If you do not have a Microsoft account, you can sign up for a free trial.

 To perform this setup, complete the following tasks:

1.  Sign up for a Microsoft Online Services account and the Backup preview.

2.  Create a backup vault to store online backups.

3.  Download the  Azure Backup Agent.

4.  Install the  Azure Backup Add-In on the server.

####  <a name="BKMK_SignupforaMicrosoftOnlineServiceAccount"></a> Sign up for a Microsoft Online Services account and the Backup preview

1.  Log on to the Windows Server Essentials Dashboard.

2.  On the Dashboard **Home** page, click the **ADD-INS** category, click **Integrate with Azure Backup**, and then click **Click to sign up for Azure Backup**.

3.  On the  Azure **Recovery Services** page, in the **Backup (Preview)** section, review the details.

4.  If you do not have an  Azure subscription, click **Free Trial**, and then follow the instructions to get an  Azure subscription.

     If you already have an  Azure subscription, click **Portal** in the upper-right corner of the web page to go to the  Azure Management Portal.

5.  On the  Azure Management Portal page, you'll see **Recovery Services** in the left pane. That's where you'll manage the backup vaults that store your online backups from Windows Server Essentials.

####  <a name="BKMK_Createabackupvaulttostoreonlinebackups"></a> Create a backup vault to store online backups

1.  Sign in to the [Azure Management Portal](https://portal.azure.com)from the web browser on your Windows Server Essentials server.

2.  In the  Azure Management Portal, click **New**, click **Data Services**, click **Recovery Services**, click **Backup Vault**, and then click **Quick Create**.

3.  Enter a name for your backup vault, choose the region where you want to store your backups, and then click **Quick Create**.

     The **Recovery Services** area opens with your new backup vault displayed.

####  <a name="BKMK_DownloadtheWindowsAzureBackupAgent"></a> Download the Azure Backup Agent

1.  Open the Windows Server Essentials Dashboard.

2.  On the Dashboard **Home** page, click the **Get Started** tab, click the **ADD-INS** category, click **Integrate with Azure Backup**, and then click **Click to download Azure Backup integration module**.

####  <a name="BKMK_InstalltheWindowsAzureBackupAddIn"></a> Install the Azure Backup Add-In on the server

1. Sign in to your server using an administrator account, and then run the **OnlineBackupAddin.wssx** file that you downloaded in the preceding step.

2. The **Software License Terms** are displayed. If you agree with the terms and conditions, click **Accept** to continue the installation.

3. On the **Install the add-in** page, click **Install the Add-in**.

   > [!NOTE]
   >  You might be required to restart the server in order to install any prerequisite software.

    The **Installation** page is displayed. A progress indicator displays when the installation begins and shows the progress of the installation. When the installation is complete, you will receive a message that the  Azure Backup Add-in was installed successfully.

4. Click **Finish**.

5. Close and reopen the Dashboard.

    A new tab, **Online Backup**, is added to the Dashboard. From this tab, you can register your server, configure backup settings, and open **Recovery Services** in the  Azure Management Portal to manage the backup vaults for your servers.

   After completing these steps, do the following:

6. In  Windows Server Essentials, upload a certificate to use for online backups. For more information, see [Upload a certificate to the Azure Backup vault](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1).

7. Register the server with the  Azure Backup vault. For more information, see [Register this server for backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5).

8. Configure online backup of the server. For more information, see [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2).

###  <a name="BKMK_17"></a> Integrate Azure Backup with Windows Server Essentials
 The  Microsoft Azure Backup integration module is a new feature of Windows Server Essentials that enables you to encrypt and back up files and folders from your server to an  Azure-hosted storage system provided by Microsoft. By using  Azure Backup to encrypt and back up data on the server, you can help prevent catastrophic loss of critical business data due to fire, flood, theft, or other disasters. When you use  Azure Backup to back up server data, the information is encrypted using your passphrase before it is uploaded to a secure datacenter on the Internet. To access data from an online backup, you must have a server that is authenticated by a certificate and must provide the passphrase.

 After integrating and registering the server with  Azure Backup, you can configure online backup settings to perform regularly scheduled backups. You can also initiate an online backup at any time by clicking the **Start backup now** task in the Online Backup Dashboard.

 The online backup setup involves these steps:

1.  [Sign up for Azure Backup Service](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_16) - After you sign up for the Backup service, you will create a backup vault, download and install the  Azure Backup integration module.

2.  [Upload a certificate to the Azure Backup vault](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_1)

3.  [Register this server for backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_5)

4.  [Configure online backup](Manage-Online-Backup-in-Windows-Server-Essentials.md#BKMK_2)

> [!NOTE]
>   Azure Backup uses the passphrase to encrypt files and folders for the online backup. Changing the encryption passphrase will replace the passphrase that you specified when you registered the server. The passphrase accepts only ASCII-coded characters.

###  <a name="BKMK_18"></a> Protect folders for online backup in Windows Server Essentials
 The **Protected Folders** sub-section in the Online Backup section of the Dashboard displays a list of all shared folders on the server. The following table describes the information that is included in the list.

|Column|Description|
|------------|-----------------|
|**Folder Name:**|The name of the folder that is included in the online backup.<br /><br /> To add or exclude a folder, run the **Configure online backup** task.|
|**Folder Path:**|The location of the folder.|
|**Status:**|There are three types of status - **Protected**, **Not protected**, and **Unknown**.|

###  <a name="BKMK_19"></a> Online backup history in Windows Server Essentials
 The **Backup History** sub-section in the Online Backup section of the Dashboard displays a list of recent online backups. You can use successful backups to restore file and folders. The following table describes the information that is included in the list.

|Column|Description|
|------------|-----------------|
|**Operation:**|There are two types of operations - **Backup** and **Restore**.|
|**Time:**|This is the time logged for the most recent status.|
|**Status:**|There are five types of status - **Success**, **In progress**, **Canceled**, **Warning**, and **Unsuccessful**.|

## Additional References

-   [Manage Backup and Restore](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)

-   [Manage Microsoft Online Services](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)

-   [Manage Windows Server Essentials](Manage-Windows-Server-Essentials.md)

-   [Use Windows Server Essentials](../use/Use-Windows-Server-Essentials.md)
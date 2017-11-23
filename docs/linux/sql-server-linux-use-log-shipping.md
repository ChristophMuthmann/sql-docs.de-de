---
title: "Konfigurieren des Protokollversands für SQL Server on Linux | Microsoft Docs"
description: "Dieses Lernprogramm zeigt ein einfaches Beispiel dafür, wie eine SQL Server-Instanz unter Linux auf einer sekundären Instanz, die unter Verwendung des Protokollversands repliziert."
author: meet-bhagdev
ms.author: meetb
manager: jhubbard
ms.date: 04/19/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 443330a48628e17f7dfa9688e57bb58b118605b6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="get-started-with-log-shipping-on-linux"></a>Erste Schritte mit Protokollversand unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server-Protokollversand ist eine HA-Konfiguration, in dem eine Datenbank von einem primären Server auf einem oder mehreren sekundären Servern repliziert. Kurz gesagt, ist eine Sicherung der Quelldatenbank auf dem sekundären Server wiederhergestellt. Klicken Sie dann der primäre Server erstellt Sicherungen des Transaktionsprotokolls in regelmäßigen Abständen und die sekundären Servern wiederhergestellt werden, aktualisieren die sekundäre Kopie der Datenbank. 

  ![Protokollversandmonitors](https://preview.ibb.co/hr5Ri5/logshipping.png)


Wie in der Abbildung weiter oben beschrieben, umfasst eine protokollversandsitzung die folgenden Schritte aus:

- Sichern die Transaktionsprotokolldatei auf dem primären SQL Server-Instanz
- Die Protokollsicherungsdatei Transaktion kopiert über das Netzwerk, auf eine oder mehrere sekundäre SQL Server-Instanzen
- Wiederherstellen der Sicherung Transaktionsprotokolldatei auf der sekundären SQL Server-Instanzen

## <a name="prerequisites"></a>Erforderliche Komponenten
- [Installieren von SQL Server-Agent für Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup-sql-agent)

## <a name="setup-a-network-share-for-log-shipping-using-cifs"></a>Setup einer Netzwerkfreigabe für den Protokollversand mithilfe von CIFS 

> [!NOTE] 
> Dieses Lernprogramm verwendet CIFS + Samba So richten Sie die Netzwerkfreigabe an. Wenn Sie NFS verwenden möchten, einen Kommentar ein, und diese des Dokuments hinzugefügt wird.       

### <a name="configure-primary-server"></a>Konfigurieren des primären Servers
-   Führen Sie Folgendes ein, um Samba installieren

    ```bash
    sudo apt-get install samba #For Ubuntu
    sudo yum -y install samba #For RHEL/CentOS
    ```
-   Erstellen eines Verzeichnisses zum Speichern der Protokolle für den Protokollversand und Mssql die erforderlichen Berechtigungen

    ```bash
    mkdir /var/opt/mssql/tlogs
    chown mssql:mssql /var/opt/mssql/tlogs
    chmod 0700 /var/opt/mssql/tlogs
    ```

-   Bearbeiten Sie die /etc/samba/smb.conf-Datei (benötigt Root-Berechtigung für diesen), und fügen Sie folgenden Abschnitt:

    ```bash
    [tlogs]
    path=/var/opt/mssql/tlogs
    available=yes
    read only=yes
    browsable=yes
    public=yes
    writable=no
    ```

-   Erstellen Sie einen Mssql-Benutzer für Samba

    ```bash
    sudo smbpasswd -a mssql
    ```

-   Starten Sie die Samba-Dienste
    ```bash
    sudo systemctl restart smbd.service nmbd.service
    ```
 
### <a name="configure-secondary-server"></a>Konfigurieren von sekundären Server

-   Führen Sie Folgendes ein, um den CIFS-Client installieren
    ```bash   
    sudo apt-get install cifs-utils #For Ubuntu
    sudo yum -y install cifs-utils #For RHEL/CentOS
    ```

-   Erstellen Sie eine Datei, um Ihre Anmeldeinformationen zu speichern. Verwenden Sie das Kennwort, die, das Sie vor kurzem für Ihre Mssql Samba-Konto festgelegt 

        vim /var/opt/mssql/.tlogcreds
        #Paste the following in .tlogcreds
        username=mssql
        domain=<domain>
        password=<password>

-   Führen Sie die folgenden Befehle zum Erstellen eines leeren Verzeichnis bereitstellen, und legen Sie Berechtigungen und zum Eigentum ordnungsgemäß
    ```bash   
    mkdir /var/opt/mssql/tlogs
    sudo chown root:root /var/opt/mssql/tlogs
    sudo chmod 0550 /var/opt/mssql/tlogs
    sudo chown root:root /var/opt/mssql/.tlogcreds
    sudo chmod 0660 /var/opt/mssql/.tlogcreds
    ```

-   Fügen Sie die Zeile an usw./Fstab, um die Freigabe persistent zu speichern 

        //<ip_address_of_primary_server>/tlogs /var/opt/mssql/tlogs cifs credentials=/var/opt/mssql/.tlogcreds,ro,uid=mssql,gid=mssql 0 0
        
-   Bereitstellen von den Freigaben
    ```bash   
    sudo mount -a
    ```
       
## <a name="setup-log-shipping-via-t-sql"></a>Einrichten des Protokollversands mit T-SQL

- Führen Sie dieses Skript von Ihrem primären server

    ```tsql
    BACKUP DATABASE SampleDB
    TO DISK = '/var/opt/mssql/tlogs/SampleDB.bak'
    GO
    ```
    ```tsql
    DECLARE @LS_BackupJobId AS uniqueidentifier 
    DECLARE @LS_PrimaryId   AS uniqueidentifier 
    DECLARE @SP_Add_RetCode As int 
    EXEC @SP_Add_RetCode = master.dbo.sp_add_log_shipping_primary_database 
             @database = N'SampleDB' 
            ,@backup_directory = N'/var/opt/mssql/tlogs' 
            ,@backup_share = N'/var/opt/mssql/tlogs' 
            ,@backup_job_name = N'LSBackup_SampleDB' 
            ,@backup_retention_period = 4320
            ,@backup_compression = 2
            ,@backup_threshold = 60 
            ,@threshold_alert_enabled = 1
            ,@history_retention_period = 5760 
            ,@backup_job_id = @LS_BackupJobId OUTPUT 
            ,@primary_id = @LS_PrimaryId OUTPUT 
            ,@overwrite = 1 

    IF (@@ERROR = 0 AND @SP_Add_RetCode = 0) 
    BEGIN 

    DECLARE @LS_BackUpScheduleUID   As uniqueidentifier 
    DECLARE @LS_BackUpScheduleID    AS int 

    EXEC msdb.dbo.sp_add_schedule 
            @schedule_name =N'LSBackupSchedule' 
            ,@enabled = 1 
            ,@freq_type = 4 
            ,@freq_interval = 1 
            ,@freq_subday_type = 4 
            ,@freq_subday_interval = 15 
            ,@freq_recurrence_factor = 0 
            ,@active_start_date = 20170418 
            ,@active_end_date = 99991231 
            ,@active_start_time = 0 
            ,@active_end_time = 235900 
            ,@schedule_uid = @LS_BackUpScheduleUID OUTPUT 
            ,@schedule_id = @LS_BackUpScheduleID OUTPUT 

    EXEC msdb.dbo.sp_attach_schedule 
            @job_id = @LS_BackupJobId 
            ,@schedule_id = @LS_BackUpScheduleID  

    EXEC msdb.dbo.sp_update_job 
            @job_id = @LS_BackupJobId 
            ,@enabled = 1 
            
    END 

    EXEC master.dbo.sp_add_log_shipping_alert_job 

    EXEC master.dbo.sp_add_log_shipping_primary_secondary 
            @primary_database = N'SampleDB' 
            ,@secondary_server = N'<ip_address_of_secondary_server>' 
            ,@secondary_database = N'SampleDB' 
            ,@overwrite = 1 
    ```


- Führen Sie dieses Skript aus dem sekundären server

    ```tsql
    RESTORE DATABASE SampleDB FROM DISK = '/var/opt/mssql/tlogs/SampleDB.bak'
    WITH NORECOVERY;
    ```
    
    ```tsql
    DECLARE @LS_Secondary__CopyJobId    AS uniqueidentifier 
    DECLARE @LS_Secondary__RestoreJobId AS uniqueidentifier 
    DECLARE @LS_Secondary__SecondaryId  AS uniqueidentifier 
    DECLARE @LS_Add_RetCode As int 

    EXEC @LS_Add_RetCode = master.dbo.sp_add_log_shipping_secondary_primary 
            @primary_server = N'<ip_address_of_primary_server>' 
            ,@primary_database = N'SampleDB' 
            ,@backup_source_directory = N'/var/opt/mssql/tlogs/' 
            ,@backup_destination_directory = N'/var/opt/mssql/tlogs/' 
            ,@copy_job_name = N'LSCopy_SampleDB' 
            ,@restore_job_name = N'LSRestore_SampleDB' 
            ,@file_retention_period = 4320 
            ,@overwrite = 1 
            ,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT 
            ,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT 
            ,@secondary_id = @LS_Secondary__SecondaryId OUTPUT 

    IF (@@ERROR = 0 AND @LS_Add_RetCode = 0) 
    BEGIN 

    DECLARE @LS_SecondaryCopyJobScheduleUID As uniqueidentifier 
    DECLARE @LS_SecondaryCopyJobScheduleID  AS int 

    EXEC msdb.dbo.sp_add_schedule 
            @schedule_name =N'DefaultCopyJobSchedule' 
            ,@enabled = 1 
            ,@freq_type = 4 
            ,@freq_interval = 1 
            ,@freq_subday_type = 4 
            ,@freq_subday_interval = 15 
            ,@freq_recurrence_factor = 0 
            ,@active_start_date = 20170418 
            ,@active_end_date = 99991231 
            ,@active_start_time = 0 
            ,@active_end_time = 235900 
            ,@schedule_uid = @LS_SecondaryCopyJobScheduleUID OUTPUT 
            ,@schedule_id = @LS_SecondaryCopyJobScheduleID OUTPUT 

    EXEC msdb.dbo.sp_attach_schedule 
            @job_id = @LS_Secondary__CopyJobId 
            ,@schedule_id = @LS_SecondaryCopyJobScheduleID  

    DECLARE @LS_SecondaryRestoreJobScheduleUID  As uniqueidentifier 
    DECLARE @LS_SecondaryRestoreJobScheduleID   AS int 

    EXEC msdb.dbo.sp_add_schedule 
            @schedule_name =N'DefaultRestoreJobSchedule' 
            ,@enabled = 1 
            ,@freq_type = 4 
            ,@freq_interval = 1 
            ,@freq_subday_type = 4 
            ,@freq_subday_interval = 15 
            ,@freq_recurrence_factor = 0 
            ,@active_start_date = 20170418 
            ,@active_end_date = 99991231 
            ,@active_start_time = 0 
            ,@active_end_time = 235900 
            ,@schedule_uid = @LS_SecondaryRestoreJobScheduleUID OUTPUT 
            ,@schedule_id = @LS_SecondaryRestoreJobScheduleID OUTPUT 

    EXEC msdb.dbo.sp_attach_schedule 
            @job_id = @LS_Secondary__RestoreJobId 
            ,@schedule_id = @LS_SecondaryRestoreJobScheduleID  
            
    END 
    DECLARE @LS_Add_RetCode2    As int 
    IF (@@ERROR = 0 AND @LS_Add_RetCode = 0) 
    BEGIN 

    EXEC @LS_Add_RetCode2 = master.dbo.sp_add_log_shipping_secondary_database 
            @secondary_database = N'SampleDB' 
            ,@primary_server = N'<ip_address_of_primary_server>' 
            ,@primary_database = N'SampleDB' 
            ,@restore_delay = 0 
            ,@restore_mode = 0 
            ,@disconnect_users  = 0 
            ,@restore_threshold = 45   
            ,@threshold_alert_enabled = 1 
            ,@history_retention_period  = 5760 
            ,@overwrite = 1 

    END 

    IF (@@error = 0 AND @LS_Add_RetCode = 0) 
    BEGIN 

    EXEC msdb.dbo.sp_update_job 
            @job_id = @LS_Secondary__CopyJobId 
            ,@enabled = 1 

    EXEC msdb.dbo.sp_update_job 
            @job_id = @LS_Secondary__RestoreJobId 
            ,@enabled = 1 

    END 
    ```

## <a name="verify-log-shipping-works"></a>Überprüfen Sie die Funktionsweise des Protokollversands

- Stellen Sie sicher, dass der Protokollversand funktioniert, indem der folgende Auftrag auf dem primären Server ab

    ```tsql
    USE msdb ;  
    GO  

    EXEC dbo.sp_start_job N'LSBackup_SampleDB' ;  
    GO  
    ```

- Stellen Sie sicher, dass der Protokollversand funktioniert, indem der folgende Auftrag auf dem sekundären Server ab
 
    ```tsql
    USE msdb ;  
    GO  

    EXEC dbo.sp_start_job N'LSCopy_SampleDB' ;  
    GO  
    EXEC dbo.sp_start_job N'LSRestore_SampleDB' ;  
    GO  
    RESTORE DATABASE SampleDB WITH RECOVERY;
    ```



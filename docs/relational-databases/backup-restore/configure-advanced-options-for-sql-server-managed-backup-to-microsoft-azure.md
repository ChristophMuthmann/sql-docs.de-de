---
title: "Konfigurieren der erweiterten Optionen f&#252;r die verwaltete Sicherung von SQL Server zu Microsoft Azure | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
caps.latest.revision: 8
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 7
---
# Konfigurieren der erweiterten Optionen f&#252;r die verwaltete Sicherung von SQL Server zu Microsoft Azure
  Das folgende Tutorial beschreibt, wie Sie erweiterte Optionen für [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] festlegen. Diese Prozeduren sind nur notwendig, wenn Sie die Funktionen benötigen, die sie bieten. Andernfalls können Sie [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] aktivieren und sich auf das Standardverhalten verlassen.  
  
 In jedem Szenario wird die Sicherung mit dem `database_name`-Parameter angegeben. Wenn `database_name` NULL oder * ist, beeinflussen die Änderungen die Standardeinstellungen auf Instanzebene. Instanzebeneneinstellungen wirken sich auch auf neue Datenbanken aus, die nach der Änderung erstellt wurden.  
  
 Nachdem Sie diese Einstellungen angegeben haben, können Sie die verwaltete Sicherung für die Datenbank oder Instanz mithilfe der gespeicherten Systemprozedur [managed_backup.sp_backup_config_basic &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) aktivieren. Weitere Informationen finden Sie unter [Aktivieren der verwalteten SQL Server-Sicherung in Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
> [!WARNING]  
>  Sie sollten immer die erweiterten Optionen und benutzerdefinierte Planungsoptionen konfigurieren, bevor Sie [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] mit [managed_backup.sp_backup_config_basic &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md) aktivieren. Andernfalls kann es sein, dass es im Zeitfenster zwischen der Aktivierung von [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] und der Konfiguration dieser Einstellungen zu unerwünschten Sicherungsvorgängen kommt.  
  
## Konfigurieren der Verschlüsselung  
 Die folgenden Schritte beschreiben, wie Sie die Einstellungen für die Verschlüsselung mithilfe der gespeicherten Prozedur [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) angegeben.  
  
1.  **Den Verschlüsselungsalgorithmus bestimmen:** Bestimmen Sie zunächst den Namen des Verschlüsselungsalgorithmus, der verwendet werden soll. Wählen Sie einen der folgenden Algorithmen aus:  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **Erstellen Sie einen Datenbank-Hauptschlüssel:** Wählen Sie ein Kennwort zum Verschlüsseln der Kopie des Hauptschlüssels aus, der in der Datenbank gespeichert wird.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **Ein Sicherungszertifikat oder einen asymmetrischen Schlüssel erstellen:** Sie können ein Zertifikat oder einen asymmetrischen Schlüssel mit der Verschlüsselung verwenden. Im folgenden Beispiel wird ein Sicherungszertifikat für die Verschlüsselung erstellt.  
  
    ```tsql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **Die Verschlüsselung für die verwaltete Sicherung festlegen:** Rufen Sie die gespeicherte Prozedur **managed_backup.sp_backup_config_advanced** mit den entsprechenden Werten auf. Im folgenden Beispiel wird z.B. die `MyDB`-Datenbank für die Verschlüsselung mit einem Zertifikat namens `MyTestDBBackupEncryptCert` und dem `AES_128`-Verschlüsselungsalgorithmus konfiguriert.  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  Wenn `@database_name` im vorherigen Beispiel NULL ist, werden die Einstellungen auf die SQL Server-Instanz angewendet.  
  
## Konfigurieren eines benutzerdefinierten Sicherungszeitplans  
 Die folgenden Schritte beschreiben, wie Sie einen benutzerdefinierten Zeitplan mithilfe der gespeicherten Prozedur [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) angegeben.  
  
1.  **Die Häufigkeit für vollständige Sicherungen ermitteln:** Bestimmen Sie, wie häufig vollständige Sicherungskopien der Datenbank erstellt werden sollen. Sie können für die vollständigen Sicherungen zwischen den Optionen „Täglich“ und „Wöchentlich“ wählen.  
  
2.  **Die Häufigkeit für Protokollsicherungen ermitteln:** Bestimmen Sie, wie häufig Protokollsicherungen erstellt werden sollen. Dieser Wert wird in Minuten oder Stunden angegeben.  
  
3.  **Den Wochentag für wöchentliche Sicherungen bestimmen:** Wenn die Sicherung wöchentlich durchgeführt wird, können Sie den Wochentag für die vollständige Sicherung auswählen.  
  
4.  **Die Startzeit für die Sicherung bestimmen:** Sie können die Startzeit für die Sicherung im 24-Stunden-Format angeben.  
  
5.  **Die Dauer der Sicherung bestimmen:** Sie können die Zeitspanne bestimmen, in der eine Sicherung abgeschlossen werden soll.  
  
6.  **Den benutzerdefinierten Sicherungszeitplan festlegen:** Die folgende gespeicherte Prozedur definiert einen benutzerdefinierten Zeitplan für die `MyDB`-Datenbank. Vollständige Sicherungen werden wöchentlich am `Monday` um `17:30` durchgeführt. Protokollsicherungen werden alle `5` Minuten durchgeführt. Sicherungen müssen innerhalb von zwei Stunden abgeschlossen sein.  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## Nächste Schritte  
 Nach dem Konfigurieren der erweiterten Optionen und der benutzerdefinierten Zeitpläne müssen Sie [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] auf der Zieldatenbank oder der SQL Server-Instanz aktivieren. Weitere Informationen finden Sie unter [Aktivieren der verwalteten SQL Server-Sicherung in Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
## Siehe auch  
 [SQL Server Managed Backup für Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
---
title: Sp_add_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_primary_database
- sp_add_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_primary_database
ms.assetid: 69531611-113f-46b5-81a6-7bf496d0353c
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 002e467254e145a3299b12f3df2f7d1e0e491955
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddlogshippingprimarydatabase-transact-sql"></a>sp_add_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Richtet die primäre Datenbank, einschließlich des Sicherungsauftrags sowie des lokalen und Remoteüberwachungseintrags, für eine Protokollversandkonfiguration ein.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_log_shipping_primary_database [ @database = ] 'database',   
[ @backup_directory = ] 'backup_directory',   
[ @backup_share = ] 'backup_share',   
[ @backup_job_name = ] 'backup_job_name',   
[, [ @backup_retention_period = ] backup_retention_period]  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @backup_threshold = ] backup_threshold ]   
[, [ @threshold_alert = ] threshold_alert ]   
[, [ @threshold_alert_enabled = ] threshold_alert_enabled ]   
[, [ @history_retention_period = ] history_retention_period ]  
[, [ @backup_job_id = ] backup_job_id OUTPUT ]  
[, [ @primary_id = ] primary_id OUTPUT]  
[, [ @backup_compression = ] backup_compression_option ]  
  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@database=** ] "*Datenbank*"  
 Der Name der primären Datenbank des Protokollversands. *database* ist vom Datentyp **sysname**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [  **@backup_directory=** ] "*Backup_directory*"  
 Der Pfad zum Sicherungsordner auf dem primären Server. *Backup_directory* ist **nvarchar(500)**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [  **@backup_share=** ] "*Backup_share*"  
 Der Netzwerkpfad zum Sicherungsverzeichnis auf dem primären Server. *Backup_share* ist **nvarchar(500)**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [  **@backup_job_name=** ] "*Backup_job_name*"  
 Der Name des SQL Server-Agent-Auftrags auf dem primären Server, der die Sicherung in den Sicherungsordner kopiert. *Backup_job_name* ist **Sysname** und darf nicht NULL sein.  
  
 [  **@backup_retention_period=** ] *Backup_retention_period*  
 Die Zeitdauer (in Minuten), für die die Protokollsicherungsdatei im Sicherungsverzeichnis auf dem primären Server gespeichert wird. *Backup_retention_period* ist **Int**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [  **@monitor_server=** ] "*Monitor_server*"  
 Der Name des Überwachungsservers. *Monitor_server* ist **Sysname**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [  **@monitor_server_security_mode=** ] *Monitor_server_security_mode*  
 Der Sicherheitsmodus, der zum Herstellen einer Verbindung mit dem Überwachungsserver verwendet wird.  
  
 1 = Windows-Authentifizierung  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. *monitor_server_security_mode* ist vom Datentyp **bit** und darf nicht NULL sein.  
  
 [  **@monitor_server_login=** ] "*Monitor_server_login*"  
 Der Benutzername für das Konto, das zum Zugreifen auf den Überwachungsserver verwendet wird.  
  
 [  **@monitor_server_password=** ] "*Monitor_server_password*"  
 Das Kennwort des Kontos, das zum Zugreifen auf den Überwachungsserver verwendet wird.  
  
 [  **@backup_threshold=** ] *Backup_threshold*  
 Ist die Zeitdauer in Minuten, nach der letzten Sicherung, bevor eine *Threshold_alert* Fehler ausgelöst. *Backup_threshold* ist **Int**, hat den Standardwert von 60 Minuten.  
  
 [  **@threshold_alert=** ] *Threshold_alert*  
 Die Warnung, die bei Überschreiten des Sicherungsschwellenwerts ausgelöst wird. *Threshold_alert* ist **Int**, hat den Standardwert 14,420.  
  
 [  **@threshold_alert_enabled=** ] *Threshold_alert_enabled*  
 Gibt an, ob eine Warnung wird ausgelöst, wenn *Backup_threshold* überschritten wird. Der Standardwert null (0) bedeutet, dass die Warnung deaktiviert ist und nicht ausgelöst wird. *Threshold_alert_enabled* ist **Bit**.  
  
 [  **@history_retention_period=** ] *History_retention_period*  
 Der Zeitraum (in Minuten), für den der Verlauf beibehalten wird. *history_retention_period* ist vom Datentyp **int**. Der Standardwert ist NULL. Der Wert 14420 wird verwendet, falls kein anderer Wert angegeben wird.  
  
 [  **@backup_job_id=** ] *Backup_job_id* Ausgabe  
 Die ID des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Auftrags, die dem Sicherungsauftrag auf dem primären Server zugeordnet ist. *Backup_job_id* ist **"uniqueidentifier"** und darf nicht NULL sein.  
  
 [  **@primary_id=** ] *Primary_id* Ausgabe  
 Die ID der primären Datenbank für die Protokollversandkonfiguration. *primary_id* ist vom Datentyp **uniqueidentifier** und darf nicht NULL sein.  
  
 [ **@backup_compression**=] *Backup_compression_option*  
 Gibt an, ob eine Protokollversandkonfiguration verwendet [sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md). Dieser Parameter wird nur in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (oder einer höheren Version) unterstützt.  
  
 0 = Deaktiviert. Protokollsicherungen nie komprimieren.  
  
 1 = Aktiviert. Protokollsicherungen immer komprimieren.  
  
 2 = Einstellung der der [anzeigen oder Konfigurieren der Serverkonfigurationsoption backup Compression Default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Dies ist der Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_add_log_shipping_primary_database** muss ausgeführt werden, aus der **master** Datenbank auf dem primären Server. Diese gespeicherte Prozedur führt die folgenden Aktionen aus:  
  
1.  Generieren einer primären ID und fügt einen Eintrag für die primäre Datenbank in der Tabelle **Log_shipping_primary_databases** mit den angegebenen Argumenten.  
  
2.  Erstellen eines Sicherungsauftrags für die primäre Datenbank, die deaktiviert ist.  
  
3.  Festlegen der Sicherungsauftrags-ID in der **Log_shipping_primary_databases** Eintrag, um die Auftrags-ID des Sicherungsauftrags an.  
  
4.  Hinzufügen eines lokalen Überwachungsdatensatzes in der Tabelle **Log_shipping_monitor_primary** auf dem primären Server mithilfe bereitgestellter Argumente.  
  
5.  Wenn der Überwachungsserver nicht mit dem primären Server übereinstimmt, fügt ein Überwachungsdatensatz in **Log_shipping_monitor_primary** auf dem Server mithilfe bereitgestellter Argumente.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank als primäre Datenbank in einer Protokollversandkonfiguration hinzugefügt.  
  
```  
DECLARE @LS_BackupJobId AS uniqueidentifier ;  
DECLARE @LS_PrimaryId AS uniqueidentifier ;  
  
EXEC master.dbo.sp_add_log_shipping_primary_database   
@database = N'AdventureWorks'   
,@backup_directory = N'c:\lsbackup'   
,@backup_share = N'\\tribeca\lsbackup'   
,@backup_job_name = N'LSBackup_AdventureWorks'   
,@backup_retention_period = 1440  
,@monitor_server = N'rockaway'   
,@monitor_server_security_mode = 1   
,@backup_threshold = 60   
,@threshold_alert = 0   
,@threshold_alert_enabled = 0   
,@history_retention_period = 1440   
,@backup_job_id = @LS_BackupJobId OUTPUT   
,@primary_id = @LS_PrimaryId OUTPUT   
,@overwrite = 1   
,@backup_compression = 0;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

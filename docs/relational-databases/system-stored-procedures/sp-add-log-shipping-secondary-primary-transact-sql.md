---
title: Sp_add_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_secondary_primary_TSQL
- sp_add_log_shipping_secondary_primary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_secondary_primary
ms.assetid: bfbbbee2-c255-4a59-a963-47d6e980a8e2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c83d0a0062f7f7affc19e91b929bb16831a8946d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spaddlogshippingsecondaryprimary-transact-sql"></a>sp_add_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Richtet die primären Informationen ein, fügt Links zur lokalen und Remoteüberwachung hinzu und erstellt auf dem sekundären Server Kopier- und Wiederherstellungsaufträge für die angegebene primäre Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_log_shipping_secondary_primary  
 [ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database',  
[ @backup_source_directory = ] 'backup_source_directory' ,   
[ @backup_destination_directory = ] 'backup_destination_directory'  
[ @copy_job_name = ] 'copy_job_name'  
[ @restore_job_name = ] 'restore_job_name'  
[, [ @file_retention_period = ] 'file_retention_period']  
[, [ @monitor_server = ] 'monitor_server']  
[, [ @monitor_server_security_mode = ] 'monitor_server_security_mode']  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
[, [ @copy_job_id = ] 'copy_job_id' OUTPUT ]  
[, [ @restore_job_id = ] 'restore_job_id' OUTPUT ]  
[, [ @secondary_id = ] 'secondary_id' OUTPUT]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@primary_server** = ] '*primary_server*'  
 Der Name der primären Instanz von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in der Protokollversandkonfiguration. *primary_server* ist vom Datentyp **sysname** und darf nicht NULL sein.  
  
 [ **@primary_database** = ] '*primary_database*'  
 Der Name der Datenbank auf dem primären Server. *primary_database* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [ **@backup_source_directory** = ] '*backup_source_directory*'  
 Das Verzeichnis, in dem die Dateien der Transaktionsprotokollsicherung gespeichert werden. *backup_source_directory* ist vom Datentyp **nvarchar(500)** und darf nicht NULL sein.  
  
 [ **@backup_destination_directory** = ] '*backup_destination_directory*'  
 Das Verzeichnis auf dem sekundären Server, in das Sicherungsdateien kopiert werden *backup_destination_directory* ist vom Datentyp **nvarchar(500)** und darf nicht NULL sein.  
  
 [ **@copy_job_name** = ] '*copy_job_name*'  
 Der Name für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentauftrag, der erstellt wird, um Transaktionsprotokollsicherungen auf den sekundären Server zu kopieren. *Copy_job_name* ist **Sysname** und darf nicht NULL sein.  
  
 [  **@restore_job_name**  =] '*Restore_job_name*"  
 Der Name des der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag auf dem sekundären Server, die die Sicherungen in der sekundären Datenbank wiederherstellt. *Restore_job_name* ist **Sysname** und darf nicht NULL sein.  
  
 [ **@file_retention_period** = ] '*file_retention_period*'  
 Die Zeitdauer in Minuten an, die in eine Sicherungsdatei, auf dem sekundären Server im angegebenen Pfad beibehalten wird die @backup_destination_directory Parameter vor dem Löschvorgang. *history_retention_period* ist vom Datentyp **int**. Der Standardwert ist NULL. Der Wert 14420 wird verwendet, falls kein anderer Wert angegeben wird.  
  
 [ **@monitor_server** = ] '*monitor_server*'  
 Der Name des Überwachungsservers. *Monitor_server* ist **Sysname**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [ **@monitor_server_security_mode** = ] '*monitor_server_security_mode*'  
 Der Sicherheitsmodus, der zum Herstellen einer Verbindung mit dem Überwachungsserver verwendet wird.  
  
 1 = Windows-Authentifizierung  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung  
  
 *monitor_server_security_mode* ist vom Datentyp **bit** und darf nicht NULL sein.  
  
 [  **@monitor_server_login**  =] '*Monitor_server_login*"  
 Der Benutzername für das Konto, das zum Zugreifen auf den Überwachungsserver verwendet wird.  
  
 [  **@monitor_server_password**  =] '*Monitor_server_password*"  
 Das Kennwort des Kontos, das zum Zugreifen auf den Überwachungsserver verwendet wird.  
  
 [ **@copy_job_id** = ] '*copy_job_id*' OUTPUT  
 Die dem Kopierauftrag zugeordnete ID auf dem sekundären Server *copy_job_id* is **uniqueidentifier** and cannot be NULL.  
  
 [ **@restore_job_id** = ] '*restore_job_id*' OUTPUT  
 Die dem Wiederherstellungsauftrag zugeordnete ID auf dem sekundären Server *Restore_job_id* ist **"uniqueidentifier"** und darf nicht NULL sein.  
  
 [ **@secondary_id** = ] '*secondary_id*' OUTPUT  
 Die ID für den sekundären Server in der Protokollversandkonfiguration. *Secondary_id* ist **"uniqueidentifier"** und darf nicht NULL sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_add_log_shipping_secondary_primary** muss ausgeführt werden, aus der **master** Datenbank auf dem sekundären Server. Diese gespeicherte Prozedur führt folgende Aktionen aus:  
  
1.  Generiert eine sekundäre ID für den angegebenen primären Server und die primäre Datenbank.  
  
2.  Führt Folgendes aus:  
  
    1.  Fügt einen Eintrag für die sekundäre ID in **Log_shipping_secondary** mit den angegebenen Argumenten.  
  
    2.  Erstellt einen Kopierauftrag für die sekundäre ID, die deaktiviert ist.  
  
    3.  Legt die Kopierauftrags-ID in der **Log_shipping_secondary** Eintrag, um die Auftrags-ID des Kopierauftrags.  
  
    4.  Erstellt einen Wiederherstellungsauftrag für die sekundäre ID, die deaktiviert ist.  
  
    5.  Legen Sie die Restore-Auftrags-ID in der **Log_shipping_secondary** Eintrag, um die Auftrags-ID für den Wiederherstellungsauftrag.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird die Verwendung der **Sp_add_log_shipping_secondary_primary** gespeicherte Prozedur Informationen für die primäre Datenbank einrichten [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] auf dem sekundären Server.  
  
```  
EXEC master.dbo.sp_add_log_shipping_secondary_primary   
@primary_server = N'TRIBECA'   
,@primary_database = N'AdventureWorks'   
,@backup_source_directory = N'\\tribeca\LogShipping'   
,@backup_destination_directory = N''   
,@copy_job_name = N''   
,@restore_job_name = N''   
,@file_retention_period = 1440   
,@monitor_server = N'ROCKAWAY'   
,@monitor_server_security_mode = 1   
,@copy_job_id = @LS_Secondary__CopyJobId OUTPUT   
,@restore_job_id = @LS_Secondary__RestoreJobId OUTPUT   
,@secondary_id = @LS_Secondary__SecondaryId OUTPUT ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand &#40; SQLServer &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

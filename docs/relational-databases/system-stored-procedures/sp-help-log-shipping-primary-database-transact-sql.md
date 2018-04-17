---
title: Sp_help_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- sp_help_log_shipping_primary_database_TSQL
- sp_help_log_shipping_primary_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_database
ms.assetid: e711b01c-ef29-4eb6-a016-0e647e337818
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 257d4310d46f757ab2d34760b99a394bba933330
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelplogshippingprimarydatabase-transact-sql"></a>sp_help_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft Einstellungen der primären Datenbank ab.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_log_shipping_primary_database  
[ @database = ] 'database' OR  
[ @primary_id = ] 'primary_id'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@database =** ] "*Datenbank*"  
 Der Name der primären Datenbank des Protokollversands. *database* ist vom Datentyp **sysname**, hat keinen Standardwert und darf nicht NULL sein.  
  
 [  **@primary_id =** ] "*Primary_id*"  
 Die ID der primären Datenbank für die Protokollversandkonfiguration. *primary_id* ist vom Datentyp **uniqueidentifier** und darf nicht NULL sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**primary_id**|Die ID der primären Datenbank für die Protokollversandkonfiguration.|  
|**primary_database**|Der Name der primären Datenbank in der Protokollversandkonfiguration|  
|**backup_directory**|Das Verzeichnis, in dem die Dateien der Transaktionsprotokollsicherung gespeichert werden.|  
|**backup_share**|Der Netzwerk- oder UNC-Pfad zum Sicherungsverzeichnis.|  
|**backup_retention_period**|Gibt an, wie lange (in Minuten) eine Protokollsicherungsdatei im Sicherungsverzeichnis aufbewahrt wird, bevor sie gelöscht wird.|  
|**backup_compression**|Gibt an, ob die Protokollversandkonfiguration verwendet [sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md).<br /><br /> **0** = Deaktiviert. Protokollsicherungen nie komprimieren.<br /><br /> **1** = Aktiviert. Protokollsicherungen immer komprimieren.<br /><br /> **2** = Einstellung der der [anzeigen oder Konfigurieren der Serverkonfigurationsoption backup Compression Default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md). Dies ist der Standardwert.<br /><br /> Die Komprimierung von Sicherungen wird nur in unterstützt [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (oder eine höhere Version). In allen anderen Versionen ist der Wert immer 2.|  
|**backup_job_id**|Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrags-ID von der Sicherungsauftrag auf dem primären Server zugeordnet.|  
|**monitor_server**|Der Name der Instanz von der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] als Überwachungsserver in der Protokollversandkonfiguration verwendet wird.|  
|**monitor_server_security_mode**|Der Sicherheitsmodus, der zum Herstellen einer Verbindung mit dem Überwachungsserver verwendet wird.<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Authentifizierung<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**backup_threshold**|Die Anzahl von Minuten, die zwischen Sicherungsvorgängen verstreichen darf, bevor eine Warnung generiert wird.|  
|**threshold_alert**|Die Warnung, die bei Überschreiten des Sicherungsschwellenwertes ausgelöst wird.|  
|**threshold_alert_enabled**|Bestimmt, ob Warnungen für Sicherungsschwellenwerte aktiviert sind.<br /><br /> **1** = Aktiviert.<br /><br /> **0** = Deaktiviert.|  
|**last_backup_file**|Der absolute Pfad der jüngsten Transaktionsprotokollsicherung.|  
|**last_backup_date**|Uhrzeit und Datum des letzten Protokollsicherungsvorgangs.|  
|**last_backup_date_utc**|Die Uhrzeit und das Datum der letzten Transaktionsprotokollsicherung in der primären Datenbank in UTC.|  
|**history_retention_period**|Der Zeitraum in Minuten, den Verlaufsdatensätze des Protokollversands für eine bestimmte primäre Datenbank aufbewahrt werden, ehe sie gelöscht werden.|  
  
## <a name="remarks"></a>Hinweise  
 **sp_help_log_shipping_primary_database** muss in der **master** -Datenbank auf dem primären Server ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird die Verwendung **Sp_help_log_shipping_primary_database** zum Abrufen der Einstellungen der primären Datenbank für die Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC master.dbo.sp_help_log_shipping_primary_database @database=N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

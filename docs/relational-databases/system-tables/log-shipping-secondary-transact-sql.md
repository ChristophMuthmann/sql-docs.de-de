---
title: Log_shipping_secondary (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary
- log_shipping_secondary_TSQL
dev_langs: TSQL
helpviewer_keywords: log_shipping_secondary system table
ms.assetid: 69723419-4544-49c6-a517-adb30ffa5741
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa03018420d1c5e23ff41981fd6190407a6a41bc
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="logshippingsecondary-transact-sql"></a>log_shipping_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Speichert einen Datensatz pro sekundärer ID. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**secondary_id**|**uniqueidentifier**|Die ID für den sekundären Server in der Protokollversandkonfiguration.|  
|**primary_server**|**sysname**|Der Name der primären Instanz des SQL Server-Datenbankmoduls in der Protokollversandkonfiguration|  
|**primary_database**|**sysname**|Der Name der primären Datenbank in der Protokollversandkonfiguration|  
|**backup_source_directory**|**nvarchar(500)**|Das Verzeichnis, in dem die Dateien der Transaktionsprotokollsicherung gespeichert werden.|  
|**backup_destination_directory**|**nvarchar(500)**|Das Verzeichnis auf dem sekundären Server, in das Sicherungsdateien kopiert werden|  
|**file_retention_period**|**int**|Gibt an, wie lange (in Minuten) eine Sicherungsdatei auf dem sekundären Server aufbewahrt wird, bevor sie gelöscht wird|  
|**copy_ job_id**|**uniqueidentifier**|Die dem Kopierauftrag zugeordnete ID auf dem sekundären Server|  
|**restore_job_id**|**uniqueidentifier**|Die dem Wiederherstellungsauftrag zugeordnete ID auf dem sekundären Server|  
|**monitor_server**|**sysname**|Der Name der Instanz von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] als Überwachungsserver in der Protokollversandkonfiguration verwendet wird.|  
|**monitor_server_security_mode**|**bit**|Der Sicherheitsmodus, der zum Herstellen einer Verbindung mit dem Überwachungsserver verwendet wird.<br /><br /> 1 = Windows-Authentifizierung<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**last_copied_file**|**nvarchar(500)**|Der Dateiname der letzten Sicherungsdatei, die auf den sekundären Server kopiert wurde.|  
|**last_copied_date**|**datetime**|Datum und Uhrzeit des letzten Kopiervorgangs auf den sekundären Server|  
  
## <a name="remarks"></a>Hinweise  
 Wenn es für eine bestimmte primäre Datenbank mehrere sekundäre Datenbanken auf demselben sekundären Server gibt, nutzen diese einige Einstellungen in der **log_shipping_secondary** -Tabelle gemeinsam. Wenn eine freigegebene Einstellung für eine der Datenbanken geändert wird, ändert sich diese Einstellung für alle Datenbanken.  
  
## <a name="see-also"></a>Siehe auch  
 [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Sp_add_log_shipping_secondary_database &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [Sp_change_log_shipping_secondary_database &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [Sp_delete_log_shipping_secondary_database &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Sp_help_log_shipping_secondary_database &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [Systemtabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

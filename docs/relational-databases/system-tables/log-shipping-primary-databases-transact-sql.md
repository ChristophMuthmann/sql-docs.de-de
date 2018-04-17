---
title: Log_shipping_primary_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3dfd38e9fa44dff09127c72e342223f3ae138c4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingprimarydatabases-transact-sql"></a>log_shipping_primary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Speichert einen Datensatz für die primäre Datenbank in einer Protokollversandkonfiguration. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|Die ID der primären Datenbank für die Protokollversandkonfiguration.|  
|**primary_database**|**sysname**|Der Name der primären Datenbank in der Protokollversandkonfiguration|  
|**backup_directory**|**nvarchar(500)**|Das Verzeichnis, in dem die Dateien der Transaktionsprotokollsicherung gespeichert werden.|  
|**backup_share**|**nvarchar(500)**|Der Netzwerk- oder UNC-Pfad zum Sicherungsverzeichnis.|  
|**backup_retention_period**|**int**|Gibt an, wie lange (in Minuten) eine Protokollsicherungsdatei im Sicherungsverzeichnis aufbewahrt wird, bevor sie gelöscht wird.|  
|**backup_job_id**|**uniqueidentifier**|Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrags-ID von der Sicherungsauftrag auf dem primären Server zugeordnet.|  
|**monitor_server**|**sysname**|Der Name der Instanz von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] als Überwachungsserver in der Protokollversandkonfiguration verwendet wird.|  
|**monitor_server_security_mode**|**bit**|Der Sicherheitsmodus, der zum Herstellen einer Verbindung mit dem Überwachungsserver verwendet wird.<br /><br /> 1 = Windows-Authentifizierung<br /><br /> 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.|  
|**last_backup_file**|**nvarchar(500)**|Der absolute Pfad der jüngsten Transaktionsprotokollsicherung.|  
|**last_backup_date**|**datetime**|Uhrzeit und Datum des letzten Protokollsicherungsvorgangs.|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **Sp_help_log_shipping_primary_database** und **Sp_help_log_shipping_secondary_primary** verwenden Sie diese Spalte zum Steuern der Anzeige der überwachungseinstellungen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> 0 = eine der beiden gespeicherten Prozeduren aufrufen, der Benutzer hat keinen expliziten Wert für die **@monitor_server** Parameter.<br /><br /> 1= Der Benutzer hat einen expliziten Wert angegeben.|  
|**backup_compression**|**tinyint**|Gibt an, ob die Protokollversandkonfiguration das Verhalten der Sicherungskomprimierung auf Serverebene überschreibt.<br /><br /> 0 = Deaktiviert. Protokollsicherungen werden niemals komprimiert, unabhängig von den für den Server konfigurierten Sicherungskomprimierungseinstellungen.<br /><br /> 1 = Aktiviert. Protokollsicherungen werden immer komprimiert, unabhängig von den für den Server konfigurierten Sicherungskomprimierungseinstellungen.<br /><br /> 2 = verwendet die Serverkonfiguration für die [anzeigen oder Konfigurieren der Serverkonfigurationsoption backup Compression Default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) Serverkonfigurationsoption. Dies ist der Standardwert.<br /><br /> Die Sicherungskomprimierung wird nur in der Enterprise Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Sp_add_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [Sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [Sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

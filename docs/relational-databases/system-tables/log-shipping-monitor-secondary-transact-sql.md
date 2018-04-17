---
title: Log_shipping_monitor_secondary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- log_shipping_monitor_secondary_TSQL
- log_shipping_monitor_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_secondary system table
ms.assetid: afbe1bb7-89a7-4020-9408-0af64a043c2e
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29e91437e94fc4eef4f5f65a96f28bb6b8772333
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingmonitorsecondary-transact-sql"></a>log_shipping_monitor_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Speichert einen Überwachungsdatensatz pro sekundärer Datenbank in einer Protokollversandkonfiguration. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
 Die verlaufs- und überwachungsverbundenen Tabellen werden auch auf dem primären und dem sekundären Server verwendet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**secondary_server**|**sysname**|Der Name der sekundären Instanz von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in der Protokollversandkonfiguration.|  
|**secondary_database**|**sysname**|Der Name der sekundären Datenbank in der Protokollversandkonfiguration.|  
|**secondary_id**|**uniqueidentifier**|Die ID für den sekundären Server in der Protokollversandkonfiguration.|  
|**primary_server**|**sysname**|Der Name der primären Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in der Protokollversandkonfiguration.|  
|**primary_database**|**sysname**|Der Name der primären Datenbank in der Protokollversandkonfiguration|  
|**restore_threshold**|**int**|Die Anzahl der zulässigen Minuten zwischen Wiederherstellungsvorgängen, bevor eine Warnung generiert wird.|  
|**threshold_alert**|**int**|Die Warnung, die ausgelöst wird, wenn die Wiederherstellungsschwelle überschritten wird.|  
|**threshold_alert_enabled**|**bit**|Legt fest, ob Warnungen für Wiederherstellungsschwellen aktiviert sind. 1 = Aktiviert.<br /><br /> 0 = Deaktiviert.|  
|**last_copied_file**|**nvarchar(500)**|Der Dateiname der letzten Sicherungsdatei, die auf den sekundären Server kopiert wurde.|  
|**last_copied_date**|**datetime**|Datum und Uhrzeit des letzten Kopiervorgangs auf den sekundären Server|  
|**last_copied_date_utc**|**datetime**|Datum und Uhrzeit des letzten Kopiervorgangs auf den sekundären Server in UTC (Coordinated Universal Time).|  
|**last_restored_file**|**nvarchar(500)**|Der Dateiname der letzten Sicherungsdatei, die in der sekundären Datenbank wiederhergestellt wurde.|  
|**last_restored_date**|**datetime**|Datum und Uhrzeit des letzten Wiederherstellungsvorgangs für die sekundäre Datenbank.|  
|**last_restored_date_utc**|**datetime**|Datum und Uhrzeit des letzten Wiederherstellungsvorgangs auf dem sekundären Server in UTC (Coordinated Universal Time).|  
|**last_restored_latency**|**int**|Der Zeitraum in Minuten zwischen dem Erstellen der Protokollsicherung auf dem primären Server und dem Wiederherstellen auf dem sekundären Server.<br /><br /> Der Anfangswert ist NULL.|  
|**history_retention_period**|**int**|Die Zeitdauer in Minuten, die Verlaufsdatensätze des Protokollversands für eine bestimmte sekundäre Datenbank vor dem Löschen aufbewahrt werden.|  
  
## <a name="remarks"></a>Hinweise  
 Die mit einem sekundären Server verbundenen Informationen werden sowohl auf dem Remoteüberwachungsserver als auch auf dem sekundären Server in der **log_shipping_monitor_secondary** -Tabelle gespeichert.  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Sp_add_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [Sp_change_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [Sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [Sp_help_log_shipping_monitor_secondary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql.md)   
 [Sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

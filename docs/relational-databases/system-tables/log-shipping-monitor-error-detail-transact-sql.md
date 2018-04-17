---
title: Log_shipping_monitor_error_detail (Transact-SQL) | Microsoft Docs
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
- log_shipping_monitor_error_detail_TSQL
- log_shipping_monitor_error_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_error_detail system table
ms.assetid: 0c38a625-60d2-4ee2-bcf3-2ba367914220
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff9a5a08e0b74a4cba9582b49b5224a801209130
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingmonitorerrordetail-transact-sql"></a>log_shipping_monitor_error_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Speichert Fehlerdetails für Protokollversandaufträge. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
 Die verlaufs- und überwachungsverbundenen Tabellen werden auch auf dem primären und dem sekundären Server verwendet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|Die primäre ID für Sicherungsvorgänge oder die sekundäre ID für Kopier- oder Wiederherstellungsvorgänge.|  
|**agent_type**|**tinyint**|Der Typ des Protokollversandauftrags.<br /><br /> 0 = Sicherungsauftrag<br /><br /> 1 = Kopierauftrag<br /><br /> 2 = Wiederherstellungsauftrag|  
|**session_id**|**int**|Die Sitzungs-ID für den Sicherungs-/Kopier-/Wiederherstellungsauftrag|  
|**database_name**|**sysname**|Der Name der diesem Fehlerdatensatz zugeordneten Datenbank. Die primäre Datenbank für Sicherungsaufträge, die sekundäre Datenbank für Wiederherstellungsaufträge oder eine leere Datenbank für Kopieraufträge.|  
|**sequence_number**|**int**|Eine inkrementelle Zahl, die auf die richtige Reihenfolge von Fehlerinformationen hinweist, die mehrere Datensätze umfassen.|  
|**log_time**|**datetime**|Datum und Uhrzeit der Datensatzerstellung|  
|**log_time_utc**|**datetime**|Datum und Uhrzeit der Datensatzerstellung in UTC (Coordinated Universal Time, Koordinierte Weltzeit)|  
|**Nachricht**|**nvarchar**|Meldungstext.|  
|**Quelle**|**nvarchar**|Die Quelle der Fehlermeldung oder des Ereignisses.|  
|**help_url**|**nvarchar**|Die URL (sofern vorhanden), unter der weitere Informationen zum Fehler zur Verfügung stehen.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Tabelle enthält Fehlerdetails für die Protokollversand-Agents. Jeder Fehler wird als eine Sequenz von Ausnahmen protokolliert. Für jede Sitzung eines Agents sind mehrere Fehler (Sequenzen) möglich.  
  
 Die mit dem primären verbundenen Informationen Server werden sowohl auf dem Remoteüberwachungsserver als auch auf dem primären Server in der **log_shipping_monitor_error_detail** -Tabelle gespeichert. Die mit dem sekundären Server verbundenen Informationen werden ebenfalls auf dem sekundären Server in der **log_shipping_monitor_error_detail** -Tabelle gespeichert.  
  
 Zur Identifizierung einer Agentsitzung können Sie die Spalten **agent_id**, **agent_type**und **session_id**verwenden. Sortieren Sie die Spalten nach **log_time** , um die Fehler in der Reihenfolge ihrer Protokollierung anzuzeigen.  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Log_shipping_monitor_history_detail &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)   
 [Sp_cleanup_log_shipping_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [Sp_delete_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [Sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [Sp_refresh_log_shipping_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  

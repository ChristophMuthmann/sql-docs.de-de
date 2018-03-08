---
title: Sys.Traces (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- traces
- sys.traces_TSQL
- sys.traces
- traces_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.traces catalog view
ms.assetid: 4a03be22-b7da-4e2a-97ff-94bed890a620
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a846bac5a610bac22c9b00712df5ea04c2779df1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="systraces-transact-sql"></a>sys.traces (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **sys.traces** -Katalogsicht enthält den aktuellen aktiven ablaufverfolgungen auf dem System. Diese Ansicht dient als Ersatz für die **Fn_trace_getinfo** Funktion.  
  
 Eine vollständige Liste der unterstützten Ablaufverfolgungsereignisse finden Sie unter [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen die Katalogsichten für erweiterte Ereignisse.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Ablaufverfolgungs-ID.|  
|**status**|**int**|Ablaufverfolgungsstatus:<br /><br /> 0 = beendet<br /><br /> 1 = wird ausgeführt|  
|**path**|**nvarchar(260)**|Pfad der Ablaufverfolgungsdatei. Dieser Wert ist NULL, wenn es sich um eine Rowset-Ablaufverfolgung handelt.|  
|**max_size**|**bigint**|Maximale Größe der Ablaufverfolgungsdatei in MB. Dieser Wert ist NULL, wenn es sich um eine Rowset-Ablaufverfolgung handelt.|  
|**stop_time**|**datetime**|Beendigungszeit für die aktive Ablaufverfolgung.|  
|**max_files**|**int**|Maximale Anzahl von Rolloverdateien. Dieser Wert ist NULL, wenn die maximale Anzahl nicht festgelegt wurde.|  
|**is_rowset**|**bit**|1 = Rowset-Ablaufverfolgung.|  
|**is_rollover**|**bit**|1 = Rolloveroption ist aktiviert.|  
|**is_shutdown**|**bit**|1 = Option für das Herunterfahren ist aktiviert.|  
|**is_default**|**bit**|1 = Standardablaufverfolgung.|  
|**buffer_count**|**int**|Anzahl der speicherinternen Puffer, die von der Ablaufverfolgung verwendet werden.|  
|**buffer_size**|**int**|Größe jedes einzelnen Puffers (KB).|  
|**file_position**|**bigint**|Letzte Position in der Ablaufverfolgungsdatei. Dieser Wert ist NULL, wenn es sich um eine Rowset-Ablaufverfolgung handelt.|  
|**reader_spid**|**int**|Sitzungs-ID des Lesers für die Rowset-Ablaufverfolgung. Dieser Wert ist NULL, wenn es sich um eine Dateiablaufverfolgung handelt.|  
|**start_time**|**datetime**|Startzeit der Ablaufverfolgung.|  
|**last_event_time**|**datetime**|Zeitpunkt, an dem das letzte Ereignis ausgelöst wurde.|  
|**event_count**|**bigint**|Gesamtanzahl von eingetretenen Ereignissen.|  
|**dropped_event_count**|**int**|Gesamtanzahl von verworfenen Ereignissen.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.trace_categories &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys.trace_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys.trace_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys.trace_event_bindings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys.trace_subclass_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  

---
title: dm_xe_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xe_sessions_TSQL
- dm_xe_sessions
- sys.dm_xe_sessions_TSQL
- sys.dm_xe_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_sessions dynamic management view
- extended events [SQL Server], views
ms.assetid: defd6efb-9507-4247-a91f-dc6ff5841e17
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9198b8ac568f33591ee934458dbd1a58c2e71cbe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmxesessions-transact-sql"></a>sys.dm_xe_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über eine aktive Sitzung mit erweiterten Ereignissen zurück. Diese Sitzung ist eine Auflistung von Ereignissen, Aktionen und Zielen.  
    
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|address|**varbinary(8)**|Die Speicheradresse der Sitzung. Adresse ist dem lokalen System eindeutig. Lässt keine NULL-Werte zu.|  
|name|**nvarchar(256)**|Der Name der Sitzung. Name ist im lokalen System eindeutig. Lässt keine NULL-Werte zu.|  
|pending_buffers|**int**|Die Anzahl der vollen Puffer, deren Verarbeitung noch aussteht. Lässt keine NULL-Werte zu.|  
|total_regular_buffers|**int**|Die Gesamtzahl regulärer Puffer, die der Sitzung zugeordnet sind. Lässt keine NULL-Werte zu.<br /><br /> Hinweis: in den meisten Fällen werden reguläre Puffer verwendet werden. Die Größe dieser Puffer ist ausreichend für zahlreiche Ereignisse. Normalerweise gibt es mindestens drei Puffer pro Sitzung. Die Anzahl der regulären Puffer wird vom Server auf Grundlage der Arbeitsspeicherpartitionierung automatisch bestimmt, die durch die MEMORY_PARTITION_MODE-Option festgelegt wird. Die Größe der regulären Puffer ist gleich dem Wert der MAX_MEMORY-Option (4 MB in der Standardeinstellung) dividiert durch die Anzahl der Puffer. Weitere Informationen zur MEMORY_PARTITION_MODE-Option und zur MAX_MEMORY-Option finden Sie unter [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).|  
|regular_buffer_size|**bigint**|Die Größe des regulären Puffers in Bytes. Lässt keine NULL-Werte zu.|  
|total_large_buffers|**int**|Die Gesamtzahl großer Puffer. Lässt keine NULL-Werte zu.<br /><br /> Hinweis: Große Puffer werden verwendet, wenn ein Ereignis eines regulären Puffers überschreitet. Sie werden explizit für diesen Zweck reserviert. Große Puffer werden reserviert, wenn die Ereignissitzung startet, und werden anhand der MAX_EVENT_SIZE-Option skaliert. Weitere Informationen zur MAX_EVENT_SIZE-Option finden Sie unter [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).|  
|large_buffer_size|**bigint**|Die Größe des großen Puffers in Bytes. Lässt keine NULL-Werte zu.|  
|total_buffer_size|**bigint**|Die Gesamtgröße des Arbeitsspeicherpuffers, der zum Speichern von Ereignissen für die Sitzung verwendet wird, in Bytes. Lässt keine NULL-Werte zu.|  
|buffer_policy_flags|**int**|Eine Bitmap, die angibt, wie sich Sitzungsereignispuffer verhalten, wenn alle Puffer voll sind und ein neues Ereignis ausgelöst wird. Lässt keine NULL-Werte zu.|  
|buffer_policy_desc|**nvarchar(256)**|Eine Beschreibung des Verhaltens von Sitzungsereignispuffern, wenn alle Puffer voll sind und ein neues Ereignis ausgelöst wird.  Lässt keine NULL-Werte zu. Buffer_policy_desc kann einen der folgenden sein:<br /><br /> Ereignis löschen<br /><br /> Ereignisse nicht löschen<br /><br /> Vollen Puffer löschen<br /><br /> Neuen Puffer reservieren|  
|flags|**int**|Eine Bitmap, die die Flags angibt, die für die Sitzung festgelegt wurden. Lässt keine NULL-Werte zu.|  
|flag_desc|**nvarchar(256)**|Eine Beschreibung der Flags, die für die Sitzung festgelegt sind.  Lässt keine NULL-Werte zu. Flag_desc kann eine beliebige Kombination der folgenden sein:<br /><br /> Puffer beim Schließen leeren<br /><br /> Dedizierter Verteiler<br /><br /> Rekursive Ereignisse zulassen|  
|dropped_event_count|**int**|Die Anzahl der Ereignisse, die bei gefüllten Puffern gelöscht wurden. Dieser Wert ist **0** , wenn die Pufferrichtlinie "Vollen Puffer löschen" oder "Ereignisse nicht löschen" ist. Lässt keine NULL-Werte zu.|  
|dropped_buffer_count|**int**|Die Anzahl der Puffer, die gelöscht wurden, als die Puffer gefüllt waren. Dieser Wert ist **0** , wenn die Pufferrichtlinie auf "Ereignis löschen" oder "Ereignisse nicht löschen" festgelegt ist. Lässt keine NULL-Werte zu.|  
|blocked_event_fire_time|**int**|Die Dauer, für die das Auslösen von Ereignissen verhindert wurde, als die Puffer gefüllt waren. Dieser Wert ist **0** , wenn die Pufferrichtlinie "Vollen Puffer löschen" oder "Ereignis löschen" ist. Lässt keine NULL-Werte zu.|  
|create_time|**datetime**|Die Uhrzeit, zu der die Sitzung erstellt wurde. Lässt keine NULL-Werte zu.|  
|largest_event_dropped_size|**int**|Die Größe des größten Ereignisses, das nicht in den Sitzungspuffer gepasst hat. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Korrigiert den Datentyp für den Namen und den Blocked_event_fire_time-Spalten.|  
|Entfernt die Buffer_size und Total_buffers Spalten an.|  
|Die Spalten Total_regular_buffers, Regular_buffer_size, Total_large_buffers, Large_buffer_size und Total_buffer_size wird hinzugefügt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  


---
title: Sys. dm_exec_session_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_session_wait_stats
- sys.dm_exec_session_wait_stats_tsql
- dm_exec_session_wait_stats
- dm_exec_session_wait_stats_tsql
helpviewer_keywords: sys.dm_exec_session_wait_stats
ms.assetid: df84842a-71eb-4fda-b448-5953cf9985dc
caps.latest.revision: "6"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0eb49558894d39d6aaf89332b75656446675ecd3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecsessionwaitstats-transact-sql"></a>Sys. dm_exec_session_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu allen Wartevorgängen in Threads, die für jede Sitzung ausgeführt. Verwenden Sie diese Ansicht Diagnostizierung von Leistungsproblemen mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sitzung sowie bei bestimmten Abfragen und Batches.  Diese Sicht gibt dieselbe Informationen, die aggregiert werden, für die Sitzung zurück [dm_os_wait_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) bietet jedoch die **Session_id** auch Anzahl.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Die Id der Sitzung.|  
|wait_type|**nvarchar(60)**|Name des Wartetyps. Weitere Informationen finden Sie unter [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|waiting_tasks_count|**bigint**|Anzahl von Wartevorgängen für diesen Wartetyp. Dieser Leistungsindikator wird beim Starten eines Wartevorgangs inkrementiert.|  
|wait_time_ms|**bigint**|Gesamtwartezeit für diesen Wartetyp (in Millisekunden). Diese Zeit beinhaltet signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Maximale Wartezeit für diesen Wartetyp.|  
|signal_wait_time_ms|**bigint**|Differenz zwischen dem Zeitpunkt der Signalisierung des wartenden Threads und dem Beginn der Ausführung.|  
  
## <a name="remarks"></a>Hinweise  
 Diese DMV setzt die Informationen für eine Sitzung aus, wenn die Sitzung geöffnet wird, oder wenn die Sitzung zurückgesetzt wird (wenn Verbindungspooling),  
  
 Informationen über die Wartetypen finden Sie unter [dm_os_wait_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Wenn der Benutzer hat **VIEW SERVER STATE** Berechtigung auf dem Server, sieht der Benutzer alle zurzeit ausgeführten Sitzungen für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist, andernfalls der Benutzer sieht nur die aktuelle Sitzung.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
 

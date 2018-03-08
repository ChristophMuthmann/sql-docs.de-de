---
title: Sys.dm_pdw_errors (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4131409826a4c5dd602a4638c688c9682a1e97d2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwerrors-transact-sql"></a>sys.dm_pdw_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu Fehlern während der Ausführung einer Anforderung oder einer Abfrage.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|Der Schlüssel für diese Ansicht.<br /><br /> Eindeutige numerische Id des Fehlers.|Für alle Abfragefehlern im System eindeutig.|  
|Quelle|**nvarchar(64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|Typ|**nvarchar(4000)**|Fehlertyp, der aufgetreten ist.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|Der Zeitpunkt, an dem der Fehler aufgetreten ist.|Kleiner oder gleich der aktuellen Zeit.|  
|pwd_node_id|**int**|Bezeichner, der den bestimmten Knoten erfolgt, sofern vorhanden. Weitere Informationen zu Knoten-Ids finden Sie unter [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).||  
|session_id|**nvarchar(32)**|Der Bezeichner der Sitzung beteiligt sind, sofern vorhanden. Weitere Informationen auf der Sitzungs-Ids finden Sie unter [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|request_id|**nvarchar(32)**|Der Bezeichner der Anforderung beteiligt sind, sofern vorhanden. Zusätzliche Informationen für Anforderung-Ids finden Sie unter [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).||  
|spid|**int**|SPID der SQL Server-Sitzung beteiligt sind, sofern vorhanden.||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Details|**nvarchar(4000)**|Enthält den vollständigen Text fehlerbeschreibung.||  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie im Abschnitt "maximale Systemwerte anzeigen" in der [Mindest- und Höchstwerte (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) Thema.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

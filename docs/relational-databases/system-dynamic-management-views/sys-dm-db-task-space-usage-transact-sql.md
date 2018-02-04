---
title: Sys. dm_db_task_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_task_space_usage_TSQL
- sys.dm_db_task_space_usage_TSQL
- dm_db_task_space_usage
- sys.dm_db_task_space_usage
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_task_space_usage dynamic management view
ms.assetid: fb0c87e5-43b9-466a-a8df-11b3851dc6d0
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a10c12a2510baaace72219803e9f3cc26bebf20
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbtaskspaceusage-transact-sql"></a>sys.dm_db_task_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt für die Datenbank Aktivitäten zu Seitenzuordnungen und aufgehobenen Seitenzuordnungen nach Tasks zurück.  
  
> [!NOTE]  
>  In dieser Ansicht gilt nur für die [Tempdb-Datenbank](../../relational-databases/databases/tempdb-database.md).  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_db_task_space_usage**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|Sitzungs-ID.|  
|**request_id**|**int**|Anforderungs-ID innerhalb der Sitzung.<br /><br /> Eine Anforderung wird auch als Batch bezeichnet und enthält mindestens eine Abfrage. Für eine Sitzung können mehrere Anforderungen gleichzeitig aktiviert sein. Jede Abfrage der Anforderung kann mehrere Threads (Tasks) starten, falls ein paralleler Ausführungsplan verwendet wird.|  
|**exec_context_id**|**int**|Ausführungskontext-ID des Tasks. Weitere Informationen finden Sie unter [dm_os_tasks &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md).|  
|**database_id**|**smallint**|Datenbank-ID|  
|**user_objects_alloc_page_count**|**bigint**|Anzahl von Seiten, die von diesem Task für Benutzerobjekte reserviert oder zugeordnet werden.|  
|**user_objects_dealloc_page_count**|**bigint**|Anzahl von Seiten, deren Zuordnung von diesem Task für Benutzerobjekte aufgehoben wird und die nicht mehr reserviert sind.|  
|**internal_objects_alloc_page_count**|**bigint**|Anzahl von Seiten, die von diesem Task für interne Objekte reserviert oder zugeordnet werden.|  
|**internal_objects_dealloc_page_count**|**bigint**|Anzahl von Seiten, deren Zuordnung von diesem Task für interne Objekte aufgehoben wird und die nicht mehr reserviert sind.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="remarks"></a>Hinweise  
 IAM-Seiten werden nicht in die von dieser Sicht gemeldete Seitenanzahl einbezogen.  
  
 Seitenzähler werden zu Beginn einer Anforderung mit null (0) initialisiert. Diese Werte werden auf der Sitzungsebene aggregiert, wenn die Anforderung abgeschlossen ist. Weitere Informationen finden Sie unter [Sys. dm_db_session_space_usage &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md).  
  
 Das Zwischenspeichern von Arbeitstabellen bzw. temporären Tabellen sowie verzögerte Löschvorgänge beeinflussen die Anzahl von Seiten, die für einen angegebenen Task zugeordnet werden bzw. deren Zuordnung aufgehoben wird.  
  
## <a name="user-objects"></a>Benutzerobjekte  
 Die folgenden Objekte sind in den Seitenindikatoren für Benutzerobjekte enthalten:  
  
-   Benutzerdefinierte Tabellen und Indizes  
  
-   Systemtabellen und -indizes  
  
-   Globale temporäre Tabellen und Indizes  
  
-   Lokale temporäre Tabellen und Indizes  
  
-   Tabellenvariablen  
  
-   In Tabellenwertfunktionen zurückgegebene Tabellen  
  
## <a name="internal-objects"></a>Interne Objekte  
 Interne Objekte gibt es nur in **Tempdb**. Die folgenden Objekte sind in den Seitenzählern für interne Objekte enthalten:  
  
-   Arbeitstabellen für Cursor- oder Spoolvorgänge und die Speicherung temporärer LOBs (Large Object)  
  
-   Arbeitsdateien für Vorgänge wie Hashjoins  
  
-   Sortierläufe  
  
## <a name="physical-joins"></a>Physische Joins  
 ![Physische Joins für Sys. dm_db_session_task_usage](../../relational-databases/system-dynamic-management-views/media/join-dm-db-task-space-usage-1.gif "physische joins für Sys. dm_db_session_task_usage")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|dm_db_task_space_usage.request_id|dm_exec_requests.request_id|1:1|  
|dm_db_task_space_usage.session_id|dm_exec_requests.session_id|1:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_os_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  



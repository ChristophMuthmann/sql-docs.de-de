---
title: sys.dm_exec_query_memory_grants (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_query_memory_grants_TSQL
- sys.dm_exec_query_memory_grants
- sys.dm_exec_query_memory_grants_TSQL
- dm_exec_query_memory_grants
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_memory_grants dynamic management view
ms.assetid: 2c417747-2edd-4e0d-8a9c-e5f445985c1a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 92b11100a0a037374871dc38844fecc8b69b0c72
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecquerymemorygrants-transact-sql"></a>sys.dm_exec_query_memory_grants (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu allen Abfragen, die angefordert haben und auf eine arbeitsspeicherzuweisung warten oder eine arbeitsspeicherzuweisung erhalten haben. Abfragen, die nicht auf eine arbeitsspeicherzuweisung erforderlich ist, werden in dieser Ansicht nicht angezeigt. Z. B. Sortierung und Hash Join-Vorgängen über arbeitsspeicherzuweisungen für die abfrageausführung, während Abfragen ohne eine **ORDER BY** Klausel keinen Speicher zu gewähren.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert. Darüber hinaus werden die Werte in den Spalten **Scheduler_id**, **Wait_order**, **Pool_id**, **Group_id** gefiltert; der Spaltenwert wird festgelegt. auf NULL.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_exec_query_memory_grants**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|ID (SPID) der Sitzung, in der die Abfrage ausgeführt wird.|  
|**request_id**|**int**|ID der Anforderung. Ist im Kontext der Sitzung eindeutig.|  
|**scheduler_id**|**int**|ID des Zeitplanungsmoduls, der diese Abfrage plant.|  
|**dop**|**smallint**|Grad an Parallelität für diese Abfrage.|  
|**request_time**|**datetime**|Datum und Uhrzeit, zu der die Abfrage die Arbeitsspeicherzuweisung angefordert hat.|  
|**grant_time**|**datetime**|Datum und Uhrzeit, zu der die Arbeitsspeicherzuweisung für die Abfrage erfolgt ist. NULL, wenn noch kein Arbeitsspeicher zugewiesen wurde.|  
|**requested_memory_kb**|**bigint**|Insgesamt angeforderter Arbeitsspeicher in Kilobytes.|  
|**granted_memory_kb**|**bigint**|Insgesamt tatsächlich zugewiesener Arbeitsspeicher in Kilobytes. Kann NULL sein, wenn noch kein Arbeitsspeicher zugewiesen wurde. Für eine typische Situation dieser Wert sollte identisch sein **Requested_memory_kb**. Für die Indexerstellung wird möglicherweise vom Server bei Bedarf weiterer Arbeitsspeicher über den ursprünglich zugewiesenen hinaus zugelassen.|  
|**required_memory_kb**|**bigint**|Minimaler Arbeitsspeicher in Kilobyte, der erforderlich ist, um diese Abfrage auszuführen. **Requested_memory_kb** entspricht oder diesen übersteigt.|  
|**used_memory_kb**|**bigint**|Der zu diesem Zeitpunkt verwendete physische Arbeitsspeicher in Kilobytes.|  
|**max_used_memory_kb**|**bigint**|Der bis zu diesem Zeitpunkt verwendete maximale physische Arbeitsspeicher in Kilobytes.|  
|**query_cost**|**float**|Die geschätzten Abfragekosten.|  
|**timeout_sec**|**int**|Timeout in Sekunden, nach dem die Abfrage die Anforderung der Arbeitsspeicherzuweisung aufgibt.|  
|**resource_semaphore_id**|**smallint**|Nicht eindeutige ID des Ressourcensemaphors, auf das die Abfrage wartet.<br /><br /> **Hinweis:** diese ID ist in Versionen von eindeutig [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die älter sind als [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Diese Änderung kann die Abfrageausführung bei der Problembehandlung beeinflussen. Weitere Informationen finden Sie im Abschnitt "Hinweise" weiter unten in diesem Thema.|  
|**queue_id**|**smallint**|ID der Warteschlange, in der die Abfrage auf Arbeitsspeicherzuweisungen wartet. NULL, wenn der Arbeitsspeicher bereits zugewiesen wurde.|  
|**wait_order**|**int**|Sequenzielle Position wartender Abfragen in der angegebenen **Queue_id**. Der Wert kann sich für eine Abfrage ändern, wenn andere Abfragen Arbeitsspeicherzuweisungen erhalten oder für diese ein Timeout eintritt. NULL, wenn bereits Arbeitsspeicher zugewiesen wurde.|  
|**is_next_candidate**|**bit**|Kandidat für die nächste Arbeitsspeicherzuweisung.<br /><br /> 1 = Ja<br /><br /> 0 = Nein<br /><br /> NULL = Arbeitsspeicher wurde bereits zugewiesen|  
|**wait_time_ms**|**bigint**|Wartezeit in Millisekunden. NULL, wenn der Arbeitsspeicher bereits zugewiesen wurde.|  
|**plan_handle**|**varbinary(64)**|Bezeichner für diesen Abfrageplan. Verwendung **dm_exec_query_plan** um den tatsächlichen XML-Plan zu extrahieren.|  
|**sql_handle**|**varbinary(64)**|Bezeichner für den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Text dieser Abfrage. Verwendung **Sys. dm_exec_sql_text** den tatsächlichen abzurufenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Text.|  
|**group_id**|**int**|ID für die Arbeitsauslastungsgruppe, in der diese Abfrage ausgeführt wird.|  
|**pool_id**|**int**|ID des Ressourcenpools, zu dem die Arbeitsauslastungsgruppe gehört.|  
|**is_small**|**tinyint**|Der Wert 1 gibt an, dass diese Zuweisung das kleine Ressourcensemaphor verwendet. Der Wert 0 gibt an, dass ein normales Semaphor verwendet wird.|  
|**ideal_memory_kb**|**bigint**|Größe der Arbeitsspeicherzuweisung in Kilobyte (KB), um alles in den physischen Speicher aufzunehmen. Dieser Wert basiert auf der Kardinalitätsschätzung.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  
  
## <a name="remarks"></a>Hinweise  
 Ein typisches Debugszenario für ein Abfragetimeout sieht folgendermaßen aus:  
  
-   Überprüfen Sie die gesamte Arbeitsspeicherstatus im Gesamtsystem mithilfe [dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md), [Sys. dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md), und verschiedenen Leistungsindikatoren.  
  
-   Überprüfen Sie für die Ausführung der Abfrage arbeitsspeicherreservierungen in **dm_os_memory_clerks** , in denen `type = 'MEMORYCLERK_SQLQERESERVATIONS'`.  
  
-   Überprüfen Sie für Abfragen mit Zuweisungen warten **dm_exec_query_memory_grants**.  
  
    ```  
    --Find all queries waiting in the memory queue  
    SELECT * FROM sys.dm_exec_query_memory_grants where grant_time is null  
    ```  
  
-   Suchen von Cache für Abfragen mit arbeitsspeicherzuweisungen, die mit[dm_exec_cached_plans &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) und [dm_exec_query_plan &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
    ```  
    -- retrieve every query plan from the plan cache  
    USE master;  
    GO  
    SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
    GO  
  
    ```  
  
-   Untersuchen Sie arbeitsspeicherintensive Abfragen mithilfe [Sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).  
  
    ```  
    --Find top 5 queries by average CPU time  
    SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    Plan_handle, query_plan   
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
    ORDER BY total_worker_time/execution_count DESC;  
    GO  
  
    ```  
  
-   Untersuchen Sie eine endlosabfrage den Showplan in [dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) und den Batchtext aus [Sys. dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 Abfragen mithilfe dynamischer Verwaltungssichten, die ORDER BY oder Aggregate enthalten, können die Arbeitsspeichernutzung erhöhen und so zu dem Problem beitragen, das mit ihnen behandelt werden soll.  
  
 Mit der Ressourcenkontrollen-Funktion kann ein Datenbankadministrator Serverressourcen auf Ressourcenpools verteilen, bis zu maximal 64 Pools. Beginnend mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], jeder Pool verhält sich wie eine kleine unabhängige Serverinstanz und erfordert 2 Semaphore. Die Anzahl von zurückgegebenen Zeilen **dm_exec_query_resource_semaphores** können nicht mit bis zu 20-Mal länger als die im zurückgegebenen Zeilen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. dm_exec_query_resource_semaphores &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql.md)   
 [Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



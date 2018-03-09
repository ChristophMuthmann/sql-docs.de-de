---
title: dm_exec_cached_plans (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/18/2017
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
- sys.dm_exec_cached_plans
- dm_exec_cached_plans
- dm_exec_cached_plans_TSQL
- sys.dm_exec_cached_plans_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plans dynamic management view
ms.assetid: 95b707d3-3a93-407f-8e88-4515d4f2039d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5bdddde1f7aedfc2aa576d5745df9d0f601c868f
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="sysdmexeccachedplans-transact-sql"></a>sys.dm_exec_cached_plans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jeden Abfrageplan zurück, der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für eine schnellere Abfrageausführung zwischengespeichert wird. In dieser dynamischen Verwaltungssicht können Sie zwischengespeicherte Abfragepläne, zwischengespeicherten Abfragetext, den von zwischengespeicherten Plänen verwendeten Arbeitsspeicher und die Anzahl der Wiederverwendungen für zwischengespeicherte Pläne suchen.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert. Darüber hinaus werden die Werte in den Spalten **Memory_object_address** und **Pool_id** gefiltert; der Spaltenwert auf NULL festgelegt ist.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_exec_cached_plans**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|bucketid|**int**|ID des Hashbuckets, in dem der Eintrag gespeichert ist. Der Wert gibt einen Bereich von 0 bis zur Hashtabellengröße für den Typ des Caches an.<br /><br /> Für die SQL-Plan- und Objektplancaches kann die Hashtabellengröße in 32-Bit-Systemen bis zu 10007 und in 64-Bit-Systemen bis zu 40009 betragen. Für den Cache für gebundene Strukturen kann die Hashtabellengröße in 32-Bit-Systemen bis zu 1009 und in 64-Bit-Systemen bis zu 4001 betragen. Für den Cache für erweiterte gespeicherte Prozeduren kann die Hashtabellengröße in 32-Bit-Systemen und 64-Bit-Systemen bis zu 127 betragen.|  
|refcounts|**int**|Anzahl der Cacheobjekte, die auf dieses Cacheobjekt verweisen. **RefCounts** muss mindestens 1 sein für einen Eintrag im Cache befinden.|  
|usecounts|**int**|Häufigkeit, mit der das Cacheobjekt nachgeschlagen wurde. Nicht inkrementiert, wenn parametrisierte Abfragen einen Plan im Cache suchen. Kann bei Verwenden von Showplan mehrmals inkrementiert werden.|  
|size_in_bytes|**int**|Anzahl von Bytes, die vom Cacheobjekt belegt werden.|  
|memory_object_address|**varbinary(8)**|Speicheradresse des zwischengespeicherten Eintrags. Dieser Wert kann verwendet werden, mit [dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) zum Abrufen der arbeitsspeicheraufteilung des zwischengespeicherten Plans und mit [Sys. dm_os_memory_cache_entries](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md), um die Kosten für das Zwischenspeichern des Eintrags abzurufen.|  
|cacheobjtype|**nvarchar(34)**|Typ des Objekts im Cache. Die folgenden Werte sind möglich:<br /><br /> Kompilierter Plan<br /><br /> Stub des kompilierten Plans<br /><br /> Analysestruktur<br /><br /> Erweiterte Prozedur<br /><br /> Kompilierte CLR-Funktion<br /><br /> Kompilierte CLR-Prozedur|  
|objtype|**nvarchar(16)**|Typ des Objekts. Im folgenden sind die möglichen Werte und deren entsprechenden Beschreibungen.<br /><br /> Prozedur: Gespeicherte<br />Vorbereitet wird: Vorbereitete Anweisung<br />Ad-hoc-: Ad-hoc-Abfrage. Bezieht sich auf [!INCLUDE[tsql](../../includes/tsql-md.md)] als Sprachereignisse mithilfe von übermittelt **Osql** oder **Sqlcmd** anstatt als Remoteprozeduraufrufe.<br />ReplProc:--Replikationsfilterprozedur<br />Trigger: Trigger<br />Ansicht: Ansicht<br />Standard: Standard<br />UsrTab: Benutzertabelle<br />SysTab:-Systemtabelle<br />Überprüfung: CHECK-Einschränkung<br />Regel: Regel|  
|plan_handle|**varbinary(64)**|Bezeichner für den speicherinternen Plan. Dieser Bezeichner ist vorübergehend und bleibt nur für die Dauer der Speicherung des Plans im Cache konstant. Dieser Wert kann mit den folgenden dynamischen Verwaltungsfunktionen verwendet werden:<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|  
|pool_id|**int**|Die ID des Ressourcenpools, auf die sich diese Planspeicherauslastung bezieht.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
 <sup>1</sup>  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-batch-text-of-cached-entries-that-are-reused"></a>A. Zurückgeben des Batchtexts von zwischengespeicherten Einträgen, die wiederverwendet werden  
 Im folgenden Beispiel wird der SQL-Text aller zwischengespeicherten Einträge zurückgegeben, die mehr als einmal verwendet wurden.  
  
```  
SELECT usecounts, cacheobjtype, objtype, text   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
WHERE usecounts > 1   
ORDER BY usecounts DESC;  
GO  
```  
  
### <a name="b-returning-query-plans-for-all-cached-triggers"></a>B. Zurückgeben von Abfrageplänen für alle zwischengespeicherten Trigger  
 Im folgenden Beispiel werden die Abfragepläne für alle zwischengespeicherten Trigger zurückgegeben.  
  
```  
SELECT plan_handle, query_plan, objtype   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_query_plan(plan_handle)   
WHERE objtype ='Trigger';  
GO  
```  
  
### <a name="c-returning-the-set-options-with-which-the-plan-was-compiled"></a>C. Zurückgeben der SET-Optionen, mit denen der Plan kompiliert wurde  
 Im folgenden Beispiel werden die SET-Optionen zurückgegeben, mit denen der Plan kompiliert wurde. Die `sql_handle` für der Plan wird ebenfalls zurückgegeben. Der PIVOT-Operator wird verwendet, in die Ausgabe der `set_options` und `sql_handle` Attribute, die als Spalten und nicht als Zeilen. Weitere Informationen zu den zurückgegebenen Wert `set_options`, finden Sie unter [dm_exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md).  
  
```  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
      SELECT plan_handle, epa.attribute, epa.value   
      FROM sys.dm_exec_cached_plans   
      OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
      WHERE cacheobjtype = 'Compiled Plan'  
      ) AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
### <a name="d-returning-the-memory-breakdown-of-all-cached-compiled-plans"></a>D. Zurückgeben der Arbeitsspeicheraufteilung aller zwischengespeicherter kompilierter Pläne  
 Im folgenden Beispiel wird die Aufteilung des Arbeitsspeichers zurückgegeben, der von allen kompilierten Plänen im Zwischenspeicher verwendet wird.  
  
```  
SELECT plan_handle, ecp.memory_object_address AS CompiledPlan_MemoryObject,   
    omo.memory_object_address, type, page_size_in_bytes   
FROM sys.dm_exec_cached_plans AS ecp   
JOIN sys.dm_os_memory_objects AS omo   
    ON ecp.memory_object_address = omo.memory_object_address   
    OR ecp.memory_object_address = omo.parent_address  
WHERE cacheobjtype = 'Compiled Plan';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)   
 [sys.dm_os_memory_cache_entries &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  



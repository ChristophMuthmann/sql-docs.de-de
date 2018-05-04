---
title: Sys. dm_exec_sql_text (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_sql_text
- sys.dm_exec_sql_text
- sys.dm_exec_sql_text_TSQL
- dm_exec_sql_text_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sql_text dynamic management function
ms.assetid: 61b8ad6a-bf80-490c-92db-58dfdff22a24
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0252d77f6d27134ba291c7e67e926e640eba9a9c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecsqltext-transact-sql"></a>sys.dm_exec_sql_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den Text der SQL-batch, identifiziert durch das angegebene *Sql_handle*. Diese Tabellenwertfunktion ersetzt die Systemfunktion **Fn_get_sql**.  
  
 
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_exec_sql_text(sql_handle | plan_handle)  
```  
  
## <a name="arguments"></a>Argumente  
*sql_handle*  
Das SQL-Handle für den zu suchenden Batch. *Sql_handle* ist **varbinary(64)**. *Sql_handle* kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
  
-   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
  
-   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  
  
*plan_handle*  
Identifiziert eindeutig einen Abfrageplan für einen Batch, der zwischengespeichert ist oder gerade ausgeführt wird. *plan_handle* ist **varbinary(64)** *plan_handle* kann von den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
-   [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|ID der Datenbank.<br /><br /> Für Ad-hoc-Anweisungen und vorbereitete SQL-Anweisungen, die ID der Datenbank, in der die Anweisungen kompiliert wurden.|  
|**objectid**|**int**|ID des Objekts.<br /><br /> Dieser Wert ist für Ad-hoc-Anweisungen und vorbereitete SQL-Anweisungen NULL.|  
|**number**|**smallint**|Für eine nummerierte gespeicherte Prozedur gibt diese Spalte die Nummer der gespeicherten Prozedur zurück. Weitere Informationen finden Sie unter [numbered_procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md).<br /><br /> Dieser Wert ist für Ad-hoc-Anweisungen und vorbereitete SQL-Anweisungen NULL.|  
|**encrypted**|**bit**|1 = Der SQL-Text ist verschlüsselt.<br /><br /> 0 = Der SQL-Text ist nicht verschlüsselt.|  
|**text**|**Nvarchar (Max** **)**|Text der SQL-Abfrage.<br /><br /> Der Wert ist für verschlüsselte Objekte NULL.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW SERVER STATE`-Berechtigung auf dem Server.  
  
## <a name="remarks"></a>Hinweise  
Für ad-hoc-Abfragen die SQL-Handles sind Hashwerte basierend auf den SQL-Text an den Server gesendet wird, und können aus einer beliebigen Datenbank stammen. 

Für Datenbankobjekte, z. B. gespeicherte Prozeduren, Trigger oder Funktionen, werden die SQL-Handles von der Datenbank-ID, Objekt-ID und Objektnummer abgeleitet. 

Planhandle ist ein Hashwert aus dem kompilierten Plan des gesamten Batchs abgeleitet. 

> [!NOTE]
> **DBID** kann nicht bestimmt werden, von *Sql_handle* für ad-hoc-Abfragen. Um zu bestimmen, **Dbid** für ad-hoc-Abfragen verwenden *Plan_handle* stattdessen.
  
## <a name="examples"></a>Beispiele 

### <a name="a-conceptual-example"></a>A. Konzeptionelle-Beispiel
Folgender Ausdruck ist ein einfaches Beispiel zur Veranschaulichung der Übergabe einer **Sql_handle** entweder direkt oder über **CROSS APPLY**.
  1.  Erstellen Sie die Aktivität.  
Führen Sie die folgende T-SQL in ein neues Abfragefenster im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].   
      ```sql
      -- Identify current spid (session_id)
      SELECT @@SPID;
      GO
  
      -- Create activity
        WAITFOR DELAY '00:02:00';
      ```
      
    2.  Mit **CROSS APPLY**.  
    Sql_handle von **Sys. dm_exec_requests** übergeben werden, um **Sys. dm_exec_sql_text** mit **CROSS APPLY**. Öffnen Sie ein neues Abfragefenster, und übergeben Sie die Spid, die in Schritt 1 identifiziert. In diesem Beispiel wird die Spid entspricht `59`.

        ```sql
        SELECT t.*
        FROM sys.dm_exec_requests AS r
        CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t
        WHERE session_id = 59 -- modify this value with your actual spid
         ```      
 
    2.  Übergeben von **Sql_handle** direkt.  
Abrufen der **Sql_handle** aus **Sys. dm_exec_requests**. Übergeben Sie dann die **Sql_handle** direkt zu **Sys. dm_exec_sql_text**. Öffnen Sie ein neues Abfragefenster, und übergeben Sie die Spid, die in Schritt 1 identifizierten **Sys. dm_exec_requests**. In diesem Beispiel wird die Spid entspricht `59`. Übergeben Sie das zurückgegebene **Sql_handle** als Argument an **Sys. dm_exec_sql_text**.

        ```sql
        -- acquire sql_handle
        SELECT sql_handle FROM sys.dm_exec_requests WHERE session_id = 59  -- modify this value with your actual spid
        
        -- pass sql_handle to sys.dm_exec_sql_text
        SELECT * FROM sys.dm_exec_sql_text(0x01000600B74C2A1300D2582A2100000000000000000000000000000000000000000000000000000000000000) -- modify this value with your actual sql_handle
         ```      
    
  
### <a name="b-obtain-information-about-the-top-five-queries-by-average-cpu-time"></a>B. Abrufen von Informationen zu den fünf Abfragen mit der höchsten durchschnittlichen CPU-Zeit  
 Im folgenden Beispiel wird der Text der SQL-Anweisung und die durchschnittliche CPU-Zeit für die fünf Abfragen mit der höchsten durchschnittlichen CPU-Zeit zurückgegeben.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    SUBSTRING(st.text, (qs.statement_start_offset/2)+1,   
        ((CASE qs.statement_end_offset  
          WHEN -1 THEN DATALENGTH(st.text)  
         ELSE qs.statement_end_offset  
         END - qs.statement_start_offset)/2) + 1) AS statement_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
ORDER BY total_worker_time/execution_count DESC;  
```  
  
### <a name="c-provide-batch-execution-statistics"></a>C. Geben Sie die Batchausführung Statistiken  
 Im folgenden Beispiel wird der Text von SQL-Abfragen zurückgegeben, die in Batches ausgeführt werden. Außerdem werden statistische Informationen zu den Abfragen bereitgestellt.  
  
```sql  
SELECT s2.dbid,   
    s1.sql_handle,    
    (SELECT TOP 1 SUBSTRING(s2.text,statement_start_offset / 2+1 ,   
      ( (CASE WHEN statement_end_offset = -1   
         THEN (LEN(CONVERT(nvarchar(max),s2.text)) * 2)   
         ELSE statement_end_offset END)  - statement_start_offset) / 2+1))  AS sql_statement,  
    execution_count,   
    plan_generation_num,   
    last_execution_time,     
    total_worker_time,   
    last_worker_time,   
    min_worker_time,   
    max_worker_time,  
    total_physical_reads,   
    last_physical_reads,   
    min_physical_reads,    
    max_physical_reads,    
    total_logical_writes,   
    last_logical_writes,   
    min_logical_writes,   
    max_logical_writes    
FROM sys.dm_exec_query_stats AS s1   
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS s2    
WHERE s2.objectid is null   
ORDER BY s1.sql_handle, s1.statement_start_offset, s1.statement_end_offset;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_cursors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)   
 [sys.dm_exec_xml_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)   
 [dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [Verwenden von APPLY](../../t-sql/queries/from-transact-sql.md#using-apply)   
 [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  


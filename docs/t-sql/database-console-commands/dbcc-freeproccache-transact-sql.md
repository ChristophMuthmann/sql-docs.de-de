---
title: DBCC FREEPROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREEPROCCACHE_TSQL
- FREEPROCCACHE
- DBCC_FREEPROCCACHE_TSQL
- DBCC FREEPROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- freeing procedure cache
- removing procedure cache elements
- deleting procedure cache elements
- DBCC FREEPROCCACHE statement
- procedure cache [SQL Server]
- clearing procedure cache
ms.assetid: 0e09d210-6f23-4129-aedb-3d56b2980683
caps.latest.revision: 61
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bda4cf8c1859d011e0a320887fd8a9cc53d8cea0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-freeproccache-transact-sql"></a>DBCC FREEPROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Entfernt alle Elemente aus dem Plancache, entfernt einen bestimmten Plan aus dem Plancache durch Angabe eines Planhandles oder SQL-Handles oder entfernt alle einem angegebenen Ressourcenpool zugeordneten Cacheinträge.

>[!NOTE]
>Die Ausführungsstatistik für systemintern kompilierte gespeicherte Prozeduren wird durch DBCC FREEPROCCACHE nicht gelöscht. Der Prozedurcache enthält keine Informationen zu systemintern kompilierten gespeicherten Prozeduren. Jede Ausführungsstatistik, die Prozedur erfasst wird in die Ausführungsstatistik DMVs angezeigt: [Sys. dm_exec_procedure_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) und [dm_exec_query_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
Die Syntax für SQLServer:

```sql
DBCC FREEPROCCACHE [ ( { plan_handle | sql_handle | pool_name } ) ] [ WITH NO_INFOMSGS ]  
```  

Die Syntax für Azure SQL Datawarehouse und Parallel Datawarehouse:
  
```sql
DBCC FREEPROCCACHE [ ( COMPUTE | ALL ) ] 
     [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 ({ *Plan_handle* | *Sql_handle* | *Pool_name* })  
 *Plan_handle* identifiziert eindeutig einen Abfrageplan für einen Batch, die ausgeführt wurde, dessen Plan sich im Plancache befindet. *Plan_handle* ist **varbinary(64)** und kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
 -   [dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
 -   [Sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
 -   [Sys. dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  

 *Sql_handle* ist der SQL-Handle der zu löschenden Batch. *Sql_handle* ist **varbinary(64)** und kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
 -   [Sys. dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
 -   [Sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
 -   [dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
 -   [dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  

 *Pool_name* ist der Name eines Ressourcenpools der Ressourcenkontrolle. *Pool_name* ist **Sysname** und abgerufen werden können, indem Sie Abfragen der [dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) -verwaltungssicht.  
 Um einen Ressourcenpool eine Arbeitsauslastungsgruppe der Ressourcenkontrolle zuzuordnen, Fragen Sie die [dm_resource_governor_workload_groups](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) -verwaltungssicht. Informationen über die Arbeitsauslastungsgruppe für eine Sitzung durch Abfragen der [Sys. dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) -verwaltungssicht.  

  
 WITH NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
 COMPUTE  
 Löschen Sie von jeder Serverknoten Abfrageplancache befinden. Dies ist der Standardwert.  
  
 ALL  
 Löschen Sie auf jedem Knoten der COMPUTE- und aus dem Knoten "Zugriffssteuerung" Abfrageplancache befinden.  
  
## <a name="remarks"></a>Hinweise  
Verwenden Sie DBCC FREEPROCCACHE, um den Plancache sorgfältig zu leeren. Durch das Leeren des Plancaches wird beispielsweise eine gespeicherte Prozedur erneut kompiliert, statt aus dem Cache erneut verwendet zu werden. 

Dies kann einen plötzlichen, vorübergehenden Abfall der Abfrageleistung verursachen. Für jeden geleerten Cachespeicher im Plancache die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll enthält die folgende Meldung zur Information: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurden %d Leerungen des Cachespeichers für die '%s'-Cachespeicher (Bestandteil des Plancache) aufgrund von ' DBCC FREEPROCCACHE' oder 'DBCC FREESYSTEMCACHE'-Vorgängen. " Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.

Der Prozedurcache wird außerdem durch die folgenden Neukonfigurierungsvorgänge gelöscht:
-   access check cache bucket count  
-   access check cache quota  
-   clr enabled  
-   cost threshold for parallelism  
-   cross db ownership chaining  
-   index create memory  
-   max degree of parallelism  
-   Max. Serverarbeitspeicher  
-   max text repl size  
-   max worker threads  
-   Min. Arbeitsspeicher pro Abfrage  
-   Min. Serverarbeitsspeicher  
-   query governor cost limit  
-   query wait  
-   remote query timeout  
-   user options  
  
## <a name="result-sets"></a>Resultsets  
Wenn die WITH NO_INFOMSGS-Klausel nicht angegeben ist, gibt DBCC FREEPROCCACHE zurück: "DBCC-Ausführung wurde abgeschlossen. Falls DBCC Fehlermeldungen ausgegeben hat, wenden Sie sich an den Systemadministrator."
  
## <a name="permissions"></a>Berechtigungen  
Gilt für: SQLServer, Parallel Datawarehouse 

- Erfordert die ALTER SERVER STATE-Berechtigung auf dem Server.  

Gilt für: Azure SQL Data Warehouse
- Erfordert die Mitgliedschaft in der festen Serverrolle "DB_OWNER".  

## <a name="general-remarks-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Allgemeine Hinweise für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC FREEPROCCACHE Befehlsfolge können gleichzeitig ausgeführt werden.
In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], deaktivieren den Abfrageplancache kann eine temporäre Verringerung der abfrageleistung verursachen, wenn Sie Abfragen neu kompiliert wurden. 

DBCC FREEPROCCACHE (RECHENLOGIK) nur bewirkt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abfragen neu kompiliert, wenn sie auf den Serverknoten ausgeführt werden. Er führt nicht dazu, dass [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] So kompilieren Sie den parallelen Abfrageplan, der generiert wird, auf den Knoten "Zugriffssteuerung".
DBCC FREEPROCCACHE kann während der Ausführung abgebrochen werden.
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Einschränkungen für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC FREEPROCCACHE kann nicht innerhalb einer Transaktion ausgeführt.
DBCC FREEPROCCAHCE wird in einer EXPLAIN-Anweisung nicht unterstützt.
  
## <a name="metadata-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Metadaten für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Die Systemsicht sys.pdw_exec_requests wird eine neue Zeile hinzugefügt, wenn DBCC FREEPROCCACHE ausgeführt wird.
  
## <a name="examples-includessnoversionincludesssnoversion-mdmd"></a>Beispiele:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
### <a name="a-clearing-a-query-plan-from-the-plan-cache"></a>A. Löschen eines Abfrageplans im Plancache  
Im folgenden Beispiel wird ein Abfrageplan im Plancache gelöscht, indem das Abfrageplanhandle angegeben wird. Um sicherzustellen, dass die Beispielabfrage im Plancache vorhanden ist, wird die Abfrage zuerst ausgeführt. Die `sys.dm`_`exec` \_ `cached_plans` und `sys.dm` \_ `exec` \_ `sql` \_ `text` dynamische Verwaltungssichten werden abgefragt, um das Zurückgeben der Das planhandle für die Abfrage. 

Der Planhandlewert aus dem Resultset wird dann in die `DBCC FREEPROCACHE`-Anweisung eingefügt, sodass nur dieser Plan aus dem Plancache entfernt wird.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM Person.Address;  
GO  
SELECT plan_handle, st.text  
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st  
WHERE text LIKE N'SELECT * FROM Person.Address%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

{!!! Mispalced Text? !!!}
 `plan_handle                                         text`  
  
 `--------------------------------------------------  -----------------------------`  
  
 `0x060006001ECA270EC0215D05000000000000000000000000  SELECT * FROM Person.Address;`  
  
 `(1 row(s) affected)`  
{End Misplaed Text bitten}
  
```sql  
-- Remove the specific plan from the cache.  
DBCC FREEPROCCACHE (0x060006001ECA270EC0215D05000000000000000000000000);  
GO  
```  
  
### <a name="b-clearing-all-plans-from-the-plan-cache"></a>B. Löschen aller Pläne im Plancache  
Im folgenden Beispiel werden alle Elemente im Plancache gelöscht. Die WITH `NO_INFOMSGS` -Klausel angegeben ist, um zu verhindern, dass die Meldung angezeigt wird.
  
```sql  
DBCC FREEPROCCACHE WITH NO_INFOMSGS;  
```  
  
### <a name="c-clearing-all-cache-entries-associated-with-a-resource-pool"></a>C. Löschen aller einem Ressourcenpool zugeordneten Cacheeinträge  
Im folgenden Beispiel werden alle einem angegebenen Ressourcenpool zugeordneten Cacheeinträge gelöscht. Die `sys.dm_resource_governor_resource_pools` Ansicht wird zuerst abgefragt, um Abrufen des Werts für *Pool_name*.
  
```sql  
SELECT * FROM sys.dm_resource_governor_resource_pools;  
GO  
DBCC FREEPROCCACHE ('default');  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-dbcc-freeproccache-basic-syntax-examples"></a>D. Beispiele für DBCC FREEPROCCACHE die grundlegende Syntax  
Im folgende Beispiel entfernt alle vorhandenen Caches für die Abfrage-Plan von den Computeknoten. Obwohl der Kontext auf UserDbSales festgelegt ist, werden die Compute-Knoten Abfrage Plan Caches für alle Datenbanken entfernt werden wird. Die WITH NO_INFOMSGS-Klausel wird verhindert, dass informationsmeldungen in die Ergebnisse angezeigt werden.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE) WITH NO_INFOMSGS;  
```  
  
 Das folgende Beispiel enthält die gleichen Ergebnisse wie im vorherigen Beispiel, außer dass informationsmeldungen in die Ergebnisse angezeigt werden.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE);  
```  
  
Wenn informationsmeldungen angefordert werden, und die Ausführung erfolgreich ist, müssen die Ergebnisse der Abfrage eine Zeile pro Compute-Knoten.
  
### <a name="e-granting-permission-to-run-dbcc-freeproccache"></a>E. Erteilen von Berechtigungen zum Ausführen von DBCC FREEPROCCACHE  
Im folgenden Beispiel wird die Anmeldung David Berechtigung zum Ausführen von DBCC FREEPROCCACHE.  
  
```sql
GRANT ALTER SERVER STATE TO David;  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)
  
  


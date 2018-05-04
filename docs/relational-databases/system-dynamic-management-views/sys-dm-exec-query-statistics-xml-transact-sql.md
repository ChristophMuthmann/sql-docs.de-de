---
title: sys.dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
caps.latest.revision: 6
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: f52c0a1a39d3c8ab56241644e4c8e4d42c9d0af7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Gibt Abfragen Ausführungsplan für in-Flight-Anforderungen. Verwenden Sie diese DMV, um Showplan XML vorübergehenden Statistiken abzurufen. 

## <a name="syntax"></a>Syntax

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>Argumente 
*session_id*  
 Die Sitzungs-Id wird den Batch gesucht werden soll ausgeführt werden. *Session_id* ist **"smallint"**. *Session_id* kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>Zurückgegebene Tabelle
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|ID der Sitzung. Lässt keine NULL-Werte zu.|
|request_id|**int**|ID der Anforderung. Lässt keine NULL-Werte zu.|
|sql_handle|**varbinary(64)**|Hashzuordnung des SQL-Text der Anforderung. NULL-Werte sind zulässig.|
|plan_handle|**varbinary(64)**|Hashzuordnung des Abfrageplans. NULL-Werte sind zulässig.|
|query_plan|**xml**|Showplan XML mit partiellen Statistiken. NULL-Werte sind zulässig.|

## <a name="remarks"></a>Hinweise
Mit dieser Systemfunktion steht ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1.

Mit dieser Systemfunktion funktioniert unter beiden **standard** und **einfache** abfrageausführungsstatistik Infrastruktur profilerstellung.  
  
**Standard** Infrastruktur profilerstellung Statistiken können mit aktiviert werden:
  -  [SET STATISTICS XML AUF](../../t-sql/statements/set-statistics-xml-transact-sql.md)
  -  [SET STATISTICS PROFILE AUF](../../t-sql/statements/set-statistics-profile-transact-sql.md)
  -  die `query_post_execution_showplan` erweiterte Ereignisse.  
  
**Lightweight** Statistiken Infrastruktur profilerstellung steht in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 und [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und kann aktiviert werden:
  -  Global mithilfe von Trace flag 7412.
  -  Mithilfe der [ *Query_thread_profile* ](http://support.microsoft.com/kb/3170113) erweiterte Ereignisse.
  
> [!NOTE]
> Nach der Aktivierung von Ablaufverfolgungsflag 7412 einfache profilerstellung aktiviert, um jeder Consumer der Infrastruktur statt standard Profil, z. B. die DMV profilerstellung abfrageausführungsstatistik [dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md).
> Standard-profilerstellung wird jedoch immer noch verwendet für SET STATISTICS XML *Istplan enthalten* Aktion in [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], und `query_post_execution_showplan` xEvent.

> [!IMPORTANT]
> In TPC C wie Arbeitslast Tests fügt das einfache statistikinfrastruktur profilerstellung aktivieren ein 1,5 bis 2 Prozent Mehraufwand aus. Im Gegensatz dazu kann die standardmäßigen Profilerstellungsdaten statistikinfrastruktur bis zu 90 Prozent Mehraufwand für das gleiche arbeitsauslastungsszenario hinzufügen.

## <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW SERVER STATE`-Berechtigung auf dem Server.  

## <a name="examples"></a>Beispiele  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. Ansehen von Abfrageplan und Ausführungskontext Statistiken zu aktiven Abfragen für einen ausgeführten batch  
 Die folgende Beispielabfrage **Sys. dm_exec_requests** finden Sie interessante Abfrage- und kopieren die `session_id` aus der Ausgabe.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Klicken Sie dann, um den Abfrageplan und Ausführungskontext Statistiken zu aktiven Abfragen zu erhalten, verwenden den kopierten `session_id` mit der Systemfunktion **sys.dm_exec_query_statistics_xml**.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 Oder für alle ausgeführten Anforderungen kombiniert.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>Siehe auch
  [Ablaufverfolgungsflags](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  


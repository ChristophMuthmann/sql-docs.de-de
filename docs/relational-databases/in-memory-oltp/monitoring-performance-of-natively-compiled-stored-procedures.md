---
title: "Überwachen der Leistung von systemintern kompilierten gespeicherten Prozeduren | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8db102af60a736dd0e971a1799508188a8332dc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>Überwachen der Leistung von systemintern kompilierten gespeicherten Prozeduren
  In diesem Thema wird erläutert, wie Sie die Leistung von systemintern kompilierten gespeicherten Prozeduren überwachen können.  
  
## <a name="using-extended-events"></a>Unter Verwendung erweiterter Ereignisse  
 Verwenden Sie das erweiterte Ereignis **sp_statement_completed** , um die Ausführung einer Abfrage zu verfolgen. Erstellen Sie eine Sitzung für erweiterte Ereignisse mit diesem Ereignis. Optional können Sie für eine bestimmte systemintern kompilierte gespeicherte Prozedur nach object_id filtern. Das erweiterte Ereignis wird nach der Ausführung jeder Abfrage ausgelöst. Die vom erweiterten Ereignis angegebene CPU-Zeit und Dauer geben an, wie lange die CPU genutzt und wie lange die Abfrage ausgeführt wurde. Bei einer systemintern kompilierten gespeicherten Prozedur, die viel CPU-Zeit beansprucht, treten u. U. Leistungsprobleme auf.  
  
 Neben**line_number**kann auch **object_id** im erweiterten Ereignis verwendet werden, um die Abfrage zu untersuchen. Mithilfe der folgenden Abfrage kann die Prozedurdefinition abgerufen werden. Anhand der Zeilennummer wird die Abfrage innerhalb der Definition identifiziert:  
  
```tsql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 Weitere Informationen zum erweiterten Ereignis **sp_statement_completed** finden Sie unter [Abrufen der Anweisung, durch die ein Ereignis ausgelöst wurde](http://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx).  
  
## <a name="using-data-management-views"></a>Unter Verwendung von Datenverwaltungssichten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt Ausführungsstatistiken für systemintern kompilierte gespeicherte Prozeduren sowohl auf Prozedur- als auch auf Abfrageebene. Das Sammeln statistischer Ausführungsdaten ist aufgrund der Leistungsauswirkungen standardmäßig nicht aktiviert.  
  
 Die Statistiksammlung für systemintern kompilierte gespeicherte Prozeduren kann mit [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) aktiviert und deaktiviert werden.  
  
 Wenn die Erfassung von Statistiken mit [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) aktiviert ist, können Sie [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) verwenden, um die Leistung einer nativ kompilierten gespeicherten Prozedur zu überwachen.  
  
 Wenn die Erfassung von Statistiken mit [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) aktiviert ist, können Sie [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) verwenden, um die Leistung einer nativ kompilierten gespeicherten Prozedur zu überwachen.  
  
 Zu Beginn aktivieren Sie die Statistiksammlung. Anschließend führen Sie die systemintern kompilierte gespeicherte Prozedur aus. Am Ende deaktivieren Sie die Statistiksammlung. Anschließend analysieren Sie die von den DMVs zurückgegebene Ausführungsstatistik.  
  
 Nachdem die Statistiksammlung abgeschlossen wurde, können die Ausführungsstatistiken zu nativ kompilierten gespeicherten Prozeduren mit [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) für eine Prozedur und für Abfragen mit [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) abgefragt werden.  
  
> [!NOTE]  
>  Wenn die Statistiksammlung für systemintern kompilierte gespeicherte Prozeduren aktiviert ist, wird worker_time in Millisekunden erfasst. Wird die Abfrage in weniger als einer Millisekunde ausgeführt, lautet der Wert 0. Wenn zahlreiche Ausführungen weniger als 1 Millisekunde dauern, wird **total_worker_time** bei nativ kompilierten gespeicherten Prozeduren u.U. nicht exakt angegeben.  
  
 Mit der folgenden Abfrage werden nach der Statistiksammlung die Prozedurnamen und Ausführungsstatistiken für systemintern kompilierte gespeicherte Prozeduren in der aktuellen Datenbank zurückgegeben:  
  
```tsql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 Mit der folgenden Abfrage werden der Abfragetext und Ausführungsstatistiken für alle Abfragen in systemintern kompilierten gespeicherten Prozeduren der aktuellen Datenbank zurückgegeben, für die statistische Daten gesammelt wurden. Die Ergebnisse sind nach total_worker_time in absteigender Reihenfolge sortiert:  
  
```tsql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  
  
 Systemintern kompilierte gespeicherte Prozeduren unterstützen SHOWPLAN_XML (geschätzter Ausführungsplan). Der geschätzte Ausführungsplan kann verwendet werden, um den Abfrageplan auf Planungsfehler zu überprüfen. Häufige Gründe für fehlerhafte Pläne sind:  
  
-   Statistiken wurden vor der Erstellung der Prozedur nicht aktualisiert.  
  
-   Fehlende Indizes  
  
 Um Showplan XML abzurufen, führen Sie folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code aus:  
  
```tsql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 Alternativ können Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Prozedurnamen auswählen und auf **Geschätzten Ausführungsplan anzeigen**klicken.  
  
 Im geschätzten Ausführungsplan für systemintern kompilierte gespeicherte Prozeduren werden die Abfrageoperatoren und Ausdrücke für die Abfragen der Prozedur angezeigt. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] unterstützt nicht alle SHOWPLAN_XML-Attribute für systemintern kompilierte gespeicherte Prozeduren. Attribute in Zusammenhang mit Kostenberechnungen des Abfrageoptimierers sind nicht Teil der SHOWPLAN_XML für die Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [Systemintern kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  

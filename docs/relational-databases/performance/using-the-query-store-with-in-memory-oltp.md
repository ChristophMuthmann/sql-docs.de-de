---
title: Verwenden des Abfragespeichers mit In-Memory OLTP | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 03/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store, in-memory
ms.assetid: aae5ae6d-7c90-4661-a1c5-df704319888a
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 31483a4450089f194241f19df0bd0072b5026375
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="using-the-query-store-with-in-memory-oltp"></a>Verwenden des Abfragespeichers mit In-Memory-OLTP
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abfragespeicher ermöglicht Ihnen das Überwachen der Leistung nativ kompilierten Codes für In-Memory-OLTP-Arbeitsauslastungen.  
Kompilier- und Laufzeitstatistiken werden auf dieselbe Weise wie bei datenträgerbasierten Arbeitsauslastungen erfasst und verfügbar gemacht.   
Bei der Migration zu In-Memory-OLTP können Sie weiterhin Abfragespeichersichten in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sowie benutzerdefinierte Skripts verwenden, die Sie vor der Migration für datenträgerbasierte Arbeitsauslastungen entwickelt haben. Dadurch war der Aufwand zum Erlernen der Abfragespeichertechnologien nicht vergebens, da Sie Ihr erlerntes Wissen zusätzlich auf die allgemeine Problembehandlung aller Arbeitsauslastungstypen anwenden können.  
Allgemeine Informationen zum Verwenden des Abfragespeichers finden Sie unter [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
 Das Verwenden des Abfragespeichers mit In-Memory-OLTP erfordert keine weitere Funktionskonfiguration. Wenn Sie ihn auf Ihrer Datenbank aktivieren, funktioniert er für alle Arbeitsauslastungstypen.   
Es gibt jedoch einige Aspekte, die Benutzer bei der Verwendung des Abfragespeichers mit In-Memory-OLTP beachten sollten:  
  
-   Wenn der Abfragespeicher aktiviert ist, werden Abfragen, Pläne und Kompilierzeitstatistiken standardmäßig erfasst. Die Erfassung von Laufzeitstatistiken ist jedoch nicht aktiviert, sofern Sie diese nicht explizit mit [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) aktivieren.  
  
-   Wenn Sie *@new_collection_value* auf 0 festlegen, erfasst der Abfragespeicher keine Laufzeitstatistiken mehr für die betroffene Prozedur oder für die gesamte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz.  
  
-   Der mit [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) konfigurierte Wert wird nicht beibehalten. Stellen Sie nach dem Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sicher, dass Sie die Statistikerfassung erneut überprüfen und konfigurieren.  
  
-   Wie bei der regulären Statistikerfassung verringert sich die Leistung möglicherweise, wenn Sie den Abfragespeicher zum Nachverfolgen der Arbeitsauslastungsausführung verwenden. Möglicherweise möchten Sie in Betracht ziehen, die Statistikerfassung nur für eine wichtige Teilmenge nativ kompilierter gespeicherter Prozeduren zu aktivieren.  
  
-   Abfragen und Pläne werden auf der ersten nativen Kompilierung erfasst und gespeichert und bei jeder Neukompilierung aktualisiert.  
  
-   Wenn Sie den Abfragespeicher aktiviert oder dessen Inhalt gelöscht haben, nachdem alle nativen gespeicherten Prozeduren kompiliert wurden, müssen Sie diese manuell erneut kompilieren, damit sie vom Abfragespeicher erfasst werden. Das Gleiche gilt, wenn Sie Abfragen manuell mit [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md) oder [sp_query_store_remove_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md) entfernt haben. Verwenden Sie [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md), um die Neukompilierung der Prozedur zu erzwingen.  
  
-   Der Abfragespeicher nutzt Planerstellungsmechanismen aus In-Memory-OLTP zum Erfassen des Abfrageausführungsplans während der Kompilierung. Der gespeicherte Plan ist semantisch gleichwertig mit einem Plan, den Sie durch die Verwendung von `SET SHOWPLAN_XML ON` erhalten würden, bis auf einen Unterschied: Im Abfragespeicher werden Pläne geteilt und für jede einzelne Anweisung gespeichert.  
    
-   Wenn Sie den Abfragespeicher in einer Datenbank mit gemischten Arbeitsauslastungen ausführen, können Sie von der nativen Kompilierung des Codes generierte Abfragepläne mithilfe des Felds **is_natively_compiled** in [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) schnell finden.  
  
-   Der Abfragespeicher-Erfassungsmodus (*QUERY_CAPTURE_MODE*-Parameter in der **ALTER TABLE**-Anweisung) beeinflusst keine Abfragen von nativ kompilierten Modulen, da diese unabhängig vom konfigurierten Wert immer erfasst werden. Dies beinhaltet das Festlegen von `QUERY_CAPTURE_MODE = NONE`.  
  
-   Die durch den Abfragespeicher erfasste Dauer der Abfragekompilierung enthält nur die Zeit, die für die Optimierung von Abfragen vor dem Generieren des nativen Codes verwendet wurde. Genauer gesagt umfasst es nicht die Zeit für die C-Code-Kompilierung und -Generierung interner Datenstrukturen, die für die Generierung von C-Code erforderlich sind.  
  
-   Speicherzuweisungsmetriken in [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md) werden für nativ kompilierte Abfragen nicht aufgefüllt; ihre Werte sind immer 0. Die Speicherzuweisungsspalten sind die folgenden: avg_query_max_used_memory, last_query_max_used_memory, min_query_max_used_memory, max_query_max_used_memory und stdev_query_max_used_memory.  
  
## <a name="enabling-and-using-query-store-with-in-memory-oltp"></a>Aktivieren und Verwenden des Abfragespeichers mit In-Memory-OLTP  
 Das folgende einfache Beispiel veranschaulicht die Verwendung des Abfragespeichers mit In-Memory-OLTP in einem End-to-End-Benutzerszenario. In diesem Beispiel wird davon ausgegangen, dass für In-Memory-OLTP eine Datenbank (`MemoryOLTP`) aktiviert ist.  
    Weitere Informationen zu den Voraussetzungen für speicheroptimierte Tabellen finden Sie unter [Erstellen einer speicheroptimierten Tabelle und einer nativ kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
```  
USE MemoryOLTP;  
GO  
  
-- Create a simple memory-optimized table   
CREATE TABLE dbo.Ord  
   (OrdNo INTEGER not null PRIMARY KEY NONCLUSTERED,   
    OrdDate DATETIME not null,   
    CustCode NVARCHAR(5) not null)   
WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
-- Enable Query Store before native module compilation  
ALTER DATABASE MemoryOLTP SET QUERY_STORE = ON;  
GO  
  
-- Create natively compiled stored procedure  
CREATE PROCEDURE dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
    BEGIN ATOMIC WITH  
    (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English')  
  
    DECLARE @OrdDate DATETIME = GETDATE();  
    INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)   
        VALUES (@OrdNo, @CustCode, @OrdDate);  
END;  
GO  
  
-- Enable runtime stats collection for queries from dbo.OrderInsert stored procedure  
DECLARE @db_id INT = DB_ID()  
DECLARE @proc_id INT = OBJECT_ID('dbo.OrderInsert');  
DECLARE @collection_enabled BIT;  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
    @database_id = @db_id, @xtp_object_id = @proc_id;  
  
-- Check the state of the collection flag  
EXEC sp_xtp_control_query_exec_stats @database_id = @db_id,   
    @xtp_object_id = @proc_id,   
    @old_collection_value= @collection_enabled output;  
SELECT @collection_enabled AS 'collection status';  
  
-- Execute natively compiled workload  
EXEC dbo.OrderInsert 1, 'A';  
EXEC dbo.OrderInsert 2, 'B';  
EXEC dbo.OrderInsert 3, 'C';  
EXEC dbo.OrderInsert 4, 'D';  
EXEC dbo.OrderInsert 5, 'E';  
  
-- Check Query Store Data  
-- Compile time data  
SELECT q.query_id, plan_id, object_id, query_hash, p.query_plan,  
    p.initial_compile_start_time, p.last_compile_start_time,   
    p.last_execution_time, p.avg_compile_duration,  
    p.last_force_failure_reason, p.force_failure_count  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
  
-- Get runtime stats  
-- Check count_executions field to verify that runtime statistics   
-- have been collected by the Query Store  
SELECT q.query_id, p.plan_id, object_id, rsi.start_time, rsi.end_time,    
    p.last_force_failure_reason, p.force_failure_count, rs.*  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Erstellen einer speicheroptimierten Tabelle und einer nativ kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)   
 [Bewährte Methoden für den Abfragespeicher](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Gespeicherte Prozeduren für den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  


---
title: "&#196;ndern einer vorhandenen Ablaufverfolgung (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ablaufverfolgungen [SQL Server], ändern"
  - "Ändern von Ablaufverfolgungen"
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# &#196;ndern einer vorhandenen Ablaufverfolgung (Transact-SQL)
  In diesem Thema wird beschrieben, wie gespeicherte Prozeduren verwendet werden können, um eine vorhandene Ablaufverfolgung zu ändern.  
  
### So ändern Sie eine vorhandene Ablaufverfolgung  
  
1.  Wenn die Ablaufverfolgung bereits ausgeführt wird, führen Sie **sp_trace_setstatus** mit **@status = 0** aus, um die Ablaufverfolgung zu beenden.  
  
2.  Um Ablaufverfolgungsereignisse zu ändern, führen Sie **sp_trace_setevent** aus, wobei Sie die Änderungen über die Parameter angeben. Der Reihenfolge nach sortiert stehen die folgenden Parameter zur Verfügung:  
  
    -   **@traceid** (Ablaufverfolgungs-ID)  
  
    -   **@eventid** (Ereignis-ID)  
  
    -   **@columnid** (Spalten-ID)  
  
    -   **@on** (ON)  
  
     Beim Ändern des **@on** -Parameters sollten Sie dessen Interaktion mit dem **@columnid** -Parameter beachten:  
  
    |ON|Column ID|Ergebnis|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|Das Ereignis ist aktiviert. Alle Spalten werden gelöscht.|  
    ||NOT NULL|Die Spalte ist für das angegebene Ereignis aktiviert.|  
    |OFF (**0**)|NULL|Das Ereignis ist deaktiviert. Alle Spalten werden gelöscht.|  
    ||NOT NULL|Die Spalte ist für das angegebene Ereignis deaktiviert.|  
  
> [!IMPORTANT]  
>  Im Gegensatz zu regulären gespeicherten Prozeduren werden die Parameter aller gespeicherten Prozeduren von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (**sp_trace_*xx***) streng typisiert, und für sie wird keine automatische Datentypkonvertierung unterstützt. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
## Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren von SQL Server Profiler &#40;SQL Server Profiler&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
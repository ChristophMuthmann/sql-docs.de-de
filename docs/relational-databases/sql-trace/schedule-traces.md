---
title: "Planen von Ablaufverfolgungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Filter [SQL Server], Ereignisse"
  - "Ablaufverfolgungen [SQL Server]"
  - "Ablaufverfolgungen [SQL Server], beenden"
  - "Ereignisse [SQL Server], Filter"
  - "Planen von Ablaufverfolgungen [SQL Server]"
  - "Ablaufverfolgungen [SQL Server], planen"
  - "Beenden von Ablaufverfolgungen"
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Planen von Ablaufverfolgungen
  Es gibt zwei Möglichkeiten, um die Ablaufverfolgung in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu planen. Folgende Aktionen sind möglich:  
  
-   Beendigungszeit für Ablaufverfolgung aktivieren.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent zum Planen einer Ablaufverfolgung verwenden.  
  
## Angeben einer Beendigungszeit  
 Sie können eine Beendigungszeit für die Ablaufverfolgung angeben, wenn Sie gespeicherte Prozeduren von [!INCLUDE[tsql](../../includes/tsql-md.md)] oder [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]verwenden. Die Beendigungszeit muss festgelegt werden, wenn die Ablaufverfolgung konfiguriert wird.  
  
## Planen von Ablaufverfolgungen mithilfe des SQL Server-Agents  
 Die beste Möglichkeit zum Planen von Ablaufverfolgungen ist die Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents, um die Ablaufverfolgung zu starten und dann mit der gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur **sp_trace_setstatus** oder mit dem [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] eine Beendigungszeit für die Ablaufverfolgung anzugeben.  
  
 **So legen Sie einen Beendigungszeitfilter für Ablaufverfolgungen fest**  
  
 [Filtern von Ereignissen anhand der Ereignisendzeit &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## Siehe auch  
 [Automatisierte Administrationstasks &#40;SQL Server Agent&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)  
  
  
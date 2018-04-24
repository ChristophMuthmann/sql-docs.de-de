---
title: Planen von Ablaufverfolgungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: sql-trace
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 18f833b64b24ebcba50003b46f036fdc854235b3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="schedule-traces"></a>Planen von Ablaufverfolgungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Es gibt zwei Möglichkeiten, um die Ablaufverfolgung in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu planen. Folgende Aktionen sind möglich:  
  
-   Beendigungszeit für Ablaufverfolgung aktivieren.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent zum Planen einer Ablaufverfolgung verwenden.  
  
## <a name="specifying-a-stop-time"></a>Angeben einer Beendigungszeit  
 Sie können eine Beendigungszeit für die Ablaufverfolgung angeben, wenn Sie gespeicherte Prozeduren von [!INCLUDE[tsql](../../includes/tsql-md.md)] oder [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]verwenden. Die Beendigungszeit muss festgelegt werden, wenn die Ablaufverfolgung konfiguriert wird.  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>Planen von Ablaufverfolgungen mithilfe des SQL Server-Agents  
 Die beste Möglichkeit zum Planen von Ablaufverfolgungen ist die Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents, um die Ablaufverfolgung zu starten und dann mit der gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Prozedur **sp_trace_setstatus**oder mit dem [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]eine Beendigungszeit für die Ablaufverfolgung anzugeben.  
  
 **So legen Sie einen Beendigungszeitfilter für Ablaufverfolgungen fest**  
  
 [Filtern von Ereignissen anhand der Ereignisendzeit &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Automatisierte Administrationstasks &#40;SQL Server Agent&#41;](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  

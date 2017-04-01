---
title: "MSSQL_ENG014165 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG014165 (Fehler)"
ms.assetid: 7bb07672-310c-4f51-ae76-c55e7c8d51ea
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG014165
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14165|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Stellen Sie sicher, dass der Merge-Agent ausgeführt wird und die erwartete Anforderung erfüllen kann.|  
  
## Erklärung  
 Mit Replikationen können Sie Warnungen für verschiedene Bedingungen aktivieren. Hierzu zählen Fehler beim Verarbeiten einer ausreichenden Anzahl von Zeilen beim Synchronisieren von Änderungen zwischen einem Mergeverleger und einem Mergeabonnenten. Für LAN-Verbindungen und DFÜ-Verbindungen sind möglicherweise unterschiedliche Zeiten angegeben.  
  
 Wenn Sie eine Warnung aktivieren, indem Sie mithilfe des Replikationsmonitors oder [Sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), geben Sie einen Schwellenwert, der bestimmt, wann eine Warnung ausgelöst wird. Wenn dieser Schwellenwert erreicht oder überschritten wird, wird im Replikationsmonitor eine Warnung angezeigt, und es wird ein Ereignis in das Windows-Ereignisprotokoll geschrieben. Durch das Erreichen eines Schwellenwerts kann zudem eine SQL Server-Agent-Warnung ausgelöst werden. Weitere Informationen finden Sie unter [Legen Sie Schwellenwerte und Warnungen im Replikationsmonitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) und [programmgesteuert Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## Benutzeraktion  
 Wenn für ein Abonnement der Schwellenwert für die Zeilenverarbeitung nicht eingehalten wird, müssen Sie ermitteln, ob im System ein Leistungsproblem vorliegt oder ob der Schwellenwert angepasst werden muss. Entwickeln Sie nach dem Konfigurieren der Replikation Grundwerte für die Leistung, mit denen Sie bestimmen können, wie die Replikation sich mit einer Arbeitsauslastung verhält, die typisch für Ihre Anwendungen und Topologie ist. Nehmen Sie die Anzahl der verarbeiteten Zeilen in diese Grundwerte auf, damit Sie einen entsprechenden Schwellenwert festlegen können.  
  
 Wenn der Schwellenwert angemessen ist, jedoch überschritten wird, müssen Sie ermitteln, wo sich der Leistungsengpass im System befindet. Weitere Informationen zum Überwachen der Replikationsleistung und zur entsprechenden Problembehandlung finden Sie in den folgenden Themen:  
  
-   [Überwachen der Leistung mit dem Replikationsmonitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) (insbesondere den Abschnitt "Anzeigen von detaillierten Synchronisierungsleistung für Mergereplikation")  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
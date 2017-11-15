---
title: MSSQL_ENG014162 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG014162 error
ms.assetid: a15eef3f-219f-45d3-8286-6a864c85a723
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64b2c96713d4487c95d69e0d9f463df6383b7fb1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqleng014162"></a>MSSQL_ENG014162
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14162|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Stellen Sie sicher, dass der Merge-Agent ausgeführt wird und die erwartete Anforderung erfüllen kann.|  
  
## <a name="explanation"></a>Erklärung  
 Mit Replikationen können Sie Warnungen für verschiedene Bedingungen aktivieren. Dazu zählt das Überschreiten einer angegebenen Zeitdauer zum Synchronisieren der Änderungen zwischen einem Mergeverleger und -abonnenten. Für LAN-Verbindungen und DFÜ-Verbindungen sind möglicherweise unterschiedliche Zeiten angegeben.  
  
 Wenn Sie mithilfe des Replikationsmonitors oder mit [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)eine Warnung aktivieren, geben Sie einen Schwellenwert an, mit dem bestimmt wird, wann eine Warnung ausgelöst wird. Wenn dieser Schwellenwert erreicht oder überschritten wird, wird im Replikationsmonitor eine Warnung angezeigt, und es wird ein Ereignis in das Windows-Ereignisprotokoll geschrieben. Durch das Erreichen eines Schwellenwerts kann zudem eine SQL Server-Agent-Warnung ausgelöst werden. Weitere Informationen finden Sie unter [Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) und [Programmgesteuertes Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## <a name="user-action"></a>Benutzeraktion  
 Wenn für ein Abonnement der Schwellenwert einer Dauer überschritten wird, müssen Sie ermitteln, ob im System ein Leistungsproblem vorliegt oder ob der Schwellenwert angepasst werden muss. Entwickeln Sie nach dem Konfigurieren der Replikation Grundwerte für die Leistung, mit denen Sie bestimmen können, wie die Replikation sich mit einer Arbeitsauslastung verhält, die typisch für Ihre Anwendungen und Topologie ist. Nehmen Sie die Dauer der Synchronisierung in diese Grundwerte auf, damit Sie einen entsprechenden Schwellenwert festlegen können.  
  
 Wenn der Schwellenwert angemessen ist, jedoch überschritten wird, müssen Sie ermitteln, wo sich der Leistungsengpass im System befindet. Weitere Informationen zum Überwachen der Replikationsleistung und zur entsprechenden Problembehandlung finden Sie in den folgenden Themen:  
  
-   [Überwachen der Leistung mit dem Replikationsmonitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) (insbesondere der Abschnitt „Anzeigen von Details zur Synchronisierungsleistung bei der Mergereplikation“)  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

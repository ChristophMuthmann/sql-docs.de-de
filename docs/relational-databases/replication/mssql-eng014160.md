---
title: "MSSQL_ENG014160 | Microsoft Docs"
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
  - "MSSQL_ENG014160 (Fehler)"
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG014160
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14160|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der Schwellenwert [%s:%s] für die [%s]-Veröffentlichung wurde festgelegt. Mindestens ein Abonnement für diese Veröffentlichung ist abgelaufen.|  
  
## Erklärung  
 Mit Replikationen können Sie Warnungen für verschiedene Bedingungen aktivieren. Dazu zählt das bevorstehende Ablaufdatum des Abonnements. Abonnements können ablaufen, wenn sie nicht innerhalb einer angegebenen *Beibehaltungsdauer*synchronisiert werden. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Wenn Sie eine Warnung aktivieren, indem Sie mithilfe des Replikationsmonitors oder [Sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), geben Sie einen Schwellenwert, der bestimmt, wann eine Warnung ausgelöst wird. Wenn dieser Schwellenwert erreicht oder überschritten wird, wird im Replikationsmonitor eine Warnung angezeigt, und es wird ein Ereignis in das Windows-Ereignisprotokoll geschrieben. Durch das Erreichen eines Schwellenwerts kann zudem eine SQL Server-Agent-Warnung ausgelöst werden. Weitere Informationen finden Sie unter [Legen Sie Schwellenwerte und Warnungen im Replikationsmonitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) und [programmgesteuert Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md).  
  
## Benutzeraktion  
 Die Lösung für dieses Problem hängt von der Ursache für die Auslösung der Warnung ab:  
  
-   Wenn der Schwellenwert überschritten wurde, das Abonnement jedoch noch nicht abgelaufen ist, synchronisieren Sie das Abonnement. Weitere Informationen finden Sie unter [Daten synchronisieren](../../relational-databases/replication/synchronize-data.md).  
  
-   Wenn der Agent ausgeführt wurde, die Änderungen jedoch nicht ordnungsgemäß repliziert wurden, kann das Abonnement aus diesem Grund ablaufen. Stellen Sie für die Transaktionsreplikation sicher, dass der Verteilungs-Agent sowie der Protokolllese-Agent ausgeführt werden. Stellen Sie für die Mergereplikation sicher, dass der Merge-Agent ausgeführt wird. Weitere Informationen zum Starten dieser Agents finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Replikations-Agent ausführbare Konzepte](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Wenn das Abonnement abgelaufen ist, muss es erneut initialisiert werden oder verworfen und neu erstellt werden. Dies richtet sich nach der Art des Abonnements und danach, wie lange es schon abgelaufen war. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
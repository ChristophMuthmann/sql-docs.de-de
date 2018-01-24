---
title: MSSQL_ENG014150 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG014150 error
ms.assetid: c3dd3109-abf3-4b38-a4e9-ef48d0235656
caps.latest.revision: "11"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f55abe74f8e2be5cd829eee53f9a22265f2e8772
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="mssqleng014150"></a>MSSQL_ENG014150
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14150|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Replikations-%1!: %2! (Agent) erfolgreich. %3!|  
  
## <a name="explanation"></a>Erklärung  
 Mit dieser Meldung wird angegeben, dass ein Replikations-Agent erfolgreich zu Ende ausgeführt wurde. Für die Replikation werden die folgenden Agents verwendet:  
  
-   Der Momentaufnahme-Agent. Dieser Agent wird von allen Veröffentlichungen verwendet.  
  
-   Der Protokolllese-Agent. Dieser Agent wird von allen Transaktionsveröffentlichungen verwendet.  
  
-   Der Warteschlangenlese-Agent. Dieser Agent wird von Transaktionsveröffentlichungen verwendet, die für Abonnements mit verzögertem Update über eine Warteschlange aktiviert sind.  
  
-   Der Verteilungs-Agent. Mit diesem Agent werden Abonnements für Transaktions- und Momentaufnahmeveröffentlichungen synchronisiert.  
  
-   Der Merge-Agent. Mit diesem Agent werden Abonnements für Mergeveröffentlichungen synchronisiert.  
  
-   Aufträge zur Replikationswartung.  
  
## <a name="user-action"></a>Benutzeraktion  
 Der Protokolllese-Agent, der Warteschlangenlese-Agent und der Verteilungs-Agent werden normalerweise kontinuierlich ausgeführt. Die anderen Agents werden hingegen bei Bedarf oder nach einem Zeitplan ausgeführt. Wenn Sie nicht erwarten, dass ein Agent zu Ende ausgeführt wurde, überprüfen Sie den Status des Agents. Weitere Informationen finden Sie unter [Monitor Replication Agents](../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replikations-Agentverwaltung](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replikationsverteilungs Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replikationsprotokolllese-Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replikationsmerge-Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Warteschlangenlese-Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  

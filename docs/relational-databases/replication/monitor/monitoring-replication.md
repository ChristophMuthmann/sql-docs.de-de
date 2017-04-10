---
title: "&#220;berwachen (Replikation) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überwachen der Leistung [SQL Server-Replikation], Informationen zum Überwachen der Leistung"
  - "Transaktionsreplikation, Überwachung"
  - "Überwachen [SQL Server-Replikation]"
  - "Überwachen der Mergereplikation [SQL Server-Replikation]"
  - "Momentaufnahmereplikation [SQL Server], überwachen"
  - "Replikation [SQL Server], überwachen"
  - "Verwalten der Replikation, überwachen"
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# &#220;berwachen (Replikation)
  Die Überwachung einer Replikationstopologie ist ein wichtiger Aspekt bei der Bereitstellung der Replikation. Da die Replikationsaktivität verteilt ist, ist es außerordentlich wichtig, die Aktivität und den Status auf allen an der Replikation beteiligten Computern nachzuverfolgen. Zum Überwachen der Replikation stehen die folgenden Tools zur Verfügung:  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikationsmonitor  
  
     Der Replikationsmonitor ist das wichtigste Tool für die Überwachung der Replikation. Es bietet eine verlegerfokussierte Sicht auf die gesamte Replikationsaktivität. Weitere Informationen finden Sie unter [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] bietet Zugriff auf den Replikationsmonitor. Darüber hinaus können Sie sich hier den aktuellen Status und die letzte Meldung anzeigen lassen, die vom Protokolllese-Agent, Momentaufnahme-Agent, Merge-Agent bzw. Verteilungs-Agent protokolliert wurde. Außerdem können Sie hier auch alle diese Agents starten und beenden. Weitere Informationen finden Sie unter [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] und Replication Management Objects (RMO)  
  
     Dank beider Schnittstellen können Sie alle Replikationstypen vom Verteiler aus überwachen. Bei Mergereplikationen haben Sie außerdem die Möglichkeit, die Replikation vom Abonnenten aus zu überwachen.  
  
-   Warnungen für Replikations-Agentereignisse  
  
     Die Replikation bietet eine Reihe vordefinierter Warnungen für Replikations-Agentereignisse. Darüber hinaus können Sie bei Bedarf auch zusätzliche Warnungen erstellen. Warnungen können verwendet werden, um eine automatische Antwort auf ein Ereignis auszulösen und/oder einen Administrator zu benachrichtigen. Weitere Informationen finden Sie unter [mit Warnungen für Replikations-Agent-Ereignisse](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
-   Systemmonitor  
  
     Mit dem Systemmonitor kann die Leistung überwacht werden. Er stellt eine Reihe von Zählern für die Replikation bereit. Weitere Informationen finden Sie unter [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  
## Siehe auch  
 [Verwaltung & #40; Replikation & #41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Bewährte Methoden für die Replikationsverwaltung](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
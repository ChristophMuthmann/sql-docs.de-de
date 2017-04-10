---
title: "Anzeigen von Informationen und Ausf&#252;hren von Aufgaben f&#252;r die einer Ver&#246;ffentlichung zugeordneten Agents (Replikationsmonitor) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agents [SQL Server-Replikation], Anzeigen von Informationen"
  - "Anzeigen von Informationen zum Replikations-Agent"
  - "Agents [SQL Server-Replikation], Tasks im Replikationsmonitor"
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Anzeigen von Informationen und Ausf&#252;hren von Aufgaben f&#252;r die einer Ver&#246;ffentlichung zugeordneten Agents (Replikationsmonitor)
  Der Replikationsmonitor stellt die Registerkarte **Agents** bereit, auf der Informationen zu den Agents enthalten sind, die der ausgewählten Veröffentlichung zugeordnet sind. Der Snapshot-Agent und der Merge-Agent sind Abonnements zugeordnet. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
 Diese Registerkarte enthält Informationen zu folgenden Agents:  
  
-   Momentaufnahme-Agent, der von allen Veröffentlichungen verwendet wird.  
  
-   Protokolllese-Agent, der von allen Transaktionsveröffentlichungen verwendet wird.  
  
-   Warteschlangenlese-Agent, der von Transaktionsveröffentlichungen verwendet wird, die für Abonnements mit verzögertem Update über eine Warteschlange aktiviert wurden.  
  
 Wenn Sie weitere Informationen zu den Optionen dieser Registerkarte erhalten möchten, klicken Sie auf der Menüleiste auf **Hilfe** . Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### So zeigen Sie Informationen für die einer Veröffentlichung zugeordneten Agents an und führen Aufgaben aus  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Agents** , um Informationen zu Agents anzuzeigen. Sie können von dieser Registerkarte aus auch auf detailliertere Informationen zugreifen und Aufgaben ausführen:  
  
    -   Detaillierte Informationen zu einem Agent (z. B. informationsmeldungen und Fehlermeldungen) anzeigen, mit der rechten Maustaste des Agents, und klicken Sie auf **Details zum**.  
  
    -   Um ausführliche Informationen zum Auftrag anzuzeigen, die der Agent (z. B. Zeitplan, Auftragsschrittdetails usw.) ausgeführt wird, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Eigenschaften**.  
  
    -   Um Profile für den Agent zu verwalten, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agentprofil**. Weitere Informationen finden Sie unter [Arbeiten mit Replikations-Agentprofile](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Um einen Agent zu starten, die nicht ausgeführt wird, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agent starten**.  
  
    -   Um einen Agent zu beenden, die ausgeführt wird, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agent beenden**.  
  
## Siehe auch  
 [Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
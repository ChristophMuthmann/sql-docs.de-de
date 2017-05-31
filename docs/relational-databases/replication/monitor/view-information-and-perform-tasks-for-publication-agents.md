---
title: "Anzeigen von Informationen und Ausführen von Aufgaben für Veröffentlichungs-Agents | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d2896e84ecfba28325f559da8e9391315c21046
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="view-information-and-perform-tasks-for-publication-agents"></a>Anzeigen von Informationen und Ausführen von Aufgaben für Veröffentlichungs-Agents
  Der Replikationsmonitor stellt die Registerkarte **Agents** bereit, auf der Informationen zu den Agents enthalten sind, die der ausgewählten Veröffentlichung zugeordnet sind. Weitere Informationen zum Verteilungs-Agent und zum Merge-Agent, die Abonnements zugeordnet sind, finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
 Diese Registerkarte enthält Informationen zu folgenden Agents:  
  
-   Momentaufnahme-Agent, der von allen Veröffentlichungen verwendet wird.  
  
-   Protokolllese-Agent, der von allen Transaktionsveröffentlichungen verwendet wird.  
  
-   Warteschlangenlese-Agent, der von Transaktionsveröffentlichungen verwendet wird, die für Abonnements mit verzögertem Update über eine Warteschlange aktiviert wurden.  
  
 Wenn Sie weitere Informationen zu den Optionen dieser Registerkarte erhalten möchten, klicken Sie auf der Menüleiste auf **Hilfe** . Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>So zeigen Sie Informationen für die einer Veröffentlichung zugeordneten Agents an und führen Aufgaben aus  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Agents** , um Informationen zu Agents anzuzeigen. Sie können von dieser Registerkarte aus auch auf detailliertere Informationen zugreifen und Aufgaben ausführen:  
  
    -   Wenn Sie ausführliche Informationen zu einem Agent (z. B. Informationsmeldungen und Fehlermeldungen) anzeigen möchten, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Details anzeigen**.  
  
    -   Wenn Sie detaillierte Informationen zu dem Auftrag anzeigen möchten, durch den der Agent ausgeführt wird (z. B. Zeitplan, Details zu den Auftragsschritten usw.), klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie anschließend auf **Eigenschaften**.  
  
    -   Wenn Sie die Profile für den Agent verwalten möchten, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Agentprofil**. Weitere Informationen finden Sie unter [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Um einen Agent zu starten, der nicht ausgeführt wird, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Agent starten**.  
  
    -   Um einen Agent zu beenden, der ausgeführt wird, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Agent beenden**.  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  

---
title: "&#220;berwachen der Replikations-Agents | Microsoft Docs"
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
  - "Überwachen der Leistung [SQL Server-Replikation], Agents"
  - "Protokolllese-Agent, Überwachung"
  - "Replikationsmonitor, Agents"
  - "Merge-Agent, Überwachung"
  - "Warteschlangenlese-Agent, Überwachung"
  - "Momentaufnahme-Agent, Überwachung"
  - "Agents [SQL Server-Replikation], Überwachung"
  - "Verteilungs-Agent, Überwachung"
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# &#220;berwachen der Replikations-Agents
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bietet einen systemischen Überblick über die Replikationsaktivität und erleichtert gleichzeitig die Suche nach Informationen zu einem bestimmten Agent. Die folgende Liste enthält alle Agents, die Registerkarten im Replikationsmonitor, auf denen die Agents zu finden sind, und einen Verweis darauf, wo Sie Informationen zum Zugreifen auf die jeweilige Registerkarte finden:  
  
-   Die folgenden Agents sind Veröffentlichungen im Replikationsmonitor zugeordnet:  
  
    -   Momentaufnahme-Agent  
  
    -   Protokolllese-Agent  
  
    -   Warteschlangenlese-Agent  
  
     Zugriff auf Informationen und Aufgaben im Zusammenhang mit diesen Agents kann über die folgenden Registerkarten: **Agents** (verfügbar für jeden Verleger und Veröffentlichung) und **Warnungen** (verfügbar für jede Veröffentlichung). Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Publikation & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   Die folgenden Agents sind Abonnements im Replikationsmonitor zugeordnet:  
  
    -   Verteilungs-Agent  
  
    -   Merge-Agent  
  
     Zugriff auf Informationen und Aufgaben im Zusammenhang mit diesen Agents kann über die folgenden Registerkarten: **Überwachungsliste für Abonnements** (für jeden Verleger verfügbar) oder der **alle Abonnements** (verfügbar für jede Veröffentlichung). Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Überwachen der Replikations-Agents mit SQL Server Management Studio  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] stellt die folgenden Dialogfelder zum Überwachen von Replikations-Agents bereit:  
  
-   **Status des Snapshot-Agents anzeigen** (für alle Veröffentlichungen)  
  
-   **Anzeigen des Status des Protokolllese-Agent** (für alle transaktionsveröffentlichungen)  
  
-   **Synchronisierungsstatus anzeigen** (bei allen Abonnements; dieses Dialogfeld ermöglicht den Zugriff auf den Verteilungs-Agent und der Merge-Agent)  
  
 Der Replikationsmonitor stellt darüber hinaus zusätzliche Informationen zu den einzelnen Agents bereit und bietet außerdem die Möglichkeit der Überwachung des Warteschlangenlese-Agents, sofern dieser verwendet wird. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Publikation & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), [Informationen anzeigen und Ausführen von Aufgaben für eine Veröffentlichung & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), und [Informationen anzeigen und Ausführen von Aufgaben für ein Abonnement & #40; zugeordneten Agents Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
#### So überwachen Sie den Momentaufnahme-Agent und den Protokokolllese-Agent  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Mit der rechten Maustaste einer Veröffentlichung, und klicken Sie dann auf **Log Reader Agent-Anzeigestatus** oder **Snapshot-Agent-Anzeigestatus**.  
  
4.  Führen Sie im Dialogfeld **Status des Protokolllese-Agents anzeigen** bzw. **Status des Momentaufnahme-Agents anzeigen** einen oder mehrere der folgenden Schritte aus:  
  
    -   Zeigen Sie den Agentstatus an.  
  
    -   Starten oder beenden Sie den Agent bei Bedarf.  
  
    -   Klicken Sie auf **Überwachen** , um den **Replikationsmonitor**zu starten.  
  
5.  Klicken Sie auf **Schließen**.  
  
#### So überwachen Sie den Verteilungs-Agent und den Merge-Agent (vom Verleger aus)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** .  
  
3.  Erweitern Sie die Veröffentlichung für das Abonnement, das überwacht werden soll.  
  
4.  Maustaste auf das Abonnement, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
5.  Führen Sie im Dialogfeld **Synchronisierungsstatus anzeigen** einen oder mehrere der folgenden Schritte aus:  
  
    -   Zeigen Sie den Agentstatus an.  
  
    -   Starten oder beenden Sie den Agent bei Bedarf.  
  
    -   Klicken Sie bei Pushabonnements auf **Überwachen** , um den **Replikationsmonitor**zu starten.  
  
    -   Klicken Sie bei Pullabonnements auf **Auftragsverlauf anzeigen** , um den **Protokolldatei-Viewer**zu starten, in dem das Ergebnis aus dem Agentprotokoll angezeigt wird.  
  
6.  Klicken Sie auf **Schließen**.  
  
#### So überwachen Sie den Verteilungs-Agent und den Merge-Agent (vom Abonnenten aus)  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Abonnements** .  
  
3.  Mit der rechten Maustaste des Abonnements zu überwachen, und klicken Sie dann auf **Synchronisierungsstatus anzeigen**.  
  
4.  Führen Sie im Dialogfeld **Synchronisierungsstatus anzeigen** einen oder mehrere der folgenden Schritte aus:  
  
    -   Zeigen Sie den Agentstatus an.  
  
    -   Starten oder beenden Sie den Agent bei Bedarf.  
  
    -   Klicken Sie auf **Auftragsverlauf anzeigen** , um den **Protokolldatei-Viewer**zu starten, in dem das Ergebnis aus dem Agentprotokoll angezeigt wird.  
  
5.  Klicken Sie auf **Schließen**.  
  
## Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Replikations-Agents (Übersicht)](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
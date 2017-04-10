---
title: "Anzeigen von Informationen und Ausf&#252;hren von Aufgaben f&#252;r die einem Abonnement zugeordneten Agents (Replikationsmonitor) | Microsoft Docs"
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
  - "Agents [SQL Server-Replikation], Anzeigen von Informationen"
  - "Anzeigen von Informationen zum Replikations-Agent"
  - "Agents [SQL Server-Replikation], Tasks im Replikationsmonitor"
ms.assetid: fbb59d31-2424-4552-9195-0da8d83e755f
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Anzeigen von Informationen und Ausf&#252;hren von Aufgaben f&#252;r die einem Abonnement zugeordneten Agents (Replikationsmonitor)
  Im Replikationsmonitor gibt es zwei Registerkarten, über die Sie auf Informationen zu den Agents zugreifen können, die dem jeweiligen Abonnement zugeordnet sind:  
  
-   **Alle Abonnements**  
  
     Auf dieser Registerkarte werden Informationen zu allen Abonnements für die ausgewählte Veröffentlichung angezeigt.  
  
-   **Überwachungsliste für Abonnements**  
  
     Auf dieser Registerkarte werden Informationen zu Abonnements von allen auf dem ausgewählten Verleger vorhandenen Veröffentlichungen angezeigt, für die Fehlermeldungen oder Warnungen ausgegeben wurden bzw. bei denen Leistungsprobleme aufgetreten sind. Bei Verteilern, auf denen Versionen vor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ausgeführt werden, wird diese Registerkarte nicht angezeigt.  
  
 Weitere Informationen zu den Optionen der einzelnen Registerkarten finden Sie, wenn Sie auf die Registerkarte im rechten Bereich und dann auf **Hilfe** auf der Menüleiste klicken. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### So können Sie für die einem Abonnement zugeordneten Agents Informationen anzeigen und Aufgaben ausführen (Registerkarte Alle Abonnements)  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** , um sich Informationen zu den Abonnements anzeigen zu lassen. Sie können von dieser Registerkarte aus auch auf detailliertere Informationen zugreifen und Aufgaben ausführen:  
  
    -   Um ausführliche Informationen zu den einem Abonnement zugeordneten Agent anzeigen, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Details zum**. Zu den Detailinformationen gehören: Agentverlauf und Fehlermeldungen, bei der Transaktionsreplikation eine Leistungsstatistik und bei der Mergereplikation eine Synchronisierungsstatistik auf Artikelebene.  
  
         Welche Registerkarten das Detailfenster enthält, hängt von der Art des Abonnements ab: Bei Momentaufnahmeabonnements wird die Registerkarte **Verlauf Verteiler zu Abonnent**angezeigt, bei Transaktionsabonnements enthält das Fenster die Registerkarten **Verlauf Verleger zu Verteiler**, **Verlauf Verteiler zu Abonnent**und **Nicht verteilte Befehle**, und bei Mergeabonnements finden Sie hier die Registerkarte **Synchronisierungsverlauf**.  
  
    -   Um ein Pushabonnement zu synchronisieren, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Synchronisierung starten**.  
  
    -   Um ein Abonnement erneut zu initialisieren, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Abonnement erneut initialisieren**.  
  
    -   Um ein einzelnes Mergeabonnement überprüfen möchten, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Abonnement überprüfen**. Um alle Abonnements für eine Mergeveröffentlichung zu validieren, mit der rechten Maustaste in der Publikation, und klicken Sie dann auf **alle Abonnements überprüfen**um alle Abonnements für eine Transaktionspublikation überprüfen, mit der rechten Maustaste in der Veröffentlichung und klicken Sie dann auf **Abonnements überprüfen**.  
  
    -   Um Profile für den Agent zu verwalten, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agentprofil**. Weitere Informationen finden Sie unter [Arbeiten mit Replikations-Agentprofile](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
### So können Sie für die einem Abonnement zugeordneten Agents Informationen anzeigen und Aufgaben ausführen (Registerkarte Überwachungsliste für Abonnements)  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, und klicken Sie dann auf einen Verleger.  
  
2.  Klicken Sie auf die Registerkarte **Überwachungsliste für Abonnements** , um sich Informationen zu den Abonnements anzeigen zu lassen. Sie können von dieser Registerkarte aus auch auf detailliertere Informationen zugreifen und Aufgaben ausführen:  
  
    -   Um ausführliche Informationen zu den einem Abonnement zugeordneten Agent anzeigen, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Details zum**. Zu den Detailinformationen gehören: Agentverlauf und Fehlermeldungen, bei der Transaktionsreplikation eine Leistungsstatistik und bei der Mergereplikation eine Synchronisierungsstatistik auf Artikelebene.  
  
         Welche Registerkarten das Detailfenster enthält, hängt von der Art des Abonnements ab: Bei Momentaufnahmeabonnements wird die Registerkarte **Verlauf Verteiler zu Abonnent**angezeigt, bei Transaktionsabonnements enthält das Fenster die Registerkarten **Verlauf Verleger zu Verteiler**, **Verlauf Verteiler zu Abonnent**und **Leistung**, und bei Mergeabonnements finden Sie hier die Registerkarte **Synchronisierungsverlauf**.  
  
    -   Um ein Pushabonnement zu synchronisieren, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Synchronisierung starten**.  
  
    -   Um ein Abonnement erneut zu initialisieren, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Abonnement erneut initialisieren**.  
  
    -   Um ein einzelnes Mergeabonnement überprüfen möchten, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Abonnement überprüfen**. Um alle Abonnements für eine Mergeveröffentlichung zu validieren, mit der rechten Maustaste in der Publikation, und klicken Sie dann auf **alle Abonnements überprüfen**um alle Abonnements für eine Transaktionspublikation überprüfen, mit der rechten Maustaste in der Veröffentlichung und klicken Sie dann auf **Abonnements überprüfen**.  
  
    -   Um Profile für den Agent zu verwalten, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agentprofil**. Weitere Informationen finden Sie unter [Arbeiten mit Replikations-Agentprofile](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
## Siehe auch  
 [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
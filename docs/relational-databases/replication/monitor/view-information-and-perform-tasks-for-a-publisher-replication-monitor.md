---
title: "Anzeigen von Informationen und Ausf&#252;hren von Aufgaben f&#252;r einen Verleger (Replikationsmonitor) | Microsoft Docs"
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
  - "Verleger [SQL Server-Replikation], Replikationsmonitortasks"
  - "Anzeigen von Verlegerinformationen"
  - "Verleger [SQL Server-Replikation], Anzeigen von Informationen"
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Anzeigen von Informationen und Ausf&#252;hren von Aufgaben f&#252;r einen Verleger (Replikationsmonitor)
  Der Replikationsmonitor bietet folgende Registerkarten, auf denen Informationen zu dem ausgewählten Verleger angezeigt werden:  
  
-   **Veröffentlichungen**  
  
     Diese Registerkarte enthält Informationen zu allen Veröffentlichungen auf dem ausgewählten Verleger.  
  
-   **Überwachungsliste für Abonnements**  
  
     Auf dieser Registerkarte werden Informationen zu Abonnements von allen auf dem ausgewählten Verleger vorhandenen Veröffentlichungen angezeigt, für die Fehlermeldungen oder Warnungen ausgegeben wurden bzw. bei denen Leistungsprobleme aufgetreten sind. Bei Verteilern, auf denen Versionen vor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ausgeführt werden, wird diese Registerkarte nicht angezeigt.  
  
-   Registerkarte**Agents**   
  
     Diese Registerkarte zeigt ausführliche Informationen zu den Agents und Aufträgen an, die von allen Replikationstypen verwendet werden. Über diese Registerkarte können Sie zudem alle Agents und Aufträge starten und beenden.  
  
 Wenn Sie weitere Informationen zu den Optionen auf den einzelnen Registerkarten anzeigen möchten, klicken Sie im rechten Bereich auf die Registerkarte, und klicken Sie anschließend auf der Menüleiste auf **Hilfe** . Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### So zeigen Sie Informationen für einen Verleger an und führen Aufgaben aus  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, und klicken Sie dann auf einen Verleger.  
  
2.  Um Informationen zu allen Veröffentlichungen anzuzeigen, klicken Sie auf die Registerkarte **Veröffentlichungen** .  
  
3.  Um Informationen zu Abonnements anzuzeigen, klicken Sie auf die Registerkarte **Überwachungsliste für Abonnements** . Über diese Registerkarte können Sie auch auf ausführliche Informationen zugreifen und Aufgaben ausführen:  
  
    -   Um ausführliche Informationen zu den einem Abonnement zugeordneten Agent anzeigen, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Details zum**.  
  
    -   Zum Anzeigen der Eigenschaften eines Abonnements mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Eigenschaften**.  
  
    -   Um ein Pushabonnement zu synchronisieren, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Synchronisierung starten**.  
  
    -   Um ein Abonnement erneut zu initialisieren, mit der rechten Maustaste des Abonnements, und klicken Sie dann auf **Abonnement erneut initialisieren**.  
  
4.  Um Informationen zu Agents anzuzeigen, klicken Sie auf die Registerkarte **Agents** . Sie können von dieser Registerkarte aus auch auf detailliertere Informationen zugreifen und Aufgaben ausführen:  
  
    -   Detaillierte Informationen zu einem Agent (z. B. informationsmeldungen und Fehlermeldungen) anzeigen, mit der rechten Maustaste des Agents, und klicken Sie auf **Details zum**.  
  
    -   Um ausführliche Informationen zum Auftrag anzuzeigen, die der Agent (z. B. Zeitplan, Auftragsschrittdetails usw.) ausgeführt wird, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Eigenschaften**.  
  
    -   Um Profile für den Agent zu verwalten, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agentprofil**. Weitere Informationen finden Sie unter [Arbeiten mit Replikations-Agentprofile](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Um einen Agent zu starten, die nicht ausgeführt wird, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agent starten**.  
  
    -   Um einen Agent zu beenden, die ausgeführt wird, mit der rechten Maustaste des Agents, und klicken Sie dann auf **Agent beenden**.  
  
## Siehe auch  
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
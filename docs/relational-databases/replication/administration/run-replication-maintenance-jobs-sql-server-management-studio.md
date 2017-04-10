---
title: "Ausf&#252;hren von Auftr&#228;gen zur Replikationswartung (SQL Server Management Studio) | Microsoft Docs"
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
  - "Aufträge [SQL Server-Replikation]"
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Ausf&#252;hren von Auftr&#228;gen zur Replikationswartung (SQL Server Management Studio)
  Bei der Replikation werden folgende Wartungsaufträge verwendet:  
  
-   **Abonnements mit Datenüberprüfungsfehlern neu initialisieren**  
  
-   **Agentverlaufscleanup: Verteilung**  
  
-   **Aktualisierung für die Replikationsüberwachung für Verteilung.**  
  
-   **Überprüfung des Replikations-Agents**  
  
-   **Verteilungscleanup: Verteilung**  
  
-   **Cleanup abgelaufener Abonnements**  
  
 Diese Aufträge können über den Ordner **Aufträge** in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] sowie über die Registerkarte **Agents** im Replikationsmonitor gestartet und beendet werden. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md). Anzeigen und Ändern von Eigenschaften für jeden Auftrag in der **Auftragseigenschaften - \< Auftrag>** Dialogfeld, das über den gleichen Ordner und die Registerkarte verfügbar ist.  
  
### So starten Sie einen Auftrag zur Replikationswartung in Management Studio  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Maustaste auf einen Auftrag, und klicken Sie dann auf **Auftrag starten** oder **Auftrag zum Beenden des**.  
  
### So starten Sie einen Auftrag zur Replikationswartung im Replikationsmonitor  
  
1.  Erweitern Sie im Replikationsmonitor eine Verlegergruppe, und wählen Sie dann einen Verleger aus.  
  
2.  Klicken Sie auf die Registerkarte **Agents** .  
  
3.  Mit der rechten Maustaste eines Auftrags im Raster, und klicken Sie dann auf **Auftrag starten** oder **Auftrag zum Beenden des**.  
  
### So zeigen Sie Eigenschaften für einen Auftrag zur Replikationswartung in Management Studio an oder ändern sie  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Maustaste auf einen Auftrag, und klicken Sie dann auf **Eigenschaften**.  
  
4.  In der **Auftragseigenschaften - \< Auftrag>** im Dialogfeld ändern Sie die Eigenschaften bei Bedarf, und klicken Sie dann auf **OK**.  
  
### So zeigen Sie Eigenschaften für einen Auftrag zur Replikationswartung im Replikationsmonitor an oder ändern sie  
  
1.  Erweitern Sie im Replikationsmonitor eine Verlegergruppe, und wählen Sie dann einen Verleger aus.  
  
2.  Klicken Sie auf die Registerkarte **Agents** .  
  
3.  Mit der rechten Maustaste eines Auftrags im Raster, und klicken Sie dann auf **Eigenschaften**.  
  
4.  In der **Auftragseigenschaften - \< Auftrag>** im Dialogfeld ändern Sie die Eigenschaften bei Bedarf, und klicken Sie dann auf **OK**.  
  
## Siehe auch  
 [Starten Sie und beenden Sie eines Replikations-Agents & #40. SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  